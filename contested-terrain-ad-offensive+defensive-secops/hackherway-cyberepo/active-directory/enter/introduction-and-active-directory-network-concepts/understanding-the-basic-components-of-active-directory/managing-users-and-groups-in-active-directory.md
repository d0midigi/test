# Managing Users and Groups in Active Directory

One of the primary functions of Active Directory (AD) is to manage user accounts and groups. This management includes creating, modifying, and removing accounts, as well as organizing users into groups for easier administration.

### Creating User Accounts

Creating a user account in AD is a straightforward process:

1. **Navigate to the Correct OU:** In Active Directory Users and Computers (ADUC), locate the OU where you want to create the new user account.
2. **New User Wizard:** Right-click on the OU and select ‘New’ > ‘User’. This opens the New User Wizard, where you’ll enter the user’s details, such as their name and user logon name.
3. **Set Initial Password:** Towards the end of the wizard, you’ll set an initial password for the account and can choose whether the user must change the password at the next logon.

### Managing Groups

Groups in AD are used to collect user accounts, computer accounts, and other groups into manageable units. Working with groups is similar to working with individual user accounts:

1. **Create a New Group:** Right-click on the OU where you want the group and select ‘New’ > ‘Group’. Name the group and define its scope and type.
2. **Add Members to the Group:** Once the group is created, you can add members by opening the group’s properties and navigating to the ‘Members’ tab.

#### Practical Example

Imagine a scenario where a new marketing team is formed in your company. You would first create individual user accounts for each team member. Then, you would create a group called “Marketing Team” and add all the marketing team’s user accounts to this group. This setup simplifies processes like assigning permissions or sending emails to the entire team, as you can now apply actions to the group instead of each user individually.

### Importance of Regular Maintenance

Regularly updating user information, resetting passwords, and cleaning up inactive accounts are critical for maintaining the security and efficiency of your AD environment. For instance, when an employee leaves the company, their user account should be disabled or removed to prevent unauthorized access.

Next, we will learn how to implement Organizational Units (OUs) in Active Directory.

<br>

<br>

<br>

<br>
