# Clear choice form setup 

Get set up with a form that you can use to introduce your sites visitors to Choose Wisely’s award winning personal loan comparison service.

- No API calls.
- No iFrames.
- No REST responses.

It works by running a stand-alone application form on your site. Your visitors complete the form and are then automatically redirected to a comparison table on choosewisely where we will match them with their best available options.  
 
## Get started
Your code snippet comes in two parts. 
### Part 1, container tag
Paste this where you want the form to run on your site.

```html
<div id="ccApply"></div>
```

### Part 2, the script
Paste this just before the closing `</body>` tag.

```html
    <script type="text/javascript">
      window.clearChoice_conf = window.clearChoice_conf || {};
      clearChoice_conf = {
        key: 'your-affiliate-key-goes-here',
        ref: 'your-affiliate-reference-goes-here', // Optional
        elemId: 'ccApply', // Container tag id
	theme: 'ChooseWisely' // Optional
      };
    </script>
    <script type="text/javascript" src="https://3pi.choosewisely.co.uk/ccLoader.js"></script>
```

## Form settings
ccBundle accepts the object `clearChoice_conf` as configuration with the following options.


| Name            | Type     | Default       | Description                                                                                                                                                                                                    |
| --------------- | -------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key             | String   | REQUIRED      | Your affiliate key, must be a valid key with no spaces.                                                                                                                                                        |
| ref             | String   | `''`          | Your affiliate reference, must be a valid reference with no spaces.                                                                                                                                            |
| elemId          | String   | `'ccApply'`   | Id of the element where your form will render, must be a valid id with no spaces.                                                                                                                              |
| submitText      | String   | `'Get Quote'` | The text that will show inside your submit button.                                                                                                                                                             |
| onSubmit        | Function | `NOOP`        | Callback that will run when the form is submitted. Contains customer data. Can be used to send events to analytics platforms like GA. |
| sendingText        | String | `''`        | Message that the user will see after clicking the submit button on the form.  Also includes a loading bar. |
| continueText      | String   | `'Continue'` | The button text that shows next to input fields when they are valid.                                                                                                                                          |
| onSubmit        | Function | `NOOP`        | Callback that will run when the form is submitted. Can be used to send events to analytics platforms like GA. |
| loanAmount      | Integer  | `1000`        | Loan amount for application. You may want to pass this to the form from your landing page.                                                                                                                     |
| loanTerm        | Integer  | `12`          | Loan term for application. You may want to pass this to the form from your landing page.                                                                                                                       |
| alwaysShowFirstStage      | Boolean  | `false`        | Always start on the first stage of the form. Useful if you want to set a default `loanAmount` and or `loanTerm` but stil want to show these fields.                                                 |
| showInputWarnings      | Boolean  | `true`        | Show or hide warnings if users enter data that passes validation but looks suspect.                                                                                                                     |
| laMax           | Integer  | `1000`        | Maximum Loan amount accepted by the form. Must be less than or equal to 25000.                                                                                                                                 |
| laMin           | Integer  | `100`         | Maximum Loan amount accepted by the form. Must be more than or equal to 100.                                                                                                                                   |
| laStep          | Integer  | `100`         | The amount you want to increment the loan amount slider by.                                                                                                                                                    |
| ltStep          | Integer  | `1`           | The amount you want to increment the loan term slider by.                                                                                                                                                      |
| fixedControls   | Boolean  | `true`        | The form has fixed controls at the bottom of the screen. Setting fixedControls to false forces these controls to sit directly under the form fields. Use this if you want to control the height of your form.  |
| laMarks         | Object   | `{}`          | Loan amount marks for the slider.                                                                                                                                                                              |
| ltMarks         | Boolean  | `false`       | Add loan term marks to the loan term slider.                                                                                                                                                                              |
| termsConditions | String   | `''`          | Absolute URL of your terms and conditions page. This will include a link to your terms and conditions on the submit stage                                                                                      |
| privacyPolicy   | String   | `''`          | Absolute URL of your privacy policy page. This will include a link to your privacy policy on the submit stage                                                                                                  |
| hideLoanAmountStage | Boolean   | `false`          | If you are providing the loanAmount configuration setting, this setting will remove the loan amount stage from the form completely.                                                                    |
| hideLoanTermStage   | Boolean   | `false`          | If you are providing the loanTerm configuration setting, this setting will remove the loan term stage from the form completely.                                                                        |
| theme           | Enum     | `''`          | Apply one of the predefined themes to the form using a theme from the [list below](#themes)                                                                                    |

### Settings Example
```js
  window.clearChoice_conf = window.clearChoice_conf || {};
  clearChoice_conf = {
    key: 'KCB3FDCD-ABCD-1234-9HGD-123CVRGVE4FE',
    ref: '1234', 
    elemId: 'ccApply', 
    submitText: 'Get my quote', 
    continueText: 'Go', 
    loanAmount: 2000,
    alwaysShowFirstStage: true,
    showInputWarnings: false,
    loanTerm: 15,
    laMax: 10000,
    laMin: 100,
    laStep: 100,
    ltMax: 36,
    ltMin: 3,
    ltStep: 1,
    fixedControls: true,
    onSubmit:function(){
      // Callback, runs when the form is submitted
	window.ga('send', {
	  hitType: 'event',
	  eventCategory: 'Loan application form',
	  eventAction: 'Submit',
	  eventLabel: 'Success'
	});
    },
    laMarks: {
      1000: '£1k',
      3000: '£3k',
      5000: '£5k',
      10000: '£10k',
      20000: '£20k',
    },
    termsConditions: 'https://www.yourdomain.com/terms-and-conditions',
    privacyPolicy: 'https://www.yourdomain.com/privacy-policy',
    theme: 'ChooseWisely',
  };
```

## Layout
Higher conversion rates can be expected if you run the form on a stand alone page with minimal navigation and no footer. This also requires the minimum level of styling work to get running. For a working example [see Choose Wisely's own form](https://www.choosewisely.co.uk/loans/short-term-loan-search/apply)


## Styling the form

[See a basic demo here](https://jsfiddle.net/ratio/1aq4up3j/) where the colors have been changed.

[This more advanced demo](https://jsfiddle.net/ratio/xr2n8675/) shows how you can lay out the multi choice boxes in a grid.

The form has its own stylesheet and a set of basic styles. The stylesheet is loaded asynchronously using javascript to prevent any render blocking by the browser. This stylesheet is prepended to the top of the <head/> tag. To override the default styles you will need to modify your sites stylesheets.


### Themes
The form has a list of prestyled themes that can be applied, use a theme name from the table below in your form settings configuration.

| Name             | Decription                                         |
| ---------------- | -------------------------------------------------- |
| `ChooseWisely`   | Styled to look like the default Choose Wisely form |

### CSS
The form is wrapped in the class `.ccAppForm` all form elements are prefixed with this class e.g. `.ccAppForm--button`. This is to prevent the forms styles from affecting other elements on your site. Below are some example selectors.

#### Validation 

```css
/* Valid */
.ccAppForm .ccAppForm--button--success {
  background-color: green;
  border-color: green;
  color: #fff;
}

.ccAppForm .ccAppForm--success {
  color: green;
  border-color: green;
}


/* Error */
.ccAppForm .ccAppForm--button--error {
  background-color: red;
  border-color: red;
  color: #fff;
}

.ccAppForm .ccAppForm--error {
  color: red;
  border-color: red;
}
```


#### Buttons

```css
.ccAppForm .ccAppForm--button--primary {
  background-color: #007bff;
  border-color: #007bff;
  color: #fff;
}
```
