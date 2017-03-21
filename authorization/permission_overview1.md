# Microsoft Graph permission scopes

Microsoft Graph uses OAuth 2.0 and exposes permissions to control the access that applications have to resources. As a developer, you decide which permissions your app requests (like reading messages or reading and writing files). When a user or administrator signs in to your app they are given an opportunity to consent to the permissions you've requested, which results in your application being granted access to resources. For apps that don't take a signed-in user, like service apps and daemons, permissions are usually pre-consented to by an administrator when the app is installed. 

The permissions you select for your app, the way that you configure these permissions, the way that your app requests them, and the consent experience for your users will depend on a number of factors:

* Whether you are using the Azure AD endpoint or the Azure AD v2.0 endpoint for authentication.
* Whether users sign in to your app or whether your app runs without a user present.
* Whether users of your app have personal Microsoft accounts or organizational accounts. 
* Whether your app is a consumer app, a Line of Business app published by your organization for its own use (single-tenant), or a commercial app for use by multiple organizations (multi-tenant).

## Permission name conventions
Permission names follow a simple pattern: _resource.operation.constraint_. Examples of _resource_ are Group, User, or Drive. Examples of _operation_ are Read or ReadWrite. The _constraint_ element of the name determines the potential extent of access the app will have within the directory. Currently Microsoft Graph supports three different constraints: 

* **All** grants permission for the app to perform the operations on all of the resources of the specified type in a directory. For example, User.Read.All potentially grants the app privileges to read the profiles of all of the users in a directory. 
* **Shared** grants permission for the app to perform the operations on a shared subset of the specified resource in the directory. This constraint is largely used with Outlook resources to grant an app acting on behalf of a signed-in user access to a set of shared elements. For example, Mail.Read.Shared, grants privileges to to read mail that the user can access, including the user's own and shared mail.
* **No constraint specified** limits the app to performing the operation on the resources owned by the signed-in user. For example, User.Read grants privileges to read the profile of only the signed-in user.

**Note**: In delegated scenarios, the effective permissions granted to your app will be further constrained by the directory permissions of the signed-in user. 

## Delegated vs. Application permissions 
Microsoft Graph has two types of permissions: **Delegated permissions** and **Application permissions**. 

**Delegated permissions** are used by apps that have a signed-in user present. For these apps either the user or an administrator consents to the permissions that the app requests and the app is delegated permission to act on behalf of the signed-in user when making calls to Microsoft Graph. The *effective permissions* of the app are the least privileged intersection of the delegated permissions the app has been granted (via consent) and the permissions of the signed-in user. The app can never have more permissions than the signed-in user. For example, if an app has been granted delegated permissions to read and update all user profiles (_User.ReadWrite.All_) but the signed-in user only has permissions to update their own user profile, the app can only update the signed-in user's profile. Some delegated permissions can be consented to by non-administrative users, but some higher privileged delegated permissions require administrator consent.  

**Application permissions** are used by apps that run without a signed-in user present; for example, apps that run as background services or daemons. Applications permissions grant the full level of privileges implied by the permission. Thus the *effective permissions* of the app are are the full level of privileges implied by the permission and the app has the same privileges that an administrator would with the same permission. For example, an app that has the _User.ReadWrite.All_ Application permission can write the profile of every user in a directory. Application permissions can only be consented by an administrator. 

## Personal Microsoft Accounts vs Organizational Accounts



>**Note:** Some Microsoft Graph permissions, such as those pertaining to groups and tasks, are not applicable to personal accounts.  





## Permission scope details

Permission names follow a simple pattern: _resource.operation.constraint_. Examples of _resource_ are Group, User, or Drive. Examples of _operation_ are Read or ReadWrite. Examples of constraint for example, Group.ReadWrite.All. If the constraint is "All", the scope grants the app the ability to perform the operation (ReadWrite) on all of the specified resources (Group) in the directory; otherwise, the scope only permits the operation on the profile of the signed-in user. Scopes may grant limited privileges for the specified operation. See the **Description** column for details.
You must configure your app to have the necessary permissions to access Microsoft Graph  resources. The permissions are scoped to individual resources for the rights to read, write, or  both. 

The following tables list the Microsoft Graph permission scopes and explains the access granted by each. 

