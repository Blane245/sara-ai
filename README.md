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
| DueDate | null for appoint or not define, or the date the item is due |
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
## List Access
The list of owners who can access a list ownned by someone else
| Item | Description |
|------|-------------|
| uid | unique ID|
| ActivityList | the key of the activity list being accessed |
| User | the key of the user given access |
| AcccessType | read or write |
# Use Cases
## Add User
performed by administrator. 
Creates a user and Activity list record for the user
Modify, display, and delete use cases available
Display provides read access to user's activity list
## Set Context
when user logs in, context is set to user's activity list, write
## Request to access another activity list
context is set to named activiy list if user is authorized, read or write based on permission
## Add task (requires write access)
user provides name, priority (default) normal, DueDate (optional), reminder time (optional)

