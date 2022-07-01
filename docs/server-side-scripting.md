# 1. Server-side Scripting
**Server-side scripts execute on the ServiceNow server or database.**

Some examples:
* Update record fields when a database query run.
* Set field values on related records when a record is saved.
* Send email.
* Send REST messages and retrieve results.


## 1.1 Business Rules
Business Rules are server-side logic that execute when database records are queried, updated, inserted, or deleted.
Use business rules to automatically change values in form fields when the specified conditions are met.

*To create a Business Rule: open System Application Studio -> Create Application File -> Type Business Rule in Filter.*

```
Key: "interact with the databases".
```
When Business Rules Run
* **before**: execute logic before a database operation occurs. For example, concatenate two fields values and write the concatenated values to the Description field.
* **after**:  execute logic immediately after a database operation occurs and before the resulting form is rendered for the user (Waiting for complete).
* **async**: execute logic after a database operation occurs (Not waiting like **after**).
* **display**:  execute logic when a form loads and a record is loaded from the database.



<div align="center"><img style="display: block; margin-left: auto;margin-right: auto;" src="https://developer.servicenow.com/app_store_learnv2_scripting_sandiego_serverscripting_images_script_brprocessflow.png" alt="business-rules-process-flow" height="400px"></div>

<div align="center">Process Flow of Business Rules</div>

<hr>

![image](https://user-images.githubusercontent.com/58679620/176623297-e6326b5e-7a00-4f8f-950e-b955da832f9e.png)

<div align="center">Example of Business Rule</div>

## 1.2 Business Rule Actions
Using for set fields values, Add a message to the top of a form, Abort the Business Rule execution.

```
Notes: Client-side Script also can set fields values with GlideForm (g_form) and GlideUser (g_user).
```

## 1.3 Business Rule Scripts
Use the server-side API. Some actions:

* Invoking web services.
* Changing field values.
* Modifying date formats.
* Generating events.
* Writing log messages.


![image](https://user-images.githubusercontent.com/58679620/176623586-0286aeab-eb1c-47b0-8acb-0811415a9123.png)

<div align="center">Example of Business Rule Script</div>

UPDATING......

## GlideRecord
The GlideRecord class is the way to interact with the ServiceNow database from a script. 

See more: [GlideRecord API](https://developer.servicenow.com/dev.do#!/reference/api/sandiego/server/c_GlideRecordScopedAPI)

```
NOTE: The GlideRecord API discussed here is a server-side API. 
There is a client-side GlideRecord API for global applications. 
The client-side GlideRecord API cannot be used in scoped applications.
```

## GlideDateTime
GlideDateTime methods to perform date-time operations, such as instantiating a GlideDateTime object, performing date-time calculations,
 formatting a date-time, or converting between date-time formats.


```
(function executeRule(current, previous /*null when async*/ ) {

    // rightnow stores the current time
    var rightnow = new GlideDateTime();
    // Create a GlideDateTime object for the When needed date
    var whenNeeded = new GlideDateTime(current.u_when_needed);
    // Challenge:  Do not allow same-day requests
    // Get the date portion of rightnow and whenNeeded (no timestamp)

    // If the When needed date is before rightnow, do not write the record to the database
    // Output an error message to the screen
    if (whenNeeded.before(rightnow)) {
        gs.addErrorMessage("When needed date cannot be in the past.  Your request has not been saved to the database.");
        current.setAbortAction(true);
    }
    var today = rightnow.getLocalDate();
    var istoday = whenNeeded.getLocalDate();
    // Compare today and istoday to see if they are the same day
    if (today.compareTo(istoday) == 0) {
        gs.addErrorMessage("You cannot submit NeedIt requests for today.");
        current.setAbortAction(true);
    }



})(current, previous);

```

<div align="center">Example of Bussiness Rule prevent users choose a date in the past and today.</div>


## Debugging Business Rules


