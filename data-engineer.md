# Fresh8 Data Engineer Coding Challenge

## Rules

Feel free to spend as much or as little time on the exercise as you like, as long as the following requirements have been met: 

- Please complete at least one of the tasks described above.
- You should provide clear instructions on your test setup and how to execute your tests. The clarity and precision of these instructions - and the ease with which the interviewers can execute them - will be a key part of the assessment. Please create a README file detailing said instructions. Please also use this file for listing any additional comments or observations you might want to share about your submission.

You can create the solution in any language or framework of your choice.

To complete the challenge, please provide us with your codebase. This can either be in a new repository, provided to us as a compressed file, or any other method you feel is acceptable.

## Tasks

Fresh8 raises a variety of events but the core business events consist of `Viewed`, `Interacted` and `Click-Through`.

The challenge consists of two tasks:

* Write an app that can generate core business events in batches; then write those events to a line-delimited JSON file at specified intervals.
* Stream the line-delimited JSON files that you generated in step one into program which will output a running total of each event type to the terminal every five seconds.

### Generator App
Write an app that can generate core business events:

* Each event grouping will produce one of the following sets of events:
	* `Viewed` (85%)
	* `Viewed` -> `Interacted` (5%)
	* `Viewed` -> `Click-Through` (5%)
	* `Viewed` -> `Interacted` -> `Click-Through` (5%)
* The batch of events within a given interval should be stored in a line-delimited JSON file named `events-<timestamp>.json` ex. events-2017-05-14-18-47-29-879763.json
* The app must take 4 arguments
	* `number-of-groups` - Number of event groups to generate which will each produce one or more events, based on the probability listed above.
	* `batch-size` - Batch size of events per file.
	* `interval` - Interval in seconds between each file being created.
	* `output-directory` - Output directory for all created files.
* How to run the app

```bash
generate-events --number-of-groups=1000000 --batch-size=5000 --interval=1 --output-directory=<local-dir>
```
* Example shows a snippet of ten event groups from the content of a generated file. Each event is on its own line separated by a linebreak.

```json
{ "type": "Viewed", "data": { "viewId": "aa072e9e-cb04-45c8-9ad6-cfeae76dcbe7", "eventDateTime": "2018-05-14T12:00:00Z" } }
{ "type": "Interacted", "data": { "viewId": "aa072e9e-cb04-45c8-9ad6-cfeae76dcbe7", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Viewed", "data": { "viewId": "1665f348-086a-4781-9aad-4ede19535376", "eventDateTime": "2018-05-14T12:00:00Z" } }
{ "type": "Click-Through", "data": {"viewId": "1665f348-086a-4781-9aad-4ede19535376", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Viewed", "data": { "viewId": "e78a2f0c-f0bf-4b6c-947f-5988233f74bd", "eventDateTime": "2018-05-14T12:00:00Z" } }
{ "type": "Viewed", "data": { "viewId": "da4a7eae-e801-480f-bfc0-03438ec8da6d", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Viewed", "data": { "viewId": "522187cb-439a-4327-9958-9321a7d23b27", "eventDateTime": "2018-05-14T12:00:00Z" } }
{ "type": "Viewed", "data": {"viewId": "5dd31ff0-18b7-41d2-95b4-c4264d8b15c3", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Viewed", "data": {"viewId": "38391820-dee0-44da-9926-b23cbd9a7fed", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Interacted", "data": { "viewId": "f017a45c-0886-452f-b867-1b4586ae73bf", "eventDateTime": "2018-05-14T12:00:00Z" } }
{ "type": "Click-Through", "data": {"viewId": "f017a45c-0886-452f-b867-1b4586ae73bf", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Viewed", "data": {"viewId": "6e820e8d-fc55-49dc-a017-818b756e4d31", "eventDateTime": "2018-05-14T12:00:00Z"} }
{ "type": "Viewed", "data": { "viewId": "3aea6700-ce17-4316-af27-e1fb79bd51af", "eventDateTime": "2018-05-14T12:00:00Z" } }
{ "type": "Viewed", "data": { "viewId": "f017a45c-0886-452f-b867-1b4586ae73bf", "eventDateTime": "2018-05-14T12:00:00Z"} }
```
* Every `Interacted` and `Click-Through` event must have a `Viewed` event with the same `viewId`.

### Streamer App
Write an app that can stream the events generated:

* Monitor a given directory for new files.
* Process new files containing order events.
* Output a running total for each event type to the terminal.
* Keep a 5 second delay between each terminal output.
ex. Terminal displaying a running total of each event type from the previous JSON snippet
```bash
"Viewed": 10
"Interacted": 2
"Click-Through": 2
```
