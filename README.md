# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked 'enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Need a tool to read data from csv file and storing it in the form, possible to analysis
3. Report PDF generator
4. Messaging Service for Notification
5. Calendar

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No			| It involves another tool so it should be a regression
Counting the breaches       | Yes		    | It is needed to check whether functionality that counts breaches is working fine
Detecting trends            | Yes           | can be covered by unit tests as its an functionality, independent from other dependencies
Notification utility        | Yes           | no end to end testing as notification must be sent to user/admin but fake notification service possible

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Count the no. of breaches based on threshold in the month from the csv containing readings
4. Record date and time when the reading was continuously increasing for 30 mins
5. Send notification when new Report available
(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input          		| Output                      | Faked/mocked part
|--------------------------|------------------------|-----------------------------|---
Read input from server     | csv file       		| internal data-structure     | Fake the server store
Validate input             | csv data       		| valid / invalid             | None - it's a pure function
Notify report availability | receiver & via 		| message via email/sms/log   | fake the receiver and notifier
Report inaccessible server | server accessibility   | message as a result         | Fake the server accessibility
Find minimum and maximum   | csv data       		| min and max                 | none - its a pure function
Detect trend               | csv data       		| date and time from csv data | none
Write to PDF               | analysis data     		| PDF file ready              | unit test not possible as need to access storage
