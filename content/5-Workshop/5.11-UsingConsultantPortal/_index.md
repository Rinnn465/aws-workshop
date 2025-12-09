---
title : "Using the Consultant Portal"
date :  "2025-09-09" 
weight : 11
chapter : false
pre : " <b> 5.11. </b> "
---

## Using the Consultant Portal

The Consultant Portal is a dedicated interface for consultants to manage their appointments and view their schedules.

### Accessing the Consultant Portal

1. Open the Consultant Portal URL from the `outputs.json` file or URL from FrontendStack Outputs in the AWS CloudFormation console.
2. Log in with your consultant email and password
3. First-time users will need to change their temporary password

{{% notice info %}}
Consultant accounts are created by administrators through the Admin Dashboard. You will receive your login credentials via email.
{{% /notice %}}

### My Appointments Page

The **My Appointments** page is your central hub for managing all your scheduled meetings.

#### View Appointments

See all your appointments in a table view with:
- Customer name and contact
- Appointment date and time
- Status (Pending, Confirmed, Completed, Cancelled)




#### Filter Appointments

Use the filter options to narrow down your view:
- **By Status**: Show only pending, confirmed, or completed appointments
- **By Date Range**: View appointments for specific time periods


#### Appointment Actions

For each appointment, you can:


**Confirm Appointments:**
- Change status from Pending to Confirmed
- Customer receives automatic email notification

**Complete Appointments:**
- Mark appointments as Completed after the meeting

**Cancel Appointments:**
- Cancel appointments with a reason
- System sends cancellation email to customer

{{% notice warning %}}
You cannot directly modify appointment times or dates. Contact your administrator if changes are needed.
{{% /notice %}}



![My Appointments](/images/5-Workshop/5.11-UsingConsultantPortal/1.jpg)



### My Schedule Page

The **My Schedule** page displays your weekly availability.

#### Weekly View

- See your time slots organized by day of week
- Color-coded slot status:
  - **Green**: Available
  - **Gray**: Booked/Unavailable
  


#### View-Only Schedule

{{% notice info %}}
Consultants have **read-only** access to their schedules. All schedule modifications must be made by administrators through the Admin Dashboard.
{{% /notice %}}




### Troubleshooting

**Issue: Cannot log in**
- Verify you're using the correct Consultant Portal URL (not Admin Dashboard)
- Reset password if needed

You're now ready to effectively manage your consulting appointments through the Consultant Portal!
