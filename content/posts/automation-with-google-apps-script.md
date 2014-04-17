Title: Automation with Google Apps Script
Date: 2012-03-11 19:56
Author: andrewsomething
Category: Ubuntu
Tags: calendar, google, snippets, trello, Ubuntu
Slug: automation-with-google-apps-script

I maintain a [GCal of the Ubuntu release schedule][], and I just updated
it to contain the proposed schedule for the Q-series. As you can
imagine, adding all those events by hand can be annoying. Luckily you
can use [Google App Script][], which is more or less JavaScript for the
Google Cloud, to automate tasks like this.

I could have probably come up with something to automate the entire
process start to finish, scrapping the wiki every few days and pushing
out updates. But this isn't something that I have to do all that often,
so I just wanted to write something quick and simple. Here's what I
ended up with:

    var EVENT_ADDED = "EVENT_ADDED";

    function sheet2cal() {
      var sheet = SpreadsheetApp.getActiveSheet();
      var startRow = 2;  // First row of data to process
      var numRows = sheet.getLastRow()-1;   // Number of rows to process
      var dataRange = sheet.getRange(startRow, 1, numRows, 5);
      var data = dataRange.getValues();
      var cal = CalendarApp.openByName("Ubuntu Release Schedule");
      for (var i = 0; i < data.length; ++i) {
        var row = data[i];
        var tstart = row[0]; 
        var title = row[1];
        var desc = row[2];
        var tstop = "";
        var eventAdded = row[4];
        if (eventAdded != EVENT_ADDED) {  // Prevents sending duplicates
          cal.createAllDayEvent(title, tstart, {description:desc});
          sheet.getRange(startRow + i, 5).setValue(EVENT_ADDED);
          SpreadsheetApp.flush();
        }
     }
    }

This iterates through a spreadsheet where the first column is the
event's date, the second one is the title, and the third is the
description. It also checks a fourth column to make sure the event
hasn't already been added, marking events added as it goes. It is
closely based on the [example][] of how to send emails from a
spreadsheet.

To add a script like this, go to **Tools \> Script editor...** in your
spreadsheet. This will open an IDE where you can write, run, and debug
your script. If you want, you can add a custom menu on your
spreadsheet's tool bar to trigger the script with something like:

    function onOpen() {
      var ss = SpreadsheetApp.getActiveSpreadsheet();
      var menuEntries = [ {name: "Add to calendar", functionName: "sheet2cal"} ];
      ss.addMenu("Scripts", menuEntries);
    }

You can also set scripts that will be [triggered at specific time
intervals][], [communicate with other services][], and do things like
[parse JSON][]. This opens up a lot of possibilities.

For instance, I'm on a team that is using [Trello][] for internal
organization and task tracking. [Kevin Pelgrims has a great example][]
of integrating Trello and Google Docs to track project progress over
time that I've started using.

  [GCal of the Ubuntu release schedule]: http://andrewsomething.wordpress.com/2011/08/19/ubuntu-release-calendar/
  [Google App Script]: http://code.google.com/googleapps/appsscript/guide.html
  [example]: http://code.google.com/googleapps/appsscript/articles/sending_emails.html
  [triggered at specific time intervals]: http://code.google.com/googleapps/appsscript/guide_events.html#TimeTriggers
  [communicate with other services]: http://code.google.com/googleapps/appsscript/class_urlfetchapp.html
  [parse JSON]: http://code.google.com/googleapps/appsscript/class_utilities.html#jsonParse
  [Trello]: https://trello.com/
  [Kevin Pelgrims has a great example]: http://kevinpelgrims.com/blog/2012/03/06/project-progress-tracking-with-google-docs-and-trello
