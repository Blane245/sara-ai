# Questions
# Activity Structure
These are the records that make up the sara-ai database. The primary entries are Activitiy lists and users. Each user may have one
activity list. The list owner may grant access persmissions to other users. An activity list can consist of any number of activities. 
## Activities
| Item | Description |
|------|-------------|
| uid | unique ID |
| ActivityList | the key of the activity list that owns this ativity List |
| Name | the name of the item (no necessarily) unique |
| Type | task, recurring task, calendar event, recurring calendar event |
| recurrence pattern | null, or RecurEvery, DOYs, EndBy |
| Status | Not Started, In Progress, Completed, Waiting for someone else,  Deferred |  
| Priority | Low, Normal, High |
| DateAdded | the date/time the item eas added |
| AddedBy | the user who added the item |
| DateModified | the date/time of last modification |
| Modified By | the user who updated teh item |
| DueDate | null for appoint or not defined, or the date the item is due |
| Remainder | null if none, or TOD |
| StartDateTime | null for task, or DateTime for appointment |
| EndDateTime | null for task, or DateTime for appointment |
## Activity List
| Item | Description |
|------|-------------|
| uid | unique ID|
| Owner | the name of the user that owns the list (unique) |
## Users
| Item | Descripion |
|------|-------------|
| uid | unique ID |
| Name | the name of a person (unique) |
## Nicknames
A user may have zero or more nicknames
| Item | Descripion |
|------|-------------|
| uid | unique ID |
| OwnerName | name of the owner of this nickname |
| Name | the name of a person |
| Nickname | the nickname of the person |

## List Access
The list of owners who can access a list ownned by someone else
| Item | Description |
|------|-------------|
| uid | unique ID|
| ActivityList | the key of the activity list being accessed |
| User | the key of the user given access |
| AcccessType | read or write |
# Use Cases
## (Add, Modify, Delete) User
performed by administrator. 
Creates a user and Activity list record for the user
Modify, display, and delete use cases available
### Intent
'Add user $(NAME)'
### Responses
'You are not authorized to add users to Sara'  
'$(p.NAME) already exists  
'$(p.NAME) added  
### Processing
* only administrator can add users
* only one copy of a user can exist
* Add the user and an activity list for the user to the data base
### Intent
'(Rename | Modify) user $(NAME) to $(NEWNAME)'
### Responses
'You are not authorized to modify users in Sara'  
'$(p.NEWNAME) already exists  
'$(p.NAME) renamed to (p.NEWNAME)'  
### Processing
* only administrator can modify users
* only one copy of a user can exist
* modify the user anem and the activity list for the user in the database
### Intent
'Delete user $(NAME)'
### Responses
'You are not authorized to delete users from Sara'  
'$(p.NAME) does not exist  
'$(p.NAME) deleted'  
### Processing
* only administrator can delete users
* user must exist
* TODO use a confirmation dialog before allowing deletion
## Nicknames
Users may have nicknames. Anyone can add a nickname to anyone else, bu thte nickname must be unique.
### Intent
'Add $(NICKNAME) (for $(USERNAME) |)
### Responses
`$(NICKNAME) is already being used for $(USERNAME2)`
`$(NICKNAME) added for you`
`$(NICKNAME) added for $(USERNAME)`
### Processing
* Nickname must be unique
* Nickname added to current user or named user
### Intent
'(Remove | delete) $(NICKNAME)'
### Response
`$(NICKNAME) does not exist`
`$(NICKNAME) removed`
### Processing
* nickname must exist
* nickname deleted
## List Users
This will list all users and their nicknames
### Intent 
'(list | show me | tell me) (all | ) users'
### Responses
for all defined users:
* `$(USERNAME) has no nicknames`
* `$(USERNAME) has nicknames $(NICKNAMELIST)`
## Set activity list access
### Login activity list
when user logs in, context is set to user's activity list, write
### Request to access another activity list
context is set to named activiy list if user is authorized, read or write based on permission
## Set day context
identify which day is to be used for display (today, tomorrow, yesterday, monday ... Sunday, date). Default is today
## Activity maintenance
### Add (task, event) (requires write access)
user provides name, priority (default) normal, DueDate (optional), reminder time (optional)
### Change (task, event) [attribute] (requires write access)
user provides original name and new attribute value (type checked)
### Delete (task, event) (requires write access)
user provides original name. Confirmation dialog occurs
### Special maintenance use cases
#### Set (task, event) (not started, in progress, completed, waiting, deferred)
A short form of 'Change (task, event) priority'
## Activity display
### (List, Say) (all, not started, in progress, completed, waiting, deferred tasks) tasks
### (List, Say) (all, not started, in progress, completed, waiting, deferred tasks) events
# Behaviors
## Not completed Task roll over
All tasks that are not completed are in the list of tasks whose status is not completed for today even if their due date was in the past
if DueDate is not defined, then it the task is assumed to be due today
## Reminder alert
When a task or event has a reminder, an alert is sent to the user and remains active until acknowledged. This leads to a use case 'Remove reminder (id)' which will remove the reminder


