# Deploying Software via Group Policy on Client1

This guide will walk you through the steps to create a security group named **Software Deployment**, assign the computer named CLIENT1 to this group, and deploy software automatically on CLIENT1 when a user logs into an Active Directory (AD) environment using Group Policy.

# Prerequisites

- **Active Directory Setup**: Ensure that you have an Active Directory environment already set up.
- **Firefox MSI File**: Ensure that the Firefox software you want to deploy is in .msi format. Place the firefox.msi file in a shared folder on the network that all target computers, including CLIENT1, can access.

# Creating a Security Group and Assigning CLIENT1

1. **Create a Security Group for Software Deployment**:
   - Open **Active Directory Users and Computers** on your Domain Controller.
   - Right-click on your domain, select **New** -> **Group**.
   - Name the group "Software Deployment" and ensure that the group scope is set to **Security**.
   - Click **OK** to create the group.
  
2. **Assign CLIENT1 to the Software Deployment Group**:
   - In **Active Directory Users and Computers**, locate the computer object named CLIENT1 in **Computers** under **mydomain.com**.
   - Right-click CLIENT1, select **Add to a group**.
   - In the "Enter the object names to select" field, type "Software Deployment" and click **Check Names**.
   - Once the group name is verified, click **OK** to add CLIENT1 to the group.
  
# Creating a Group Policy Object (GPO) for Software Deployment.

1. **Open Group Policy Management Console (GPMC)**:
   - In the **Group Policy Management Console**, right-click on the domain itself (e.g., mydomain.com) and select **Create a GPO in this domain, and Link it here**.
   - Name the GPO (e.g., "Software Deployment") and click **OK**.
  
2. **Edit the GPO to Deploy Software**:
   - Right-click on the newly created GPO and select **Edit**.
   - Navigate to **Computer Configuration** -> **Policies** -> **Software Settings** -> **Software Installation**.
   - Right-click on **Software Installation**, select **New** -> **Package**.
   - Browse to the shared network location where the firefox.msi file is stored, select it, and choose **Assigned** (software installs automatically when the user logs in).
  
# Configuring Security Filtering

   **Set Security Filtering**:
   - If you want the software and files to be deployed only to specific users or groups, you can set security filtering in the **Scope** tab of the GPO.
   - Remove **Authenticated Users** from the security filtering list.
   - Add the **Software Deployment** group that you created earlier, ensuring that only members of this group, including CLIENT1, will receive the software and files.
# Testing the Software Deployment on CLIENT1
   **Log In to CLIENT1**:
   - Log in to CLIENT1 with a user account that is part of mydomain.com
   - You can also run gpupdate /force on CLIENT1 to apply the Group Policy immediately.
