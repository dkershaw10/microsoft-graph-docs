# Microsoft Graph permissions reference 

[Calendars.Read](#Calendars_Read) [Group.ReadWrite.All](#Group_ReadWrite_All) [User.Read](#User_Read)

<a name="Calendars_Read"></a>
## Calendars.Read

### Permission Types
**App-only**

Azure AD portal display: Read calendars in all mailboxes<br/>
Admin consent required: Yes

Allows the app to read events of all calendars without a signed-in user. 

**Delegated**

Azure AD portal display: Read user calendars<br/>
Admin consent required: No

Allows your app to read events in user calendars. 

### Common Scenarios
**App-only**

* Your app reads users' calendars in an organization and publishes schedules for a meeting room. 


<a name="Group_ReadWrite_All"></a>
## Group.ReadWrite.All
### Permission Types
**App-only**

Azure AD portal display: Read and write all groups<br/>
Admin consent required: Yes

Allows your app to create groups, read and update group memberships, and delete groups without the presence of a signed-in user. 

**Delegated**

Azure AD portal display: Read and write all groups<br/>
Admin consent required: Yes

Allows your app to create groups and read all group properties and memberships on behalf of the signed-in user.  Additionally allows group owners to manage their groups and allows group members to update group content. 

### Details

App-only support is limited to APIs for core group administration and management. 

Examples of group features that support app-only permissions: 

* Creating and deleting groups
* Getting and updating group properties pertaining to group administration or management
* Group [directory settings](../api-reference/v1.0/resources/directoryobject.md), type and synchronization
* Group owners and membership


Examples of group features that do not support app-only permissions:

* Group conversations, events, photo
* External senders, accepted or rejected senders, group subscription
* User favorites and unseen count

For more information, see [known issues](../overview/release_notes.md#groups).


### Common Scenarios
**App-only**

* Your service app creates groups. 

**Delegated**

* Your app presents a group-picker that lets a user join a group by choosing from an enumerated list of Office 365 groups that is based on search criteria entered by the user. The app needs to both discover (find) Office 365 groups and update the membership of the chosen group.
* Your app lets a user create groups. 

<a name="User_Read"></a>
## User.Read

### Permission Types
**App-only**

Not Supported

**Delegated**

Azure AD portal display: Sign-in and read user profile<br/>
Admin consent required: No

Allows users to sign-in to your app and allows your app to read the (full) profile of the signed-in user. Also allows your app to read the following basic company information of the signed-in user (through the [Organization](../api-reference/v1.0/resources/organization.md) resource): tenant ID, tenant display name, and verified domains. 

### Details
The full profile includes all of the declared properties of the [User](../api-reference/v1.0/resources/user.md) resource. <br/><br/>This permission doesn't allow your app to read relationships (navigation properties), such as manager or direct reports; for these privileges, see _User.Read.All_ or _User.ReadBasic.All_.

### Common Scenarios
**Delegated**
* Your app reads the full user profile for the signed in user. This will not include relationships. To see relationships, request _User.ReadBasic.All_ or _User.Read.All_.
* Your app reads files, mail and calendar information for the signed in user. Combine _User.Read_ with  _Files.Read_, _Mail.Read_, _Calendars.Read_  (Enable sign-in and read user profile, Read users' files,  Read user mail,  Read user calendars)
* Your app reads  the signed-in user's files (my) and files that other users have shared with the signed-in user (me). Combine  _User.Read_ with  _Files.Read_, _Sites.Read.All_ (Enable sign-in and read user profile, Read users' files,  Read items in all site collections )
