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


