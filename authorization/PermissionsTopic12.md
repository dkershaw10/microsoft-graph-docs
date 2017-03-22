# Microsoft Graph permissions reference 

[Calendars permissions](#calendars-permissions) | [Contacts permissions](#contacts-permissions) | [Device permissions](#device-permissions) | [Device Management permissions (preview)](#device-management-permissions-(preview)) | [Directory permissions](#directory-permissions) |  [Files permissions](#files-permissions) | [Group permissions](#group-permissions) | [Identity Risk Event permissions (preview)](#identity-risk-event-permissions-(preview)) |  [Mail permissions](#mail-permissions) |  [Notes permissions (preview)](#notes-permissions-(preview)) | [OpenID permissions (preview)](#openid-permissions-(preview)) | [People permissions (preview)](#people-permissions-(preview)) | [Sites permissions (preview)](#sites-permissions-(preview)) | [Tasks permissions (preview)](#tasks-permissions-(preview)) | [User permissions](#user-permissions)

---

<a name="calendars-permissions"></a>
## Calendars permissions

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
**Delegated**

* _Calendars.Read_ : Your App reads the calendars of the signed-in user.
* _Calendars.ReadWrite_ : Your app reads the calendars of the signed-in user and creates events for the signed-in user. 
* _Calendars.ReadWrite.Shared_ : Your app can read and create delete or update events in all calendars that the signed-in user can access. For organizational accounts this access is dependent upon the security groups and directoryRoles that the signed-in user is a member of. For personal Microsoft accounts the access is limited to the signed-in user. 

**Application**

* _Calendars.Read_ : Your app reads the calendars of all users in your organization and publishes schedules for meeting rooms. 
* _Calendars.ReadWrite_ : Your app reads the calendars of all users in your organization and has the ability to create, update, or delete events for all users.
* Scenario 3

For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="contacts-permissions"></a>
## Contacts permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Contacts.Read_ |    Read user contacts  | Allows the app to read user contacts. | No |
| _Contacts.Read.Shared_ |    Read user and shared contacts | Allows the app to read contacts that the user has permissions to access, including the user's own and shared contacts. | No |
| _Contacts.ReadWrite_ |    Have full access to user contacts  | Allows the app to create, read, update, and delete user contacts. | No |
| _Contacts.ReadWrite.Shared_ |    Read and write user and shared contacts | Allows the app to create, read, update and delete contacts that the user has permissions to, including the user's own and shared contacts.| No |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Contacts.Read_ |    Read contacts in all mailboxes | Allows the app to read all contacts in all mailboxes without a signed-in user. | Yes |
| _Contacts.ReadWrite_ |    Read and write contacts in all mailboxes  |Allows the app to create, read, update, and delete all contacts in all mailboxes without a signed-in user.| Yes |

### Remarks


### Example Scenarios
**Delegated**

* _Contacts.Read_ : Your app reads a contact from one of the top-level contact folders of the signed-in user (GET /me/contactfolders/{Id}/contacts/{id}).
* _Contacts.ReadWrite_ : Your app updates the contact photo of one of the signed-in user's contacts (PATCH /me/contactfolders/{contactFolderId}/contacts/{id}/photo/$value). 
* _Contacts.ReadWrite_ : Your app adds contacts to the root folder of the signed-in user (POST /me/contacts).

**Application**

* _Contacts.Read_ : Your app reads contacts from one of the top-level contact folders of any user in the organization (GET /users/{id | userPrincipalName}/contactfolders/{Id}/contacts/{id}). 
* _Contacts.ReadWrite_ : Your app can update the photo for any contact of any user in an organization (PATCH /user/{id | userPrincipalName}/contactfolders/{contactFolderId}/contacts/{id}/photo/$value). 
* _Contacts.ReadWrite_ : Your app can add contacts to the root folder of any user in the organization (POST /users/{id | userPrincipalName}/contacts).

For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="device-permissions"></a>
## Device permissions

**Delegated Permissions**

None.

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Device.ReadWrite.All_ | Read and write devices | Allows the app to read and write all device properties without a signed in user. Does not allow device creation, device deletion or update of device alternative security identifiers. | Yes |

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="device-management-permissions-(preview)"></a>
## Device Management permissions (preview)

**Delegated Permissions**

None.

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _DeviceManagementServiceConfiguration.Read.All_ | Read Microsoft Intune configuration (preview) | Allows the app to read Microsoft Intune service properties including device enrollment and third party service connection configuration. | Yes |
| _DeviceManagementServiceConfiguration.ReadWrite.All_ | Read and write Microsoft Intune configuration (preview) | Allows the app to read and write Microsoft Intune service properties including device enrollment and third party service connection configuration. | Yes |
| _DeviceManagementConfiguration.Read.All_ | Read Microsoft Intune device configuration and policies (preview) | Allows the app to read properties of Microsoft Intune-managed device configuration and device compliance policies and their assignment to groups. | Yes |
| _DeviceManagementConfiguration.ReadWrite.All_ | Read and write Microsoft Intune device configuration and policies (preview) | Allows the app to read and write properties of Microsoft Intune-managed device configuration and device compliance policies and their assignment to groups. | Yes |
| _DeviceManagementApps.Read.All_ | Read Microsoft Intune apps (preview) | Allows the app to read the properties, group assignments and status of apps, app configurations and app protection policies managed by Microsoft Intune. | Yes |
| _DeviceManagementApps.ReadWrite.All_ | Read and write Microsoft Intune apps (preview) | Allows the app to read and write the properties, group assignments and status of apps, app configurations and app protection policies managed by Microsoft Intune. | Yes |
| _DeviceManagementRBAC.Read.All_ | Read Microsoft Intune RBAC settings (preview) | Allows the app to read the properties relating to the Microsoft Intune Role-Based Access Control (RBAC) settings. | Yes |
| _DeviceManagementRBAC.ReadWrite.All_ | Read and write Microsoft Intune RBAC settings (preview) | Allows the app to read and write the properties relating to the Microsoft Intune Role-Based Access Control (RBAC) settings. | Yes |
| _DeviceManagementManagedDevices.Read.All_ | Read Microsoft Intune devices (preview) | Allows the app to read the properties of devices managed by Microsoft Intune. | Yes |
| _DeviceManagementManagedDevices.ReadWrite.All_ | Read and write Microsoft Intune devices (preview) | Allows the app to read and write the properties of devices managed by Microsoft Intune. Does not allow high impact operations such as remote wipe and password reset on the device’s owner. | Yes |
| _DeviceManagementManagedDevices.PrivilegedOperations.All_ | Perform user-impacting remote actions on Microsoft Intune devices (preview) | Allows the app to perform remote high impact actions such as wiping the device or resetting the passcode on devices managed by Microsoft Intune. | Yes |

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="directory-permissions"></a>
## Directory permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Directory.AccessAsUser.All_   |     Access directory as the signed-in user  | Allows the app to have the same access to information in the directory as the signed-in user.| Yes |
| _Directory.Read.All_           |     Read directory data                     | Allows the app to read data in your organization's directory, such as users, groups and apps. | Yes |
| _Directory.ReadWrite.All_      |     Read and write directory data           | Allows the app to read and write data in your organization's directory, such as users, and groups.  Does not allow user or group deletion. It does not allow the app to delete users or groups, or reset user passwords. | Yes |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Directory.Read.All_ | Read directory data | Allows the app to read data in your organization's directory, such as users, groups and apps, without a signed-in user. | Yes |
| _Directory.ReadWrite.All_ | Read and write directory data | Allows the app to read and write data in your organization's directory, such as users, and groups, without a signed-in user. Does not allow user or group deletion. | Yes |

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="files-permissions"></a>
## Files permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Files.Read_ |    Read user files and files shared with user | Allows the app to read the signed-in user's files and files shared with the user.| No |
| _Files.Read.All_ | Read all files that user can access | Allows the app to read all files the signed-in user can access. | No |
| _Files.Read.Selected_ |    Read files that the user selects  | Allows the app to read files that the user selects. The app has access for several hours after the user selects a file. | No |
| _Files.ReadWrite_ |   Have full access to user files and files shared with user | Allows the app to read, create, update and delete the signed-in user's files and files shared with the user. | No |
| _Files.ReadWrite.All_ | Have full access to all files user can access | Allows the app to read, create, update and delete all files the signed-in user can access. | No |
| _Files.ReadWrite.AppFolder_ | Have full access to the application's folder | Allows the app to read, create, update and delete files in the application's folder. | No |
| _Files.ReadWrite.Selected_ |    Read and write files that the user selects | Allows the app to read and write files that the user selects. The app has access for several hours after the user selects a file. | No |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Files.Read.All_ | Read all files that user can access | Allows the app to read all files in all site collections without a signed in user. | Yes |
| _Files.ReadWrite.All_ | Have full access to all files user can access | Allows the app to read, create, update and delete all files in all site collections without a signed in user. | Yes |

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="group-permissions"></a>
## Group permissions

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


### Remarks

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

<a name="identity-risk-event-permissions-(preview)"></a>
## Identity Risk Event permissions (preview)

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _IdentityRiskEvent.Read.All_ |   Read identity risk event information  (preview) | Allows the app to read identity risk event information for all users in your organization on behalf of the signed-in user. | Yes |

**Application Permissions**

None.

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="mail-permissions"></a>
## Mail permissions

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Mail.Read_ |    Read user mail | Allows the app to read email in user mailboxes. | No |
| _Mail.Read.Shared_ |    Read user and shared mail | Allows the app to read mail that the user can access, including the user's own and shared mail. | No |
| _Mail.ReadWrite_ |    Read and write access to user mail | Allows the app to create, read, update, and delete email in user mailboxes. Does not include permission to send mail.| No |
| _Mail.ReadWrite.Shared_ |    Read and write user and shared mail | Allows the app to create, read, update, and delete mail that the user has permission to access, including the user's own and shared mail. Does not include permission to send mail. | No |
| _Mail.Send_ |    Send mail as a user | Allows the app to send mail as users in the organization. | No |
| _Mail.Send.Shared_ |    Send mail on behalf of others | Allows the app to send mail as the signed-in user, including sending on-behalf of others. | No |
| _MailboxSettings.ReadWrite_ |  Read and write user mailbox settings | Allows the app to create, read, update, and delete user's mailbox settings. Does not include permission to send mail.| No |

**Application Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Mail.Read_       |    Read mail in all mailboxes | Allows the app to read mail in all mailboxes without a signed-in user.| Yes |
| _Mail.ReadWrite_ |    Read and write mail in all mailboxes | Allows the app to create, read, update, and delete mail in all mailboxes without a signed-in user. Does not include permission to send mail. | Yes |
| _Mail.Send_ |    Send mail as any user | Allows the app to send mail as any user without a signed-in user. | Yes | 
| _MailboxSettings.ReadWrite_ | Read and write all user mailbox settings  | Allows the app to create, read, update, and delete user's mailbox settings without a signed-in user. Does not include permission to send mail. | Yes |

### Remarks


### Example Scenarios
**Delegation**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="notes-permissions-(preview)"></a>
## Notes permissions (preview)

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Notes.Create_ |    Create pages in users' notebooks (preview) | Allows the app to read the titles of notebooks and sections and create new pages, notebooks and sections on behalf of the signed-in user.| No |
| _Notes.Read_ |    Read user notebooks (preview) | Allows the app to view the titles of OneNote notebooks and sections and to read all pages on behalf of the signed-in user. It cannot view password protected sections. | No |
| _Notes.Read.All_ |    Read all notebooks that the user can access (preview) | Allows the app to read the contents of all notebooks and sections that the signed-in user can access.   It cannot read password protected sections. | No |
| _Notes.ReadWrite_ |    Read and write user notebooks (preview) | Allows the app to read the titles of notebooks and sections, read all pages, write all pages and create new pages on behalf of the signed-in user.  It cannot access password protected sections. | No |
| _Notes.ReadWrite.All_ |    Read and write notebooks that the user can access (preview) | Allows the app to read and write the contents of all notebooks and sections that the signed-in user can access.  It cannot access password protected sections.| No |
| _Notes.ReadWrite.CreatedByApp_ |    Limited notebook access (preview) | Allows the app to read the titles of notebooks and sections, create new pages on behalf of the signed-in user. Also allows the app to read and update pages created by the app. | No |

**Application Permissions**

None.

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="openid-permissions-(preview)"></a>
## OpenID permissions (preview)

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _offline_access_ |    Access user's data anytime (preview) | Allows the app to read and update user data, even when they are not currently using the app.| No |
| _openid_ |    Sign users in (preview) | Allows users to sign in to the app with their work or school accounts and allows the app to see basic user profile information.| No |

**Application Permissions**

None.

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="people-permissions"></a>
## People permissions (preview)

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _People.Read_ |    Read users' relevant people lists (preview) | Allows the app to read a ranked list of relevant people of the signed-in user. The list includes local contacts, contacts from social networking, your organization's directory, and people from recent communications (such as email and Skype).| No |

**Application Permissions**

None.

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="sites-permissions-(preview)"></a>
## Sites permissions (preview)

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Sites.Read.All_ |    Read items in all site collections | Allows the application to read documents and list  items in all site collections on behalf of the signed-in user. | No |
| _Sites.ReadWrite.All_ |    Read and write items in all site collections | Allows the application to edit or delete documents and list items in all site collections on behalf of the signed-in user. | No |

**Application Permissions**

None.

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="tasks-permissions"></a>
## Tasks permissions (preview)

**Delegated Permissions**

|   Permission    |  Azure Portal String   |  Description | Admin Consent Required |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| _Tasks.Read_ | Read user tasks | Allows the app to read user tasks. | No |
| _Tasks.Read.Shared_ | Read user and shared tasks | Allows the app to read tasks a user has permissions to access, including their own and shared tasks. | No |
| _Tasks.ReadWrite_ |    Create, read, update and delete user tasks and plans (preview) | Allows the app to create, read, update and delete tasks and plans (and tasks in them), that are assigned to or shared with the signed-in user.| No |
| _Tasks.ReadWrite.Shared_ | Read and write user and shared tasks | Allows the app to create, read, update, and delete tasks a user has permissions to, including their own and shared tasks. | No |

**Application Permissions**

None.

### Remarks


### Example Scenarios
**Delegated**


**Application**


For more complex scenarios involving multiple permissions, see &lt;Permission Scenarios Topic&gt;.

---

<a name="user-permissions"></a>
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

### Remarks

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
