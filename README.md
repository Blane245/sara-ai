# Activity Structure
## Activities
| Item | Description |
| uid | unique ID |
| ActivityList | the key of the activity list that owns this ativity List |
| Type | task, recurring task, calendar event, recurring calendar event |
| recurrence pattern | null, or RecurEvery, DOYs, EndBy |
| Status | Not Started, In Progress, Completed, Waiting for someone else,  Deferred |  
| Priority | Low, Normal, High |
| Name | the name of the item (no necessarily) unique |
| DateAdded | the date/time the item eas added |
| AddedBy | the user who added the item |
| DateModified | the date/time of last modification |
| Modified By | the user who updated teh item |
| DueDate | null for appoint or not define, or the date the item is due |
| RemainderTime | null if none, or TOD |
| StartDateTime | null for task, or DateTime for appointment |
| EndDateTime | null for task, or DateTime for appointment |
## Activity List
| Item | Description |
| uid | unique ID|
| Owner | the name of the user that owns the list (unique) |
## Users
| Item | Descripion |
| uid | unique ID |
| Name | the name of a person (unique) |
## List Access
The list of owners who can access a list ownned by someone else
| Item | Description |
| uid | unique ID|
| ActivityList | the key of the activity list being accessed |
| User | the key of the user given access |
| AcccessType | read or write |


