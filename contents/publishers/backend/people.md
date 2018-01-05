# People

The management of all user accounts is contained within the People menu. This section will describe each role, how they differ from one another, what system functionality is unlocked according to those credentials, and how to edit and modify user accounts. The following sections presume you are working in the People section of the backend.

<a name="roles"></a>
## Roles

<a name="makers"></a>
### Makers

Makers represent people who author, edit, or otherwise produce the projects and texts on Manifold.

Only Maker accounts can be selected as authors or contributors of projects and texts, though Makers can have different roles on different projects (e.g., an author of one project may be a contributor to another). To add Makers to a specific project, refer to the [Projects](projects.md) page.

Maker accounts are created automatically by the system when a text is ingested, populated by author metadata included within those texts. If your text doesn't have the requisite metadata, Maker accounts can be created manually by Users with Administrative credentials. See the [Linking from a User Account](#linking-user) section for details on that process.

When linked to a User account with Author credentials, the system will know when a project author is highlighting, annotating, or commenting on his or her own work—and they will carry a special designation distinguishing them from other reader interactions. An author's highlights will appear in `{color}`, and annotations and comments will appear with an author badge beside them. See the [Linking Maker and User Accounts](#linking-accounts) section for details on how to link a Maker and User accounts in this way.

<a name="users"></a>
### Users

User accounts are for those who are logging into Manifold to engage with projects. Users are created by those first signing up for an account with a particular instance of Manifold—or by an existing user with Administrator credentials on behalf of one who doesn't yet have an account. User accounts carry different credentials according to the following roles:

<a name="administrator"></a>
#### Administrator

The Administrator role can access and use all of the backend's capabilities as well as annotate texts with resources.

<a name="reader"></a>
#### Reader

The Reader role is the default for all new users to the system. After creating an account, Readers can login and save their viewing preferences, highlights, annotations, and comments across Projects on that particular instance of Manifold.

<a name="author"></a>
#### Author

Accounts with Author credentials maintain the same privileges as a Reader and extend them in the following ways: Authors can annotate texts with resources that have already been loaded into the system and, when associated with a Maker profile, an Author's highlights, annotations, and comments will carry a special designation differentiating them from other user's marks. Authors will also be able to access and interact with Author Dashboard. See the [Makers](#makers), [Linking Maker and User Accounts](#linking-accounts), and [Author Dashboard](author-dashboard.md) sections for more.

<a name="contributor"></a>
#### Contributor

A contributor isn't a proper role in the system but a label. Contributor's are functionally the same as authors and simply describe project authors who aren't listed first on the byline.

<a name="linking-accounts"></a>
## Linking Maker and User Accounts

A link between a Maker and User account can be established from either the User or Maker account drawers. When linking from a Maker account the only option available is to link to an existing account. When linking from the User account, there is an option to create a Maker that is not already in the system. Both methods are described here.

<a name="linking-maker"></a>
### Linking from a Maker Account

To link a Maker account with a User one, click on `Makers` in the left sidebar, which will bring up a list of all Makers presently in the system. Search or navigate through the list until you find the Maker account you want to associate, and then click on the name. When you do, a drawer will open up from the right side of the screen with account details for the user in question. At the bottom of this drawer there will be a heading titled `Users`, with a button prompting you to `Add an associated user`. Click the add button and then choose an existing User account to associate with the present Maker account. The system will confirm the link has been established.

<a name="linking-user"></a>
### Linking from a User Account

To link a User account with a Maker one, click on `Users` in the left sidebar, which will bring up a list of all Users presently in the system. Search or navigate through the list until you find the User account you want to associate, and then click on the name. When you do, a drawer will open up from the right side of the screen with account details for the user in question. At the bottom of this drawer there will be a heading titled `Makers`, with a button prompting you to `Add or create a maker`. Click the add button and then choose an existing Maker account to associate with the present Maker account. If there is no account already present in the system that you want to link, you will can manually key in a name, and the account will be created (and can be modified in the Maker section). The system will confirm the link has been established.

<a name="account-details"></a>
## Managing and Deleting Accounts

Account details for both Makers and Users are accessed from their respective account drawers, which open when an account name is clicked in either the User or Maker section.

<a name="maker-account"></a>
### Maker Accounts

This section describes how to modify Maker accounts and assumes you are in the Maker account drawer. The `Users` heading at the bottom of the drawer is for linking a Maker account to a User one. See the [Linking Maker and User Accounts](#linking-accounts) section for details on that process.

#### Deleting a Maker

To delete a Maker account, click the `Delete Maker` button beside the red trashcan icon under the Maker's name.  You will receive a warning asking you to confirm you want to delete this particular Maker. Deleting a Maker permanently removes them from the system. Projects to which they are associated will otherwise be unaffected.

#### Adjusting a Makers Name

Under the `First Name` and `Last Name` headers in the drawer you can directly modify a Maker's First and Last names. Click `Save Maker` near the bottom of the drawer to push your changes into the system.

*Note*. Middle names or initials and suffixes aren't yet supported.

#### Maker Avatars

You can add a Maker avatar in either JPEG, TIFF, GIF, or PNG format to the system under the `Avatar Image` heading. Images should be in a 1:1 ratio and no less than 40 pixels wide. Maker avatars display beneath the title on the project landing page.

<a name="user-account"></a>
### User Accounts

This section describes how to modify User accounts and assumes you are in the User account drawer. The `Makers` heading at the bottom of the drawer is for linking a User account to a Maker one. See the [Linking Maker and User Accounts](#linking-accounts) section for details on that process.

#### Changing a User's Password

To change a User's password, click `Reset Password` below the user's name. A prompt will come up asking if you want to Generate a New Password or Set a New Password. If you click `Generate New Password` the system will automatically create a new password and email it to the address on file. If you click `Generate New Password` you can manually input a new password and save it to the system.

#### Deleting a User

To delete a User account, click the `Delete User` button beside the red trashcan icon under the User's name.  You will receive a warning asking you to confirm you want to delete this particular Maker. Deleting a User permanently removes them from the system along with any highlights, annotations, or comments they have made.

#### Adjusting a User's Email

Under the `EMAIL` heading in the drawer you can directly modify a User's email address. Click `Save Maker` near the bottom of the drawer to push your changes into the system.

#### Adjusting a User's Name

Under the `First Name` and `Last Name` headers in the drawer you can directly modify a Users's First and Last names. Click `Save Maker` near the bottom of the drawer to push your changes into the system.

*Note*. Middle names or initials and suffixes aren't yet supported.

#### User Avatars

You can add a User avatar in either JPEG, TIFF, GIF, or PNG format to the system under the `Avatar Image` heading. Images should be in a 1:1 ratio and no less than 40 pixels wide. Maker avatars display beside annotations and comments.
