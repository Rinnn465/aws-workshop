---
title : "Using the Admin Dashboard"
date :  "2025-09-09" 
weight : 10
chapter : false
pre : " <b> 5.10. </b> "
---

## Using the Admin Dashboard

The Admin Dashboard provides a comprehensive interface for managing consultants, schedules, and appointments.

### Overview Page

After logging in, the dashboard homepage displays:

**System Statistics:**
- Total number of customers
- Total number of consultants
- Total number of appointments

**Appointments Breakdown:**
- Visual chart showing appointments by status:
  - Pending
  - Confirmed
  - Completed
  - Cancelled

**Recent Appointments:**
- List of the most recent appointments
- Quick view of customer, consultant, date, and status

![Admin Dashboard Homepage](/images/5-Workshop/5.10-UsingAdminDashboard/1.jpg)

### Consultants Management

Navigate to the **Consultants** section to manage your consultant team.

#### View Consultants

- See all consultants in a table view
- Columns: Name, Email, Specialization, Account Status


![Consultants Management](/images/5-Workshop/5.10-UsingAdminDashboard/2.jpg)

#### Add a New Consultant

1. Click the **Add Consultant** button
2. Fill in the consultant details:
   - Full Name
   - Email
   - Phone Number
   - Specialization
   - Qualifications
3. Click **Create**

{{% notice tip %}}
Creating a consultant will automatically create a corresponding Cognito user account with temporary credentials sent to their email.
{{% /notice %}}

![Add Consultant](/images/5-Workshop/5.10-UsingAdminDashboard/3.jpg)
#### Edit Consultant Information

1. Click the **Edit** button next to a consultant
2. Update the desired fields
3. Click **Save Changes**

![Edit Consultant](/images/5-Workshop/5.10-UsingAdminDashboard/4.jpg)

#### Delete a Consultant

1. Click the **Delete** button next to a consultant
2. Confirm the deletion
3. The consultant's Cognito account will also be removed


#### Reset Consultant Password

1. Click the **Reset Password** button
2. A new temporary password will be generated
3. The consultant will receive the password via email



### Appointments Management

Navigate to the **Appointments** section for comprehensive appointment oversight.

#### View Appointments

- Table view of all appointments
- Filter by:
  - Status (Pending, Confirmed, Completed, Cancelled)
  - Date range
  - Consultant
  - Customer

![Schedules Management](/images/5-Workshop/5.10-UsingAdminDashboard/5.jpg)

#### Create Manual Appointment

1. Click **Create Appointment**
2. Select customer (or create new)
3. Select consultant
4. Choose date and time
5. Add notes (optional)
6. Click **Book Appointment**

![Create Appointment](/images/5-Workshop/5.10-UsingAdminDashboard/6.jpg)

#### Update Appointment

1. Click **Edit** on an appointment
2. Modify details (time, consultant, notes)
3. Click **Update**

![Edit Appointment](/images/5-Workshop/5.10-UsingAdminDashboard/7.jpg)



#### Change Appointment Status

Manually update appointment status:
- **Pending** → **Confirmed**: Approve a booking
- **Confirmed** → **Completed**: Mark as finished
- **Any** → **Cancelled**: Cancel the appointment



You now have full control over the MeetAssist system through the Admin Dashboard!
