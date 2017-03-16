# Microsoft Graph permissions reference 

## Delegated permissions
[Calendars.Read](#Calendars_Permissions) | [Calendars.Read.Shared](#Calendars_Permissions) | [Calendars.ReadWrite](#Calendars_Permissions) | [Calendars.ReadWrite.Shared](#Calendars_PLermissions) | [Group.Read.All](#Group_Permissions) | [Group.ReadWrite.All](#Group_Permissions) | [User.Read](#User_Permissions) | [User.ReadWriwe](#User_Permissions) | [User.ReadBasic.All](#User_Permissions) | [User.Read.All](#User_Permissions) | [User.ReadWrite.All](#User_Permissions)

## Application permissions
[Calendars.Read](#Calendars_Permissions) | [Calendars.ReadWrite](#Calendars_Permissions) | [Group.Read.All](#Group_Permissions) |  [Group.ReadWrite.All](#Group_Permissions) | [User.Read.All](#User_Permissions) | [User.ReadWrite.All](#User_Permissions)

---

<a name="Calendars_Permissions"></a>
## Calendars Permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Calendars.Read_ |    Read user calendars  | Allows the app to read events in user calendars.| No |
| _Calendars.Read.Shared_ |    Read user and shared calendars | Allows the app to read events in all calendars that the user can access, including delegate and shared calendars. | No |
| _Calendars.ReadWrite_ |    Have full access to user calendars  | Allows the app to create, read, update, and delete events in user calendars. | No |
| _Calendars.ReadWrite.Shared_ |    Read and write user and shared calendars | Allows the app to create, read, update and delete events in all calendars the user has permissions to access. This includes delegate and shared calendars.| No |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Calendars.Read_ |    Read calendars in all mailboxes  | Allows the app to read events of all calendars without a signed-in user.| Yes |
| _Calendars.ReadWrite_ |    Read and write calendars in all mailboxes | Allows the app to create, read, update, and delete events of all calendars without a signed-in user.| Yes |


### Example Scenarios
**Application**

* Your app reads users' calendars in an organization and publishes schedules for a meeting room. 
* Scenario 2
* Scenario 3

---

<a name="Group_Permissions"></a>
## Group Permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Group.Read.All_ |    Read all groups | Allows the app to list groups, and to read their properties and all group memberships on behalf of the signed-in user.  Also allows the app to read calendar, conversations, files, and other group content for all groups the signed-in user can access. | Yes |
| _Group.ReadWrite.All_ |    Read and write all groups| Allows the app to create groups and read all group properties and memberships on behalf of the signed-in user.  Additionally allows group owners to manage their groups and allows group members to update group content. | Yes |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Group.Read.All_ | Read all groups | Allows the app to read memberships for all groups without a signed-in user. Note that not all group API supports access using app-only permissions. See [known issues](../overview/release_notes.md#groups) for examples. | Yes |
| _Group.ReadWrite.All_ | Read and write all groups | Allows the app to create groups, read and update group memberships, and delete groups. All of these operations can be performed by the app without a signed-in user. Note that not all group API supports access using app-only permissions. See [known issues](../overview/release_notes.md#groups) for examples.| Yes |


### Details

Application permissions support is limited to APIs for core group administration and management. 

Examples of group features that support Application permissions: 

* Creating and deleting groups
* Getting and updating group properties pertaining to group administration or management
* Group [directory settings](../api-reference/v1.0/resources/directoryobject.md), type and synchronization
* Group owners and membership


Examples of group features that do not support Application permissions:

* Group conversations, events, photo
* External senders, accepted or rejected senders, group subscription
* User favorites and unseen count

For more information, see [known issues](../overview/release_notes.md#groups).


### Example Scenarios
**Delegated**

* Your app presents a group-picker that lets a user join a group by choosing from an enumerated list of Office 365 groups that is based on search criteria entered by the user. The app needs to both discover (find) Office 365 groups and update the membership of the chosen group.
* Your app lets a user create groups. 

**Application**

* Your service app creates groups. 

---

<a name="User_Permissions"></a>
## User Permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _User.Read_       |    Sign-in and read user profile | Allows users to sign-in to the app, and allows the app to read the profile of signed-in users. The full profile includes all of the declared properties of the User entity. The app cannot read navigation properties, such as manager or direct reports. Also allows the app to read the following basic company information of the signed-in user (through the **Organization** object): tenant ID, tenant display name, and verified domains.| No |
| _User.ReadWrite_ |    Read and write access to user profile | Allows the app to read your profile. It also allows the app to update your profile information on your behalf. | No |
| _User.ReadBasic.All_ |    Read all user's basic profiles | Allows the app to read the basic profile of all users in the organization on behalf of the signed-in user. The following properties comprise a user’s basic profile: display name, first and last name, photo, and email address. To read the groups that a user is a member of, the app will also require Group.Read.All or Group.ReadWrite.All.| No |
| _User.Read.All_                |     Read all user's full profiles           | Same as User.ReadBasic.All, except that it allows the app to read the full profile of all users in the organization and when reading navigation properties like manager and direct reports. The full profile includes all of the declared properties of the **User** entity. To read the groups that a user is a member of, the app will also require either Group.Read.All or Group.ReadWrite.All. | Yes |
| _User.ReadWrite.All_           |     Read and write all user's full profiles | Allows the app to read and write the full set of profile properties, reports, and managers of other users in your organization, on behalf of the signed-in user. | Yes |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _User.Read.All_ |    Read all users' full profiles | Allows the app to read the full set of profile properties, group membership, reports and managers of other users in your organization, without a signed-in user.| Yes |
| _User.ReadWrite.All_ |   Read and write all users' full profiles | Allows the app to read and write the full set of profile properties, group membership, reports and managers of other users in your organization, without a signed-in user.| Yes |

### Details
The full profile includes all of the declared properties of the [User](../api-reference/v1.0/resources/user.md) resource. Because the profile might contain sensitive directory information or personally identifiable information (PII), several permissions constrain app access to a limited set of properties known as a basic profile. For users, the basic profile includes only the following properties: 

- Display name
- First and last name
- Photo
- Email address


### Example Scenarios
**Delegated**
* Your app reads the full user profile for the signed in user. This will not include relationships. To see relationships, request _User.ReadBasic.All_ or _User.Read.All_.
* Your app reads files, mail and calendar information for the signed in user. Combine _User.Read_ with  _Files.Read_, _Mail.Read_, _Calendars.Read_  (Enable sign-in and read user profile, Read users' files,  Read user mail,  Read user calendars)
* Your app reads  the signed-in user's files and files that other users have shared with the signed-in user. Combine  _User.Read_ with  _Files.Read_, _Sites.Read.All_ (Enable sign-in and read user profile, Read users' files,  Read items in all site collections )
