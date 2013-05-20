# Course Awards report for Moodle 2.x

Course Awards: A quick and easy way of getting a course's rating from students, awarding courses medals based on score, and reporting on courses Moodle-wide.

This [report](https://github.com/vaughany/moodle-report_courseawards): A high level overview (admins only) of all the votes cast, notes and medals awarded across the whole site.

> **See also:** the '[vote](https://github.com/vaughany/moodle-block_courseawards_vote)' block and the '[medal](https://github.com/vaughany/moodle-block_courseawards_medal)' block.

## News: Highlighted in May 2012 OFSTED Good Practice report

The Course Awards plugins have been highlighted in a May 2012 OFSTED Good Practice report into South Devon College, alongside Moodle itself. (Look out for 'Moodle Medals' as it's known locally.)

* [OFSTED web page](http://www.ofsted.gov.uk/resources/good-practice-resource-making-most-of-information-and-communication-technology-south-devon-college)
* [PDF](http://www.ofsted.gov.uk/sites/default/files/documents/surveys-and-good-practice/s/South%20Devon%20College%20-%20Good%20practice%20example.pdf)

## Introduction

The Course Awards plug-in system consists of two blocks ('Vote' and 'Medal') and a report. Its purpose is to easily collect user feedback about a course with appropriate back-end reporting.

It is probably a good idea to fully read through this readme before embarking on any installation or bug reporting.

## Licence

Course Awards report for Moodle 2, &copy; 2013 Paul Vaughan.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.

## Purpose

The Course Awards blocks and report form part of a much larger Moodle course rating system (called Moodle Medals) which is used to recognise good practice on Moodle courses and also provide targets for course development. Learner feedback is used to inform medals awarded, however a course must also meet or exceed other criteria to gain a medal. The Bronze medal has basic criteria which must be met, the Silver medal has moderate criteria and the Gold medal has quite strict criteria.  The criteria themselves and how they are judged is performed by staff manually: this plugin is used to inform one aspect of that process.

Irrespective of this, the blocks and report can still be used to gain useful feedback from students about Moodle courses.

## The Admin Report

![The main page of the Admin Reports](http://commoodle.southdevon.ac.uk/file.php/2/course_awards_images/report-main.png "The main page of the Admin Reports") ![Admin Report showing course detail](http://commoodle.southdevon.ac.uk/file.php/2/course_awards_images/report-detail.png "Admin Report showing course detail")

For administrators only, there is a comprehensive report detailing the courses with most/least votes, all notes, students who voted the most/highest/lowest, etc. Each report can be sorted by different criteria and can be saved as a CSV file if desired.

Admins can jump directly from a course to the admin report using the vote block, and the report is also accessible by clicking Reports &rarr; Course Awards on the Admin block.

### Administrative Options (Destructive!)

*Here be dragons. Consider yourself warned.*

A more recent addition is the destructive administrative options section further down. As the title suggests, they are operations to clear out part or all of the live and/or deleted votes, notes and medals. They perform actions on the database tables used by the blocks, and any data removed is gone for good: a student deleting a vote simply flags that vote as deleted, but removing all votes via this report will permanently remove them from the database for good.

At the bottom are some statistics about how many votes, notes and medals currently exist in the system, as well as number of active voters.

## Installation

Installation is a matter of copying files to the correct locations within your Moodle installation, but it is always wise to test new plugins in a sandbox environment first, and have the ability to roll back changes.

> **Note:** The [Vote](https://github.com/vaughany/moodle-block_courseawards_vote) and [Medal](https://github.com/vaughany/moodle-block_courseawards_medal) blocks are prerequisites for the installation of the report. If either block is not installed, installation of the report will not be possible.

Download the archive and extract the files, or [clone the repository from GitHub](https://github.com/vaughany/moodle-courseawards/). You should see the following files and structure:

    courseawards/
    |-- admin.php
    |-- get_csv.php
    |-- gpl-3.0.txt
    |-- img
    |   |-- arrow_down.png
    |   |-- cross.png
    |   `-- tick.png
    |-- index.php
    |-- lang
    |   `-- en
    |       `-- report_courseawards.php
    |-- pix
    |   `-- icon.png
    |-- readme.md
    |-- report.php
    |-- settings.php
    |-- styles.css
    `-- version.php

* Create a folder in your Moodle's '**report**' folder called '**courseawards**' and place the above files into it. Do not create subfolders.

* Log in to your Moodle as Admin and click on Notifications on the Admin menu.

* The report should successfully install. If you receive any error messages, please [raise an issue on GitHub](https://github.com/vaughany/moodle-courseawards/issues).

### CSV save path

The CSV file, created when a report is run, is saved to the following location:

    $CFG->dataroot.'/temp/courseawards-report.csv'

...which is defined in two places:

    /report/courseawards/report.php:62:     define('FILE_CSV', $CFG->dataroot.'/temp/courseawards-report.csv');
    /report/courseawards/get_csv.php:34:    define('FILE_CSV', $CFG->dataroot.'/temp/courseawards-report.csv');

This location is part of Moodle and should already be writable by the web server. If you experience problems, ensure the path is writable, touch the file and give it full read/write permissions, or change to a different location (remember to change both the above DEFINE statements and ensure they are identical).

## Using the Report

* Reports are *currently* available to site administrators only.
* On the Admin menu, click Reports, then Course Awards.
* Click on the report you would like to see.
* You can sort the reports differently by clicking on the column titles.
* If the course has votes or notes, click on the number in the votes/notes column and you will see specific details about that course's votes and notes.
* If no courses have been voted on, no data will be available.
* Click 'Save as CSV' to do just that.
* Pie charts are and require an internet connection.

> **Note:** The pie chart is dependent on [Google Chart Tools](https://developers.google.com/chart/interactive/docs/gallery/piechart) to generate interactive charts on the fly. This requires an internet connection. If one is not available, the image will not be shown. Due to the interactive nature of the chart, it cannot be saved as an image by (for example) right-clicking and choosing 'Save image as...'. There are many good desktop apps and browser plugins for saving screenshots.

### Changing Permissions on the Admin Report

Moodle's reports (Admin block, click Reports) can be viewed only by site administrators. As such, the Course Awards reports are available only to site administrators, not Course Awards block admins.

### Save as CSV

This option appears on all pages where there is a table of data relating to courses or users. Use it to save the results out as a CSV file, which can then be opened with your favourite spreadsheet or word processing application.

> **Note:** If two admins are generating reports concurrently, the CSV file will be overwritten by the most recently generated report.

## Code and Image Changes

Some aspects of the report can be changed but this cannot be achieved though configuration, and will require changes to the code. A good code management and versioning system, such as Git, is highly recommended.

### Replacing the Images

It is quite possible to replace the default images with those of your own choosing:

* In '*report/coursewards/*' there is an '*img/*' folder containing images.
* Replace these images with your chosen images.
* To avoid having to change the code, save new images over the existing images. Do not use new names.

> **Note:** You may want to make copies of the images before you change them so you can restore them later.

> **Caution:** The code does not specify any widths or heights for images, so that you can use your own and they do not have to be the same size as the default images. However, it is not recommended to go too much wider than the default images as you may start experiencing layout problems with your columns. Experiment.

## Known Issues

* Report:
  * Issue with [MSSQL not having a 'LIMIT' clause](https://github.com/vaughany/moodle-courseawards/issues/2).

Should you find a bug, please [log an issue in the tracker](https://github.com/vaughany/moodle-courseawards/issues) or fork the repo, fix the problem and submit a pull request.

## To Do

* Currently the reports are available to Admins only. Moodle now differentiates between site reports and course reports, so a teacher-accessible course report is on the agenda for the next version.
* Looking at the old Mods and Plugins database entry for 'Course Awards for Moodle 1.9', someone commented that clicking on a star image may not be the most accessible way of using the block, citing issues with colour-blindness and the colours potentially lacking meaning to some. The commenter also suggested some improvements so I will look into this for the next release.
* Some of the larger language string references use underscores (`admin_error`) and others use dashes (`admin-error`). For less future headaches, this should be changed. Preference is underscores.
* Logging of use of the admin reports was around in the 1.9 version, so I should probably add it back in again. For completeness' sake, if nothing else.

Suggestions for features or submissions of non-en language packs are most welcome.

## History

**January 25th 2013 - Blocks**

* Version bump for Moodle 2.4
* Build 2013012500

Tested successfully against Moodle 2.4.1.
Added the capability 'addinstance' to both blocks.

**October 11th 2012**

* Version bump for Moodle 2.x
* Build 2012101100

No major changes, just added icons and a copy of the GPL 3.0, and version bump.

**May 17th 2012 - Vote Block**

* Version 2.0.2 for Moodle 2.x
* Build 2012051700

Fixed an issue whereby a variable double-quoted in a SQL snippet failed in MS SQL and was considered a column name.

Also, changed code where required to meet Moodle's coding guidelines (using the local Codechecker) but no changes to how the code works.

**March 19th 2012 - Medal Block**

* Version 2.0.1 for Moodle 2.x
* Build 2012031900

Fixed some errors with the Medal block, added two new features:

* Fixed a redirect bug when awarding a medal (it would redirect to the main page)
* Added 'Awarded on' and date when a medal is awarded
* Added admin option to change size of pictures between regular (the default at 100px high) and small (50px high)
    * ...which necessitated adding smaller versions of the default images and an admin config page

**February 8th 2012 - Whole System**

* Version 2.0 for Moodle 2.x
* Build 2012020800
