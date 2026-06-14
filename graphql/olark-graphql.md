# Olark GraphQL Schema

## Overview

This document describes a conceptual GraphQL schema for the Olark live chat and customer support platform. The schema is derived from the [Olark REST API](https://www.olark.com/api/rest/) and the broader Olark platform feature set, covering real-time chat sessions, visitor intelligence, transcript management, operator teams, automations, campaigns, and reporting.

## Schema Source

- REST API reference: https://www.olark.com/api/rest/
- JavaScript API reference: https://www.olark.com/api
- Platform documentation: https://www.olark.com/help
- Schema file: [olark-schema.graphql](olark-schema.graphql)

## Named Types (62 total)

### Chat

| Type | Description |
|------|-------------|
| `Chat` | A live chat session between a visitor and one or more operators |
| `ChatDetails` | Extended metadata for a chat session including page URL, referrer, and campaign |
| `ChatStatus` | Enum: PENDING, ACTIVE, CLOSED, MISSED, TRANSFERRED |
| `ChatType` | Enum: INBOUND, OUTBOUND, AUTOMATED, OFFLINE |

### Visitor

| Type | Description |
|------|-------------|
| `Visitor` | A website visitor who may engage in a chat session |
| `VisitorDetails` | Identity information including name, email, phone, and location |
| `VisitorBrowser` | Browser and device characteristics (user agent, screen size, OS) |
| `VisitorGeo` | Geographic location derived from visitor IP address |
| `VisitorOrg` | Organization or company data associated with the visitor |

### Transcript

| Type | Description |
|------|-------------|
| `Transcript` | The full record of a chat session |
| `TranscriptDetails` | Aggregate statistics: message counts, response times, rating |
| `TranscriptItem` | Union of TranscriptMessage and TranscriptEvent |
| `TranscriptMessage` | A message (operator or visitor) in the transcript |
| `TranscriptEvent` | A system event (join, leave, transfer) in the transcript |
| `OperatorMessage` | A message authored by an operator |
| `VisitorMessage` | A message authored by a visitor |

### Automation

| Type | Description |
|------|-------------|
| `Automation` | An automated rule set that triggers on visitor behavior |
| `AutomationRule` | A single rule with conditions and actions |
| `AutomationCondition` | A logical condition evaluated against visitor or session data |
| `AutomationAction` | An action performed when conditions are satisfied |
| `AutomationEvent` | The event kind that can fire an automation |

### Operator

| Type | Description |
|------|-------------|
| `Operator` | A customer support agent |
| `OperatorDetails` | Profile: email, display name, avatar, role, timezone |
| `OperatorStatus` | Real-time availability and concurrent chat count |
| `OperatorAvailability` | Scheduled hours and auto-away configuration |

### Group

| Type | Description |
|------|-------------|
| `Group` | A team or department of operators |
| `GroupDetails` | Name, description, routing settings, and language |
| `GroupMember` | An operator's membership record within a group |

### Campaign

| Type | Description |
|------|-------------|
| `Campaign` | A targeted proactive outreach campaign for visitors |
| `CampaignDetails` | Metadata including impressions, conversions, and target URL |
| `CampaignTrigger` | The criteria that fires the campaign (delay, page view count, URL) |
| `CampaignMessage` | A message delivered as part of a campaign |

### Greeting / Form

| Type | Description |
|------|-------------|
| `Greeting` | A greeting shown to visitors before or during chat |
| `Form` | A pre-chat or post-chat survey form |
| `FormField` | A single field within a form (text, select, checkbox, etc.) |

### Offline Messaging

| Type | Description |
|------|-------------|
| `OfflineMessage` | A message left by a visitor when operators are unavailable |

### Notifications

| Type | Description |
|------|-------------|
| `Notification` | A system or chat notification sent to an operator |
| `NotificationDetails` | Type, title, body, and action URL for a notification |

### Reporting

| Type | Description |
|------|-------------|
| `Report` | An aggregated report for an account or group over a time period |
| `DailySummary` | Roll-up statistics for a single day |
| `Metric` | A single numeric data point (chat volume, response time, CSAT) |
| `MetricPeriod` | The time window covered by a metric |
| `MetricDetails` | Dimension breakdown and period-over-period comparison |

### CoBrowse

| Type | Description |
|------|-------------|
| `CoBrowse` | A co-browsing session initiated during a chat |
| `CoBrowseRequest` | The request to initiate a co-browse session |

### File Transfer

| Type | Description |
|------|-------------|
| `FileTransfer` | A file transferred during a chat |
| `FileDetails` | Filename, MIME type, size, and download URL |

### Tags / Shortcuts / Notes

| Type | Description |
|------|-------------|
| `Tag` | A label applied to a chat for categorization |
| `Shortcut` | A saved text snippet an operator can insert during chat |
| `ChatNote` | An internal note attached to a chat by an operator |

### Integrations

| Type | Description |
|------|-------------|
| `Integration` | An external service connected to Olark (CRM, helpdesk, etc.) |
| `IntegrationCRM` | CRM-specific integration with field mapping configuration |

### Custom Data

| Type | Description |
|------|-------------|
| `CustomData` | A custom key-value pair attached to a visitor or chat |

### Authentication

| Type | Description |
|------|-------------|
| `APIToken` | An API credential used for REST API or webhook authentication |

### Account

| Type | Description |
|------|-------------|
| `Account` | The top-level Olark account containing all resources |
| `AccountDetails` | Settings: site ID, plan, timezone, enabled features, webhook URL |

## Root Operations

### Query

Supports fetching: `account`, `chat`, `chats`, `visitor`, `visitors`, `transcript`, `operator`, `operators`, `group`, `groups`, `campaign`, `campaigns`, `automation`, `automations`, `offlineMessages`, `report`, `tags`, `shortcuts`, `integrations`, `apiTokens`, `forms`.

### Mutation

Supports creating and updating: chats, operators, groups, campaigns, automations, tags, shortcuts, API tokens, offline messages, visitor details, and chat notes.

### Subscription

Real-time events: `chatStarted`, `chatEnded`, `messageReceived`, `operatorStatusChanged`, `visitorTyping`, `newOfflineMessage`.

## References

- Olark REST API: https://www.olark.com/api/rest/
- Olark JavaScript API: https://www.olark.com/api
- Olark Help Center: https://www.olark.com/help
- Olark Pricing: https://www.olark.com/pricing
- Olark GitHub: https://github.com/olark
