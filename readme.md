Check out the demo at: https://upbeat-booth-61589f.netlify.com/

## React Feedback Button

Inspired by teams that need to aggregate feedback on how users interact with their products, the React Feedback Button allows users to opt-in to providing feedback when they perform a specific task by displaying a tooltip with a feedback form.

By keeping the feedback form in a tooltip close to the original interaction, rather than a large modal overlay, the users are not forced to abandon their existing contextual information to assess why they've been presented with a large pop up modal. The React Feedback Button also keeps the subsequent user interactions (and the option to disable the feedback forms) in a tight grouping near the original interaction which provides a more intuitive user experience without disrupting the user's contextual map.

## Install

```
npm install react-feedback-button
```

## Props

```
<FeedbackButton
  tooltipOn = {this.state.tooltipOn}
  ButtonText="Skip"
  TooltipMessage="Would you like to help us out by providing feedback on why you skipped this?"
  Form={this.form()}
  submitFunction={this.formSubmit}
  disableTooltip = {this.toggleTooltip}
  formValidated = {this.state.formValidated}
  buttonFunction = {this.buttonFunction}
/>
```
### tooltipOn = 'Boolean'

The users should be able to opt-out of being presented with feedback questions when they interact with the UI. This property determines if the feedback should be bypassed or not and should be passed in from the global store.

### ButtonText = 'String'

This is the text that the button will display, e.g 'Submit'.

### TooltipMessage = 'String'

Usually this asks the user for permission to collect their feedback.

### Form = 'Func'

The form is passed into the component as a function that returns JSX.

```
form(){
  return (
    <form>
      <div className="form-group">
        <label>Why did you skip this job?</label>
        <select name="reason" onChange={(e) => this.changeHandler(e)}>
          <option disabled selected>Select One</option>
          <option>Not enough budget.</option>
          <option>Job details unclear.</option>
          <option>No previous experience in task.</option>
          <option>Too much additional research needed to quote.</option>
        </select>
      </div>
    </form>
  )
)
```

### submitFunction = 'Func'

This function will be fired after the form's 'Submit' button has been clicked. To allow total control of how the feedback data is handled, this should be set up outside of the component and tailored to your specific needs.

```
formSubmit(){
  axios.post('/feedback', {
      user: 'this.state.user',
      job: 'this.state.currentJobID',
      reason: 'Not enough budget'
    })
    .then(function (response) {
      console.log(response);
    })
    .catch(function (error) {
      console.log(error);
    });
}
```

### disableTooltip = 'Func'

To allow the opt-out link to work, it needs to be able to toggle the tooltipOn property in the global store. This should be set up as a function outside of the component and passed in as a property.

```
toggleTooltip(){
  let newState = {
    ...this.state,
    tooltipOn: !this.state.tooltipOn
  }
  this.setState(newState);
}
```

### formValidated = 'Boolean'

If you need your form validated, the validation should happen outside of the component, and passed in as a boolean prop.

```
formValidate(formField, value){
  return(this.state.formField.length > 0)
}
```

### buttonFunction = 'Func'

This is the original action of the button that you are seeking feedback for. This function will fire last.

```
buttonFunction(){
  /* Do something... */
}
```