- The **Scope** column lists the scope name. Scope names take the form resource.operation.constraint; for example, Group.ReadWrite.All. If the constraint is "All", the scope grants the app the ability to perform the operation (ReadWrite) on all of the specified resources (Group) in the directory; otherwise, the scope only permits the operation on the profile of the signed-in user. Scopes may grant limited privileges for the specified operation. See the **Description** column for details.
- The **Permission** column shows how the scope is displayed on the Azure portal. 
- The **Description** column describes the full set of privileges granted by the scope. For delegated scopes, the actual access granted to the app will be the least privileged combination (intersection) of the access granted by the scope and the privileges of the signed-in user. 
- The scopes are grouped according to whether the permissions require an administrator's consent.

  > **Note**: See [Known issues](../overview/release_notes.md) for `v1.0` and `beta` permission scope limitations.
  
###Permissions requiring administrator's consent

|   **Scope**                  |  **Permission**                          |  **Description** |
|:-----------------------------|:-----------------------------------------|:-----------------|
| _Directory.AccessAsUser.All_   |     Access directory as the signed-in user  | Allows the app to have the same access to information in the directory as the signed-in user.|
| _Directory.Read.All_           |     Read directory data                     | Allows the app to read data in your organization's directory, such as users, groups and apps. |
| _Directory.ReadWrite.All_      |     Read and write directory data           | Allows the app to read and write data in your organization's directory, such as users, and groups.  Does not allow user or group deletion. It does not allow the app to delete users or groups, or reset user passwords. |
| _Group.Read.All_ |    Read all groups | Allows the app to list groups, and to read their properties and all group memberships on behalf of the signed-in user.  Also allows the app to read calendar, conversations, files, and other group content for all groups the signed-in user can access. |
| _Group.ReadWrite.All_ |    Read and write all groups| Allows the app to create groups and read all group properties and memberships on behalf of the signed-in user.  Additionally allows group owners to manage their groups and allows group members to update group content. |
| _User.Read.All_                |     Read all user's full profiles           | Same as User.ReadBasic.All, except that it allows the app to read the full profile of all users in the organization and when reading navigation properties like manager and direct reports. The full profile includes all of the declared properties of the **User** entity. To read the groups that a user is a member of, the app will also require either Group.Read.All or Group.ReadWrite.All. |
| _User.ReadWrite.All_           |     Read and write all user's full profiles | Allows the app to read and write the full set of profile properties, reports, and managers of other users in your organization, on behalf of the signed-in user. |


###Permissions not requiring administrator's consent

|   **Scope**    |  **Permission**   |  **Description** |
|:-----------------------------|:-----------------------------------------|:-----------------|
| _Calendars.Read_ |    Read user calendars  | Allows the app to read events in user calendars.|
| _Calendars.Read.Shared_ |    Read user and shared calendars | Allows the app to read events in all calendars that the user can access, including delegate and shared calendars. |
| _Calendars.ReadWrite_ |    Have full access to user calendars  | Allows the app to create, read, update, and delete events in user calendars. |
| _Calendars.ReadWrite.Shared_ |    Read and write user and shared calendars | Allows the app to create, read, update and delete events in all calendars the user has permissions to access. This includes delegate and shared calendars.|
| _Contacts.Read_ |    Read user contacts  | Allows the app to read user contacts. |
| _Contacts.Read.Shared_ |    Read user and shared contacts | Allows the app to read contacts that the user has permissions to access, including the user's own and shared contacts. |
| _Contacts.ReadWrite_ |    Have full access to user contacts  | Allows the app to create, read, update, and delete user contacts. |
| _Contacts.ReadWrite.Shared_ |    Read and write user and shared contacts | Allows the app to create, read, update and delete contacts that the user has permissions to, including the user's own and shared contacts.|
| _Files.Read_ |    Read user files and files shared with user | Allows the app to read the signed-in user's files and files shared with the user.| 
| _Files.Read.All_ | Read all files that user can access | Allows the app to read all files the signed-in user can access. |
| _Files.Read.Selected_ |    Read files that the user selects  | Allows the app to read files that the user selects. The app has access for several hours after the user selects a file. |
| _Files.ReadWrite_ |   Have full access to user files and files shared with user | Allows the app to read, create, update and delete the signed-in user's files and files shared with the user. |
| _Files.ReadWrite.All_ | Have full access to all files user can access | Allows the app to read, create, update and delete all files the signed-in user can access. |
| _Files.ReadWrite.AppFolder_ | Have full access to the application's folder | Allows the app to read, create, update and delete files in the application's folder. |
| _Files.ReadWrite.Selected_ |    Read and write files that the user selects | Allows the app to read and write files that the user selects. The app has access for several hours after the user selects a file. |
| _Mail.Read_ |    Read user mail | Allows the app to read email in user mailboxes. |
| _Mail.Read.Shared_ |    Read user and shared mail | Allows the app to read mail that the user can access, including the user's own and shared mail. |
| _Mail.ReadWrite_ |    Read and write access to user mail | Allows the app to create, read, update, and delete email in user mailboxes. Does not include permission to send mail.|
| _Mail.ReadWrite.Shared_ |    Read and write user and shared mail | Allows the app to create, read, update, and delete mail that the user has permission to access, including the user's own and shared mail. Does not include permission to send mail. |
| _Mail.Send_ |    Send mail as a user | Allows the app to send mail as users in the organization. |
| _Mail.Send.Shared_ |    Send mail on behalf of others | Allows the app to send mail as the signed-in user, including sending on-behalf of others. |
| _MailboxSettings.ReadWrite_ |  Read and write user mailbox settings | Allows the app to create, read, update, and delete user's mailbox settings. Does not include permission to send mail.|
| _offline_access_ |    Access user's data anytime (preview) | Allows the app to read and update user data, even when they are not currently using the app.|
| _openid_ |    Sign users in (preview) | Allows users to sign in to the app with their work or school accounts and allows the app to see basic user profile information.|
| _User.Read_       |    Sign-in and read user profile | Allows users to sign-in to the app, and allows the app to read the profile of signed-in users. The full profile includes all of the declared properties of the User entity. The app cannot read navigation properties, such as manager or direct reports. Also allows the app to read the following basic company information of the signed-in user (through the **TenantDetail** object): tenant ID, tenant display name, and verified domains.|
| _User.ReadWrite_ |    Read and write access to user profile | Allows the app to read your profile. It also allows the app to update your profile information on your behalf. |
| _User.ReadBasic.All_ |    Read all user's basic profiles | Allows the app to read the basic profile of all users in the organization on behalf of the signed-in user. The following properties comprise a user’s basic profile: display name, first and last name, photo, and email address. To read the groups that a user is a member of, the app will also require Group.Read.All or Group.ReadWrite.All.| 

