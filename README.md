🏠 Project Overview: Circle Delivery Updates is a no-code automation project built with Zapier. The system matches delivery update emails that arrive in a Microsoft Outlook inbox with the order tracking file in Google Sheets. Each email with the subject “Delivery Update” contains an order number, a delivery status and a status date. The automation extracts this information from the email, finds the related order in the spreadsheet and records the order’s current status.

The main goal of this project is to remove the need to read delivery emails one by one and update order records manually. Automation keeps every status change in a history table and calculates how long an order waited at each stage. The same email is never processed twice, and a late-arriving email with an older date is prevented from overwriting a newer status. Emails related to orders that have no match in the main table are recorded in a separate exceptions table for review. As a result, delivery tracking runs on its own, and every status change can be traced back.

👀 You Can Access The Dataset Using The Link Below. 👀

🔗 Drive Link: https://docs.google.com/spreadsheets/d/1hvQHSK_7b0WpHeNiNXNZDNjSCC1hSvDcJDRPXQk3dJQ

📧 Sample Email Structure ⬇️

Subject: Delivery Update - [Order No]   # Must Contain "Delivery Update"

Order No: [Order No]                    # Order Number In The Main Table.

Status: [Status]                        # New Delivery Status.

Date: [DD.MM.YYYY HH:mm]                # Status Date And Time.

⚠️ Note: The Zap file is shared to show the structure of the workflow. Account-specific information has been removed from the file and replaced with placeholders starting with YOUR. To use the workflow in your own account, you need to copy the Google Sheets template to your own Drive and set up your Outlook and Google Sheets connections.

🔄 Project Workflow: The automation consists of a single Zap that runs every 15 minutes. The steps are designed to run in order, and each step uses the output of the previous one.

The flow starts with a trigger that searches the Microsoft Outlook inbox for new emails with the subject “Delivery Update”. Formatter by Zapier then extracts the Order No, Status and Date fields from the email body using a regular expression (REGEX). The date is also converted into a standard format. Before any record is written to the spreadsheet, the email’s unique Message ID is searched in the Status History sheet. If the email has already been processed, a filter stops the Zap.

In the next step, the order number is searched in the Main Table and the flow splits into two paths. If the order is found, a new row containing the order number, status, status date and Message ID is added to the Status History sheet. The formulas in this row find the date of the order’s next status and calculate the time spent in the current status in hours. For the order’s latest status, “In Progress” is shown instead.

Then, the status date in the processed email is compared with the last update date recorded in the Main Table. To make the comparison accurate, both dates are first converted into Unix timestamps. The status and last update date in the Main Table are updated only if the date in the email is newer than the date in the table. If the order is not found, the current time is captured and the email’s details are recorded in the Exceptions sheet with the reason “Order Not Found”.

🤖 Technologies Used: Zapier, Google Sheets 🤖
