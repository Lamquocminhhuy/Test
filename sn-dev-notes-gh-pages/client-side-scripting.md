### 1. Client-side Scripting

Client-side scripts execute within a user's browser and are used to manage forms and form fields.

For examples: infor or warning message when user working with form and form fields, or hide fields,.... 

* Client Scripts
* UI Policy Scripts

**Client Scripts and UI Policies both execute client-side logic and use the same API**

  
#### 1.1. Client Script Types

- Loaded **(onLoad)**: execute when form is loaded.
- Changed **(onChange)**: execute when one or more fields in form changed.
- Submitted **(onSubmit)**: execute when form is submitted, saved, or updated.
- Cell Edit **(onCellEdit)**: using when user changing in list view (working with list).

#### 1.2. GlideForm (g_form)

The GlideForm client-side API provides methods for managing form and form fields including methods to:

More details: [GlideForm API](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/client/c_GlideFormAPI)

- Retrieve a field value on a form
- Hide a field
- Make a field read-only
- Write a message on a form or a field
- Add fields to a choice list
- Remove fields from a choice list

##### Some methods:

```javascript
getValue(), addOption(), clearOptions(), addInfoMessage(), addErrorMessage(), showFieldMsg().....
```

#### 1.3. GlideUser (g_user)

To find information about the current logged in user and user roles.
More details: [Glide User API](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/client/c_GlideUserAPI)

Example:

```javascript
alert("g_user.firstName = " + g_user.firstName
   + ", \n g_user.lastName = " + g_user.lastName
   + ", \n g_user.userName = " + g_user.userName
   + ", \n g_user.userID = " + g_user.userID);
```

#### 1.4. Examples Client-side Script
  Exercise: [Client-side Script](https://developer.servicenow.com/dev.do#!/learn/courses/sandiego/app_store_learnv2_scripting_sandiego_scripting_in_servicenow/app_store_learnv2_scripting_sandiego_client_side_scripting/app_store_learnv2_scripting_sandiego_exercise_create_client_scripts)

**Set the Requested for to the currently logged in user for new records.
User can change the field value.**

```javascript
function onLoad() {
  //Check to see if the form is for a new record.  If it is a new record,
  //set the Requested for value to the currently logged in user.

  if (g_form.isNewRecord()) {
      g_form.setValue('u_requested_for', g_user.userID);
  }
}
```

**Only display What needed choices that match the Request type value.**

```javascript
function onChange(control, oldValue, newValue, isLoading, isTemplate) {
  if (newValue == '') {
      return;
  }


  var whatneeded = g_form.getValue('u_what_needed');

  // Clear all of the choices from the What needed field choice list
  g_form.clearOptions('u_what_needed');

  // If the value of the Request type field is hr, add
  // two hr choices and other to the What needed field choice list
  if (newValue == 'hr') {
      g_form.addOption('u_what_needed', 'hr1', 'Human Resources 1');
      g_form.addOption('u_what_needed', 'hr2', 'Human Resources 2');
      g_form.addOption('u_what_needed', 'other', 'Other');
  }
  // If the value of the Request type field is facilities, add
  // two facilities choices and other to the What needed field
  // choice list
  if (newValue == 'facilities') {
      g_form.addOption('u_what_needed', 'facilities1', 'Facilities 1');
      g_form.addOption('u_what_needed', 'facilities2', 'Facilities 2');
      g_form.addOption('u_what_needed', 'other', 'Other');
  }
  // If the value of the Request type field is legal, add
  // two legal choices and other to the What needed field
  // choice list
  if (newValue == 'legal') {
      g_form.addOption('u_what_needed', 'legal1', 'Legal 1');
      g_form.addOption('u_what_needed', 'legal2', 'Legal 2');
      g_form.addOption('u_what_needed', 'other', 'Other');
  }

  // If the form is loading and it is not a new record, set the u_what_needed value to the
  // value from the record before it was loaded
  if (isLoading && !g_form.isNewRecord()) {
      g_form.setValue('u_what_needed', whatneeded);
  }
}
```
#### 1.5. UI Policy

UI Policies have a condition as part of the trigger **(UI Policy Action)**.

UI Policies can take different actions when conditions return true or false.

UI Policy Actions do not require scripting to set field attributes:
* Mandatory
* Visible
* Read only

UI Policy Scripts are only visible in the Advanced view. There are "**Execute if true**" and "**Execute if false**" conditions.

```
The Reverse if false option must be selected for the Execute if false script to run.
```

#### 1.6. Review your knowledge

| Criteria                                | Client Script | UI Policy |
| --------------------------------------- | ------------- | --------- |
| Execute on form load                    | Yes           | Yes       |
| Execute on form save/submit/update      | Yes           | No        |
| Execute on form field value change      | Yes           | Yes       |
| Have access to field's old value        | Yes           | No        |
| Execute after Client Scripts            | No            | Yes       |
| Set field attributes with no scripting  | No            | Yes       |
| Require control over order of execution | Yes           | Yes       |


[Click here](https://developer.servicenow.com/dev.do#!/learn/learning-plans/sandiego/new_to_servicenow/app_store_learnv2_scripting_sandiego_test_your_client_side_scripting_knowledge)