###App-only permissions requiring administrator's consent

|   **Scope**    |  **Permission**   |  **Description** |
|:---------------|:------------------|:-----------------|
| _Calendars.Read_ |    Read calendars in all mailboxes | Allows the app to read events of all calendars without a signed-in user. |
| _Calendars.ReadWrite_ |    Read and write calendars in all mailboxes | Allows the app to create, read, update, and delete events of all calendars without a signed-in user.|
| _Contacts.Read_ |    Read contacts in all mailboxes | Allows the app to read all contacts in all mailboxes without a signed-in user. |
| _Contacts.ReadWrite_ |    Read and write contacts in all mailboxes  |Allows the app to create, read, update, and delete all contacts in all mailboxes without a signed-in user.|
| _Device.ReadWrite.All_ | Read and write devices | Allows the app to read and write all device properties without a signed in user. Does not allow device creation, device deletion or update of device alternative security identifiers. |
| _Directory.Read.All_ | Read directory data | Allows the app to read data in your organization's directory, such as users, groups and apps, without a signed-in user. |
| _Directory.ReadWrite.All_ | Read and write directory data | Allows the app to read and write data in your organization's directory, such as users, and groups, without a signed-in user. Does not allow user or group deletion. |
| _Files.Read.All_ | Read all files that user can access | Allows the app to read all files in all site collections without a signed in user. |
| _Files.ReadWrite.All_ | Have full access to all files user can access | Allows the app to read, create, update and delete all files in all site collections without a signed in user. |
| _Group.Read.All_ | Read all groups | Allows the app to read memberships for all groups without a signed-in user. Note that not all group API supports access using app-only permissions. See [known issues](../overview/release_notes.md#groups) for examples. |
| _Group.ReadWrite.All_ | Read and write all groups | Allows the app to create groups, read and update group memberships, and delete groups. All of these operations can be performed by the app without a signed-in user. Note that not all group API supports access using app-only permissions. See [known issues](../overview/release_notes.md#groups) for examples.|
| _Mail.Read_       |    Read mail in all mailboxes | Allows the app to read mail in all mailboxes without a signed-in user.|
| _Mail.ReadWrite_ |    Read and write mail in all mailboxes | Allows the app to create, read, update, and delete mail in all mailboxes without a signed-in user. Does not include permission to send mail. |
| _Mail.Send_ |    Send mail as any user | Allows the app to send mail as any user without a signed-in user. | 
| _MailboxSettings.ReadWrite_ | Read and write all user mailbox settings  | Allows the app to create, read, update, and delete user's mailbox settings without a signed-in user. Does not include permission to send mail. |
| _Member.Read.Hidden_ | Read all hidden memberships | Allows the app to read the memberships of hidden groups and administrative units without a signed-in user. |
| _Reports.Read.All_ | Read all usage reports | Allows an app to read all service usage reports without a signed-in user. Services that provide usage reports include Office 365 and Azure Active Directory. |
| _User.Read.All_ |    Read all users' full profiles | Allows the app to read the full set of profile properties, group membership, reports and managers of other users in your organization, without a signed-in user.| 
| _User.ReadWrite.All_ |   Read and write all users' full profiles | Allows the app to read and write the full set of profile properties, group membership, reports and managers of other users in your organization, without a signed-in user.|


##Permission scopes in preview

###Permissions requiring administrator's consent (preview)

|   **Scope**    |  **Permission**   |  **Description** |
|:---------------|:------------------|:-----------------|
| _IdentityRiskEvent.Read.All_ |   Read identity risk event information  (preview) | Allows the app to read identity risk event information for all users in your organization on behalf of the signed-in user. |
| _DeviceManagementServiceConfiguration.Read.All_ | Read Microsoft Intune configuration (preview) | Allows the app to read Microsoft Intune service properties including device enrollment and third party service connection configuration. |
| _DeviceManagementServiceConfiguration.ReadWrite.All_ | Read and write Microsoft Intune configuration (preview) | Allows the app to read and write Microsoft Intune service properties including device enrollment and third party service connection configuration. |
| _DeviceManagementConfiguration.Read.All_ | Read Microsoft Intune device configuration and policies (preview) | Allows the app to read properties of Microsoft Intune-managed device configuration and device compliance policies and their assignment to groups. |
| _DeviceManagementConfiguration.ReadWrite.All_ | Read and write Microsoft Intune device configuration and policies (preview) | Allows the app to read and write properties of Microsoft Intune-managed device configuration and device compliance policies and their assignment to groups. |
| _DeviceManagementApps.Read.All_ | Read Microsoft Intune apps (preview) | Allows the app to read the properties, group assignments and status of apps, app configurations and app protection policies managed by Microsoft Intune. |
| _DeviceManagementApps.ReadWrite.All_ | Read and write Microsoft Intune apps (preview) | Allows the app to read and write the properties, group assignments and status of apps, app configurations and app protection policies managed by Microsoft Intune. |
| _DeviceManagementRBAC.Read.All_ | Read Microsoft Intune RBAC settings (preview) | Allows the app to read the properties relating to the Microsoft Intune Role-Based Access Control (RBAC) settings. |
| _DeviceManagementRBAC.ReadWrite.All_ | Read and write Microsoft Intune RBAC settings (preview) | Allows the app to read and write the properties relating to the Microsoft Intune Role-Based Access Control (RBAC) settings. |
| _DeviceManagementManagedDevices.Read.All_ | Read Microsoft Intune devices (preview) | Allows the app to read the properties of devices managed by Microsoft Intune. |
| _DeviceManagementManagedDevices.ReadWrite.All_ | Read and write Microsoft Intune devices (preview) | Allows the app to read and write the properties of devices managed by Microsoft Intune. Does not allow high impact operations such as remote wipe and password reset on the device’s owner. |
| _DeviceManagementManagedDevices.PrivilegedOperations.All_ | Perform user-impacting remote actions on Microsoft Intune devices (preview) | Allows the app to perform remote high impact actions such as wiping the device or resetting the passcode on devices managed by Microsoft Intune. |

###Permissions not requiring administrator's consent (preview)

|   **Scope**    |  **Permission**   |  **Description** |
|:---------------|:------------------|:-----------------|
| _Notes.Create_ |    Create pages in users' notebooks (preview) | Allows the app to read the titles of notebooks and sections and create new pages, notebooks and sections on behalf of the signed-in user.|
| _Notes.Read_ |    Read user notebooks (preview) | Allows the app to view the titles of OneNote notebooks and sections and to read all pages on behalf of the signed-in user. It cannot view password protected sections. |
| _Notes.Read.All_ |    Read all notebooks that the user can access (preview) | Allows the app to read the contents of all notebooks and sections that the signed-in user can access.   It cannot read password protected sections. |
| _Notes.ReadWrite_ |    Read and write user notebooks (preview) | Allows the app to read the titles of notebooks and sections, read all pages, write all pages and create new pages on behalf of the signed-in user.  It cannot access password protected sections. |
| _Notes.ReadWrite.All_ |    Read and write notebooks that the user can access (preview) | Allows the app to read and write the contents of all notebooks and sections that the signed-in user can access.  It cannot access password protected sections.|
| _Notes.ReadWrite.CreatedByApp_ |    Limited notebook access (preview) | Allows the app to read the titles of notebooks and sections, create new pages on behalf of the signed-in user. Also allows the app to read and update pages created by the app. |
| _People.Read_ |    Read users' relevant people lists (preview) | Allows the app to read a ranked list of relevant people of the signed-in user. The list includes local contacts, contacts from social networking, your organization's directory, and people from recent communications (such as email and Skype).|
| _Sites.Read.All_ |    Read items in all site collections | Allows the application to read documents and list  items in all site collections on behalf of the signed-in user. |
| _Sites.ReadWrite.All_ |    Read and write items in all site collections | Allows the application to edit or delete documents and list items in all site collections on behalf of the signed-in user. |
| _Tasks.Read_ | Read user tasks | Allows the app to read user tasks. |
| _Tasks.Read.Shared_ | Read user and shared tasks | Allows the app to read tasks a user has permissions to access, including their own and shared tasks. |
| _Tasks.ReadWrite_ |    Create, read, update and delete user tasks and plans (preview) | Allows the app to create, read, update and delete tasks and plans (and tasks in them), that are assigned to or shared with the signed-in user.|
| _Tasks.ReadWrite.Shared_ | Read and write user and shared tasks | Allows the app to create, read, update, and delete tasks a user has permissions to, including their own and shared tasks. |



##Permission scope scenarios
The following are some app scenarios using the `User` and `Group` resources and their corresponding required scopes. The following table shows the permission scopes needed for an app to be able to perform specific operations. Note that in some cases the ability of the app to perform some operations will depend on whether the permission scope is app-only or delegated, and, in the case of delegated permission scopes, on the privileges of the signed-in user. 

###Access scenarios using the User resource and the required scopes

| **App tasks involving User**	 |  **Required scopes** | **Permissions** |
|:-------------------------------|:---------------------|:---------------|
| App wants to read other users' basic information (only display name and picture), for example to show in a people picking experience	 | _User.ReadBasic.All_  |  Read all user's basic profiles |
| App wants to read complete user profile for signed in user (see direct reports, and manager, etc)	 | _User.Read_ | Enable sign-in and read user profile|
| App wants to read complete user profile all users	 | _User.Read.All_ |  Read all user's full profiles   |
| App wants to read files, mail and calendar information for the signed in user	 | _User.Read_, _Files.Read_, _Mail.Read_, _Calendars.Read_ | Enable sign-in and read user profile, Read users' files,  Read user mail,  Read user calendars |
| App wants to read the signed-in user's (my) files and files that other users have shared with the signed-in user (me). | _User.Read_, _Files.Read_, _Sites.Read.All_ | Enable sign-in and read user profile, Read users' files,  Read items in all site collections |
| App wants to read and write complete user profile for signed in user	 | _User.ReadWrite_ | Read and write access to user profile |
| App wants to read and write complete user profile all users	 | _User.ReadWrite.All_ | Read and write all user's full profiles |
| App wants to read and write files, mail and calendar information for the signed in user	 | _User.ReadWrite_, _Files.ReadWrite_, _Mail.ReadWrite_, _Calendars.ReadWrite_  |  Read and write access to user profile,  Read and write access to user profile,  Read and write access to user mail, Have full access to user calendars |
   

###Access scenarios using the Group resource and the required scopes
    
| **App tasks involving Group**	 |  **Required scopes** |  **Permissions** |
|:-------------------------------|:---------------------|:---------------|
| App wants to read basic group info (only display name and picture), for example to show in a group picking experience	 | _Group.Read.All_  | Read all groups|
| App wants to read all content in all Office 365 groups, including files, conversations.  It also needs to show group memberships, be able to update group memberships, (if owner).  |  _Group.Read.All_ | Read items in all site collections, Read all groups|
| App wants to read and write all content in all Office 365 groups, including files, conversations.  It also needs to show group memberships, be able to update group memberships, (if owner).  | 	_Group.ReadWrite.All_, _Sites.ReadWrite.All_ |  Read and write all groups, Edit or delete items in all site collections |
| App wants to discover (find) an Office 365 group. It allows the user to search for a particular group and choose one from the enumerated list to allow the user to join the group.	 | _Group.ReadWrite.All_ | Read and write all groups|
| App wants to create a group through AAD Graph | 	_Group.ReadWrite.All_ | Read and write all groups|
 


