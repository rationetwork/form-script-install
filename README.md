# Clear Choice Setup 

Get set up with a form and / or results that you can use to introduce your site's visitors to Choose Wisely’s award winning personal loan comparison service.

- No API calls.
- No iFrames.
- No REST responses.

It works by running a stand-alone application form on your site. Your visitors complete the form and are then redirected to a comparison table powered by Choose Wisely where we will match them with their best available options.  
 
## Get Started
Your code snippet comes in two parts. 
### Part 1, Container Tag
Paste this where you want the form to run on your site.

```html
<div id="ccApply"></div>
```

### Part 2, The Script
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

## Configuration Settings
ccBundle accepts the object `clearChoice_conf` as configuration with the following options.

### Form Specific
| Name            | Type     | Default       | Description                                                                                                                                                                                                    |
| --------------- | -------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| key             | String   | REQUIRED      | Your affiliate key, must be a valid key with no spaces.                                                                                                                                                        |
| ref             | String   | `''`          | Your affiliate reference, must be a valid reference with no spaces (max 48 characters).                                                                                                                        |
| gclid           | String   | `''`          | Your unique click id tracking parameter, must not contain spaces (max 100 characters).                                                                                                                         |
| elemId          | String   | `'ccApply'`   | Id of the element where your form will render, must be a valid id with no spaces.                                                                                                                              |
| theme           | Enum     | `''`          | Apply one of the predefined themes to the form using a theme from the [list below](#themes).                                                                                                                   |
| mode            | Enum     | `'Redirect'`  | Define behaviour after the form has been submitted, use one of the predefined modes from the [list below](#modes).                                                                                             |
| submitText      | String   | `'Get Quote'` | The text that will show inside your submit button.                                                                                                                                                             |
| onSubmit        | Function | `NOOP`        | Callback that will run when the form is submitted. Contains customer data. Can be used to send events to analytics platforms like GA.                                                                          |
| sendingText        | String | `''`        | Message that the user will see after clicking the submit button on the form.  Also includes a loading bar.                                                                                                      |
| continueText      | String   | `'Continue'` | The button text that shows next to input fields when they are valid.                                                                                                                                          |
| loanAmount      | Integer  | `1000`        | Loan amount for application. You may want to pass this to the form from your landing page.                                                                                                                     |
| loanTerm        | Integer  | `12`          | Loan term for application. You may want to pass this to the form from your landing page.                                                                                                                       |
| alwaysShowFirstStage      | Boolean  | `false`        | Always start on the first stage of the form. Useful if you want to set a default `loanAmount` and or `loanTerm` but stil want to show these fields.                                                 |
| showInputWarnings      | Boolean  | `true`        | Show or hide warnings if users enter data that passes validation but looks suspect.                                                                                                                     |
| laMax           | Integer  | `1000`        | Maximum Loan amount accepted by the form. Must be less than or equal to 25000.                                                                                                                                 |
| laMin           | Integer  | `100`         | Maximum Loan amount accepted by the form. Must be more than or equal to 100.                                                                                                                                   |
| laStep          | Integer  | `100`         | The amount you want to increment the loan amount slider by.                                                                                                                                                    |
| fixedControls   | Boolean  | `true`        | The form has fixed controls at the bottom of the screen. Setting fixedControls to false forces these controls to sit directly under the form fields. Use this if you want to control the height of your form.  |
| laMarks         | Object   | `{}`          | Loan amount marks for the slider.                                                                                                                                                                              |
| ltMarks         | Boolean  | `false`       | Add loan term marks to the loan term slider.                                                                                                                                                                   |
| termsConditions | String   | `''`          | Absolute URL of your terms and conditions page. This will include a link to your terms and conditions on the submit stage                                                                                      |
| privacyPolicy   | String   | `''`          | Absolute URL of your privacy policy page. This will include a link to your privacy policy on the submit stage                                                                                                  |
| hideLoanAmountStage | Boolean   | `false`          | If you are providing the loanAmount configuration setting, this setting will remove the loan amount stage from the form completely.                                                                    |
| hideLoanTermStage   | Boolean   | `false`          | If you are providing the loanTerm configuration setting, this setting will remove the loan term stage from the form completely.                                                                        |
| onSubmit        | Function | `NOOP`        | Callback that will run when the form is submitted. Single parameter contains the anonymised form data. Can be used to send events to analytics platforms like GA.                                              |

### Results Specific
The configuration options below are for the **form and results** and **results only** integration methods. These are only used when the `mode` configuration is set to `Results`.

| Name                | Type     | Default       | Description                                                                                                                                                                                                    |
| ------------------- | -------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| onResultsSuccess    | function | `NOOP`        | Callback that will run in `Results` mode when the results are returned but before they are displayed. Single parameter contains the array of results.                                                      |
| onResultsError      | function | `NOOP`        | Callback that will run in `Results` mode when the API request fails. Single parameter contains details of the error.                                                                                       |

The configuration options below are only for the **results only** integration method.

| Name                | Type     | Default       | Description                                                                                                                                                                                                                             |
| ------------------- | -------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| applicantEvent      | Boolean  | `false`       | Setting this to `true` will put the application in a dormant state, it will enable an event listener that will only render and display the application process and then comparison results once it receives data. See the [example event](#applicant-event) below for the required event type. |
| resultsEvent        | Boolean  | `false`       | Setting this to `true` will put the application in a dormant state, it will enable an event listener that will only render and display the comparison results once it receives data. See the [example event](#results-event) below for the required event type. |
| applicantPayload    | Object   | ``            | Use this to pass your applicant form data in the required format, it will render and display the application process and then comparison results immediately. See the [example payload](#applicant-payload) below for the required syntax. |
| resultsPayload      | Object   | ``            | Use this to pass the result payload received from the [Choose Wisely White Label Results API](https://app.swaggerhub.com/apis/Ratio4/choosewisely-white-label-resuts/1.02), the application will render and display the comparison results immediately. See the [example payload](#successful-results-response--payload) below for the required syntax. |

### Settings Example
```js
  window.clearChoice_conf = window.clearChoice_conf || {};
  clearChoice_conf = {
    key: 'KCB3FDCD-ABCD-1234-9HGD-123CVRGVE4FE',
    ref: '1234', 
    elemId: 'ccApply', 
    theme: 'ChooseWisely',
    submitText: 'Get my quote', 
    continueText: 'Go', 
    loanAmount: 2000,
    alwaysShowFirstStage: true,
    showInputWarnings: false,
    loanTerm: 15,
    laMax: 10000,
    laMin: 100,
    laStep: 100,
    fixedControls: true,
    onSubmit: function(formData){
      // formData contains submitted data
      console.log(formData);
      
      // Send an event to google analytics.
      window.ga('send', {
        hitType: 'event',
        eventCategory: 'Form',
        eventAction: 'Submit',
        eventLabel: formData.loanAmount + '|' + formData.loanTerm,
      });
    },
    onResultsSuccess: function(results){
      console.log(results);
    },
    onResultsError: function(error){ 
      console.log(error);
    },
    laMarks: {
      1000: '£1k',
      3000: '£3k',
      5000: '£5k',
      10000: '£10k',
      20000: '£20k',
    },
    termsConditions: 'https://www.yourdomain.com/terms-and-conditions',
    privacyPolicy: 'https://www.yourdomain.com/privacy-policy'
  };
```

## Layout
Higher conversion rates can be expected if you run the application on a stand alone page with minimal navigation and no footer. This also requires the minimum level of styling work to get running. For a working example [see Choose Wisely's own form](https://www.choosewisely.co.uk/loans/short-term-loan-search/apply)


## Styling

[See a basic demo here](https://jsfiddle.net/ratio/1aq4up3j/) where the colors have been changed.

[This more advanced demo](https://jsfiddle.net/ratio/xr2n8675/) shows how you can lay out the multi choice boxes in a grid.

The form and results have their own stylesheets and a set of basic styles. The stylesheets are loaded asynchronously using javascript to prevent any render blocking by the browser. This stylesheets are prepended to the top of the `<head/>` tag. To override the default styles you will need to modify your sites stylesheets.


### Themes
The form and results have a list of prestyled themes that can be applied, use a theme name from the table below in your form settings configuration.

| Name             | Decription                                         |
| ---------------- | -------------------------------------------------- |
| `ChooseWisely`   | Styled to look like the default Choose Wisely form |

### CSS
The form is wrapped in the class `.ccAppForm`, all form elements are prefixed with this class e.g. `.ccAppForm--button`.
The comparison results are wrapped in `.ccAppResults`, and all result elements are prefixed with this class e.g. `.ccAppResults--result--button`.
This is to prevent the forms styles from affecting other elements on your site. Below are some example selectors.

#### Form Validation 

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

```css
.ccAppResults .ccAppResults--result--button {
  background-color: #007bff;
  border-color: #007bff;
  color: #fff;
}
```

## Comparison Results
After your visitors complete the form you now have the option to show them the Choose Wisely powered comparison table where we will have matched them with their best available options directly on your site.


### Modes
There are two journey options for a customer once they submit the form. The customer can redirect through to Choose Wisely
for their application process and their unique set of comparison results. Or the application process and their comparison table of results can be displayed directly on your site within the `elemId` element.

| Name        | Decription                                         |
| ------------| -------------------------------------------------- |
| `Redirect`  | Once the form is submitted, the user will redirect to Choose Wisely to display the results of their application.                                                                      |
| `Results`   | Once the form is submitted, the user will be presented with the application submission process, after which, their application results will be presented all within the same element. |

### Example Responses & Events

#### Applicant Event
Pass the customer form data into the `detail` part of the event object in the [Choose Wisely White Label Results API](https://app.swaggerhub.com/apis/Ratio4/choosewisely-white-label-resuts/1.02) format.
 
```js
dispatchEvent(new CustomEvent('cargoApplicant', {
  bubbles: true,
  detail: {
    "loanAmount": 2000,
    "loanTerm": 24,
    "title": "Mr",
    "firstName": "Frank",
    "lastName": "Zappa",
    "dob": "1981-07-29T23:00:00.000Z",
    "emailAddress": "frank@zappa.com",
    "homePhone": "02078765432",
    "mobilePhone": "07976543214",
    "workPhone": "07976543214",
    "maritalStatus": "Single",
    "residentialStatus": "Homeowner",
    "employmentStatus": "FullTime"
  }
}));

```

#### Results Event
Pass the result data returned from the Choose Wisely White Label Results API into the `detail` part of the event object.

```js
dispatchEvent(new CustomEvent('cargoResults', {
  bubbles: true,
  detail: {
    "apiResult": "success",
    "result": "",
    "errors": [],
    "warnings": [],
    "loanAmount": 2000,
    "loanTerm": 24,
    "customerId": 12345,
    "customerUid": "abc123",
    "provisionalAccepts": [],
    "lenders": [
      {
        "headline": "Accepted for £2000 if you can provide a suitable guarantor.",
        "lenderType": [
          "Guarantor"
        ],
        "resultType": [
          "primary"
        ],
        "approved": true,
        "redirectPath": "/secondary/forward/abc",
        "_id": "abc",
        "applicationURL": [],
        "lenderName": "A lender",
        "logo": "https://logo.com/logo.gif",
        "representativeExample": "If you borrow £3,500.00 over 36 months at a Representative rate of 61.8% APR and an annual interest rate of 49.10% (fixed), you would pay 36 monthly installments of £187.51. The total charge for credit will be £3,250.36 and the total amount payable will be £6,750,36.",
        "apr": 49.7,
        "loanTermType": "Months",
        "totalCreditCost": 2963.76,
        "premium": 123.49
      },
      {
        "headline": "This lender has declined your application",
        "lenderType": [
          "Specialist"
        ],
        "resultType": [
          "declined"
        ],
        "approved": false,
        "redirectPath": "",
        "_id": "abc",
        "applicationURL": [],
        "lenderName": "Lender 2",
        "logo": "https://logo.com/logo.gif",
        "representativeExample": "Amount of credit: £500. Interest rate: 0.8% per day for up to 40 days (292% per annum (variable). Representative 68.7% APR (variable).",
        "apr": 68.7,
        "loanTermType": "Days",
        "totalCreditCost": 0,
        "premium": 0
      }
    ]
  }
}));
```

#### Applicant Payload
This is an example applicant payload in the [Choose Wisely White Label Results API](https://app.swaggerhub.com/apis/Ratio4/choosewisely-white-label-resuts/1.02) format.

```json
{
  "loanAmount": 2000,
  "loanTerm": 24,
  "title": "Mr",
  "firstName": "Frank",
  "lastName": "Zappa",
  "dob": "1981-07-29T23:00:00.000Z",
  "emailAddress": "frank@zappa.com",
  "homePhone": "02078765432",
  "mobilePhone": "07976543214",
  "workPhone": "07976543214",
  "maritalStatus": "Single",
  "residentialStatus": "Homeowner",
  "employmentStatus": "FullTime"
}
```

#### Successful Results Response / Payload
This is an example response returned from the Choose Wisely White Label Results API.

```json
{
  "apiResult": "success",
  "result": "",
  "errors": [],
  "warnings": [],
  "loanAmount": 2000,
  "loanTerm": 24,
  "customerId": 12345,
  "customerUid": "abc123",
  "provisionalAccepts": [],
  "lenders": [
    {
      "headline": "Accepted for £2000 if you can provide a suitable guarantor.",
      "lenderType": [
        "Guarantor"
      ],
      "resultType": [
        "primary"
      ],
      "approved": true,
      "redirectPath": "/secondary/forward/abc",
      "_id": "abc",
      "applicationURL": [],
      "lenderName": "A lender",
      "logo": "https://logo.com/logo.gif",
      "representativeExample": "If you borrow £3,500.00 over 36 months at a Representative rate of 61.8% APR and an annual interest rate of 49.10% (fixed), you would pay 36 monthly installments of £187.51. The total charge for credit will be £3,250.36 and the total amount payable will be £6,750,36.",
      "apr": 49.7,
      "loanTermType": "Months",
      "totalCreditCost": 2963.76,
      "premium": 123.49
    },
    {
      "headline": "This lender has declined your application",
      "lenderType": [
        "Specialist"
      ],
      "resultType": [
        "declined"
      ],
      "approved": false,
      "redirectPath": "",
      "_id": "abc",
      "applicationURL": [],
      "lenderName": "Lender 2",
      "logo": "https://logo.com/logo.gif",
      "representativeExample": "Amount of credit: £500. Interest rate: 0.8% per day for up to 40 days (292% per annum (variable). Representative 68.7% APR (variable).",
      "apr": 68.7,
      "loanTermType": "Days",
      "totalCreditCost": 0,
      "premium": 0
    }
  ]
}
```
