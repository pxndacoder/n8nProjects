CIBC Budget Tracker (n8n Workflow)
Overview

This project is an automated budget tracker built using n8n. It monitors your Gmail account for CIBC card notifications with potential to monitor for other banks e.g scotia and ncb.However,CIBC's interface is easier to integrate. It then extracts transaction data, and logs it into a Google Sheet with a dynamic dashboard. The Google Sheet automatically tracks income, spending, and current balances in both BBD and JMD currencies.

The workflow includes:

Parsing incoming emails for approved card transactions, money received, and attempted sends.

Detecting the bank/card type (e.g CIBC / NCB).

Extracting amounts, merchants/senders, and transaction dates.

Updating spending and income sheets in Google Sheets.

Features

Gmail Trigger: Monitors your email account in real-time for new notifications.

Transaction Parsing: Extracts key details including amount, currency, sender/merchant, and date.

Dynamic Categorization: Identifies transaction type:

Money Received

Card Purchase

Money Sent

Attempted Send

Currency Conversion: Converts BBD to JMD automatically.

Google Sheets Integration: Appends transactions to:

Spending sheet

Income sheet

Dashboard: Tracks totals for each bank/card in both BBD and JMD.

Workflow Details

Gmail Trigger Node

Monitors Gmail every minute for incoming messages.

Filters messages to detect CIBC or NCB notifications.

Get a Message Node

Retrieves the full email body.

Ensures that email snippets do not cut off important transaction details.

Code Node (JavaScript)

Parses email content to extract:

Transaction type

Amount (BDS & JMD)

Merchant/Sender

Bank/Card

Date

Handles both CIBC and NCB formats.

IF Node

Checks if the transaction is "Money Received" (to update the Income sheet).

Routes other transaction types to Spending sheet.

Google Sheets Append Nodes

Appends extracted transaction data to the correct sheet:

Income

Spending

Updates dashboard totals automatically.

Google Sheets Structure

Income Sheet Columns:

Date

Bank/Card

Amount (BDS)

Amount (JMD)

Description

Source

Spending Sheet Columns:

Date

Bank/Card

Amount (BDS)

Amount (JMD)

Merchant

Description

Dashboard Sheet Columns:

Account

Starting Balance (BDS / JMD)

Total Income (BDS / JMD)

Total Spending (BDS / JMD)

Current Balance (BDS / JMD)

Setup Instructions

Clone the Workflow

Import the provided n8n JSON workflow into your n8n instance.

Gmail OAuth2 Credentials

Create a Gmail OAuth2 credential in n8n.

Assign it to the Gmail Trigger and Get a Message nodes.

Google Sheets OAuth2 Credentials

Create a Google Sheets OAuth2 credential in n8n.

Assign it to the Append Row in Sheet nodes.

Update Sheet URLs

Replace Google Sheet IDs in the workflow nodes with your own sheet URLs.

Ensure the sheet structure matches the columns mentioned above.

Activate Workflow

Turn on the workflow.

Incoming CIBC and NCB emails will now automatically populate your sheets.

Notes

NCB Email Parsing: Uses full email body for accurate extraction (snippet often cuts off important fields).

Currency Conversion: 1 BBD = 75 JMD (can be updated in the code node).

Dashboard Updates: Formulas in Google Sheets can automatically calculate totals for each card/account.

Future Enhancements

Support for additional banks (e.g., Scotia, RBC).

Categorize spending by type (e.g., food, transport, utilities).

Generate automated monthly reports and charts.

Handle declined transactions separately.
