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

### Remarks

NOTE: How is this differrent from the Group permissions as these give access to Group calendars (i assume that the calendars perms don't). Might want to have a scenario demonstrating this too. Scenarios below are just guesses -- the workload teams should supply these.


### Example Scenarios
**Delegation**

* _Clanendars.Read_ : Your App reads the calendars of the signed-in user.
* _Calendars.ReadWrite_ : Your app reads the calendars of the signed-in user and creates events for the signed-in user. 
* _Calendars.ReqdWrite.Shared_ : Your app can read and create delete or update events in all calendars that the signed-in user can access. For organizational accounts this access is dependent upon the security groups and directoryRoles that the signed-in user is a member of. For personal Microsoft accounts the access is limited to the signed-in user. 

**Application**

* _Calendars.Read_ : Your app reads the calendars of all users in your organization and publishes schedules for meeting rooms. 
* _Calendars.ReadWrite_ : Your app reads the calendars of all users in your organization and has the ability to create, update, or delete events for all users.
* Scenario 3

For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

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

Group functionality is not supported on personal Microsoft accounts. (How would this perm show up on a consent page presented to a personal account?)

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

* _Group.ReadWrite.All_ : Your app presents a group-picker that lets the signed-in user join a group by choosing from an enumerated list of Office 365 groups that is based on search criteria entered by the user. The app needs to both discover (find) Office 365 groups and update the membership of the chosen group.
* _Group.ReadWrite.All_ : Your app lets the signed-in user create groups. 
* scenario 3

**Application**

* _Group.ReadWrite.All_ : Your service app creates groups. 
* Scenario 2
* Scenario 3

For more complex scenarios involving multiple permissions, see \<Permission Scenarios Topic\>.

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

The full profile includes all of the declared properties of the [User](../api-reference/v1.0/resources/user.md) resource. Because the profile might contain sensitive directory information or personally identifiable information (PII), the _User.ReadBasic.All_ permission constrains app access to a limited set of properties known as a basic profile. For users, the basic profile includes only the following properties: 

- Display name
- First and last name
- Photo
- Email address

### Example Scenarios
**Delegated**

* _User.Read_ : Your app reads the full user profile for the signed in user. This will not include relationships. To see relationships, request _User.ReadBasic.All_ or _User.Read.All_. For organization accounts, basic company information can also be read -- DO YOU HAVE TO READ THE organization RESOURCE FOR THIS?
* _User.ReadBasic.All_ : Your app can read the basic profile of all users the directory. For LOB or organizations, this allows your app to read relationships like manager and directReports. HOW IS THIS DIFFERENT FOR PERSONAL ACCOUNTS -- i.e WHAT KIND OF RELATIONSHIPS CAN THEY READ?
* _User.Read_,  _Files.Read_, and _Sites.Read.All_ : Your app reads  the signed-in user's files and files that other users have shared with the signed-in user. NOT SURE WHETHER WE WOULD SHOW SCENRIOS w/ MULTIPLE PERMS LIKE THIS. THEY MIGHT FIT BETTER IN THE PERMISSION SCENARIOS TOPIC.

**Application Permissions**

* Scenario 1
* Scenario 2
* Scenario 3

For more complex scenarios involving multiple permissions, see \<Permission Scenarios Topic\>.
