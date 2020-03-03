# Reports

## Overview

The netID Developer Portal provides KPIs in individual reports as .cvs files for you to download. Here you can find an overview of the reports provided by the netID Developer Portal.

### General Information

- **Reporting interval**: daily
- **Aggregates**: Rolling time windows, aggregated to 1 day, 7 days, 30 days
- **Reporting period**: A report contains a maximum of 366 days
- Reports are calculated for the partner and each of his existing Relying Party. Each Relying Party will have its figures and the figures of its partner displayed as a sum.

### Reports in the netID Developer Portal

| Report |Description|
|---|---|
| Authentication Dialog | This report shows how many netID users wanted to register with netID and successfully entered their e-mail address for identification on the login page. |
| Authentication Process | The report provides information on how many netID users have completed the authentication process by entering a password. The report shows both successful and unsuccessful authentications. |
| Authentication Process Core Data | The report provides information about which master data was transferred in the authorization process. For each master data, it shows how often "required and optional" (as a total) or only optional master data was transferred in the authorization process. **Note:** This report only contains **daily aggregates**. |
| Authorization Dialog | The report provides information on the frequency of the master data dialog. The dialogue is played out if -  the netID user logs on to the Relying Party for the first time - the Relying Party requires new / different netID User master data - the Relying Party wants to play the master data dialog again.  **Note:** Unique users are also shown.  |
| Authorization Process | The report evaluates how often required and optional (as a total) or only optional master data was transferred after the dialog was confirmed. **Note:** Unique users are also shown. |
| Broker Dialog | The report evaluates how often the netID login flow was started, triggered by a click on the netID login button on the Relying Party page |
| Broker "new netID User" Dialog | The report evaluates the number of entered e-mail addresses that are not yet netID-enabled. These addresses were entered in the Broker dialog by the netID user. |
| Broker Process | The report evaluates the number of events that should continue the netID login flow by entering an email address. It distinguishes between successful and unsuccessful attempts. Successful if the entered e-mail address is known in the netID login context and unsuccessful if the e-mail address is incorrect or could not be assigned.** Note:** Only events that were played out via the Broker dialog are counted.|
| Broker master data transfer | The report provides information about the number of master data transferred, which were forwarded by the OpenID provider. It displays required and optional master data as a total and optional master data separately. |
| Registration Neutral Instance Dialog | The report provides information on how often a registration attempt was initiated for the netID partner. |
| Registration Neutral Instance Process | The report provides information on the number of successful and unsuccessful registrations. |
| SSO active user | The report provides information about the number of active users for the period under consideration, separated by partner and its relying party. A user activity is defined by a successful login. |
| SSO user | The report provides information on the development of the SSO user inventory. |
| SSO user first use | The report evaluates the number of first use of netID separately by partner (total) and its reeling party. |


## Download Reports

The netID Developer Portal provides individual reports as .cvs files for download.

To download a report, click on Reports in the navigation on the left.
An overview of all available reports is displayed.

Click on download to the right of the report you wish to download.

A notification appears asking you whether you want to open or save the report.

Select whether you want to open or save the report by clicking on Open or Save/Save As.

The desired report is downloaded.