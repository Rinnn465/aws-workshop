---
title: "Week 13 Worklog"
date: "2025-12-01"
weight: 13
chapter: false
pre: " <b> 1.13 </b> "
---



### Week 13 Objectives:

* Implement Consultant Portal with authentication and schedule/appointment management.
* Integrate Cognito User Pool for consultants.
* Clean up code and refactor project structure.
* Implement customer management and email notification system.
* Improve user experience with multilingual support.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ----------------------------------------- |
| 2   | - Create Consultant Portal UI <br> - Integrate with Cognito Consultant User Pool <br> - Fix authentication and API related bugs | 12/01/2025   | 12/01/2025      |  |
| 3   | - Add Login page with Cognito OAuth2 <br> - Create Schedule page with calendar navigation <br> - Create Appointments page with confirm/deny functionality <br> - Implement responsive UI with Tailwind CSS <br> - Add backend functions: get_my_schedule, get_my_appointments, confirm/deny_appointment <br> - Fix CORS errors, API paths, and account status display | 12/02/2025   | 12/02/2025      |  |
| 4   | - Code cleanup: remove unused SSM parameters <br> - Delete unnecessary API functions <br> - Remove watch-sync scripts <br> - Refactor: rename admin-dashboard → frontend <br> - Organize file structure by roles (admin, consultant) | 12/03/2025   | 12/03/2025      |  |
| 5   | - Translate UI text to Vietnamese for multiple pages <br> - Implement modal confirmation for appointment actions <br> - Enhance error handling in API service <br> - Customize email templates for Consultant User Pool | 12/04/2025   | 12/04/2025      |  |
| 6   | - Implement customer management with CRUD operations <br> - Remove unnecessary fields from customer management form <br> - Add Lambda Email Notification (outside VPC) <br> - Integrate SES for email confirmation/cancellation <br> - Extend API service with email notification methods | 12/05/2025   | 12/05/2025      |  |


### Week 13 Achievements:

* Successfully implemented Consultant Portal:
  * New user interface for consultants
  * Cognito authentication integration with Consultant User Pool
  * Login page with OAuth2 flow
  * Responsive UI with Tailwind CSS

* Functional pages for Consultant Portal:
  * Schedule page: view weekly schedule with calendar navigation
  * Appointments page: view, confirm and deny appointments
  * Personal schedule management

* Backend APIs for Consultant Portal:
  * `get_my_schedule`: consultants view their own schedules
  * `get_my_appointments`: view appointments
  * `confirm_appointment` and `deny_appointment`: handle appointments
  * `get_consultant_by_email`: map Cognito user to consultant_id

* Bug fixes and improvements:
  * Fixed CORS errors (removed allow_credentials)
  * Switched to using idToken instead of accessToken
  * Fixed API paths and SQL queries
  * Improved account status display (Active/Pending)
  * Enhanced error handling

* Code cleanup and refactoring:
  * Removed unused SSM parameters
  * Deleted unused API functions: getTables, getTableSchema, getDatabaseStats
  * Removed watch-sync scripts
  * Cleaned up redundant comments (TODO, BugNote)
  * Renamed admin-dashboard → frontend
  * Organized file structure by roles (admin/consultant)

* Localization (Multilingual support):
  * Translated UI text to Vietnamese
  * ConsultantsPage, OverviewPage, AppointmentsPage, SchedulePage
  * App services and error messages

* Customer management:
  * Full CRUD operations for customer management
  * UI integration with admin dashboard
  * Simplified forms (removed unnecessary fields)

* Email notification system:
  * Lambda Email Notification function (outside VPC)
  * Amazon SES integration
  * Auto-send emails for appointment confirmation/cancellation
  * Backend returns email details to frontend
  * Frontend triggers email notifications

* Email templates customization:
  * Consultant User Pool email templates
  * Account creation by admin messages
  * Account verification emails
  * Appointment confirmation/cancellation emails

* Improved user experience:
  * Modal confirmations for critical actions
  * Better error handling and user feedback
  * Consistent Vietnamese/English UI
  * Streamlined workflows



