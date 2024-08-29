## ***<u>Introduction</u>***
I needed to convert the existing SQL server databases to SQLite databases as part of a DB migration program and did not find any decent free converter to do the job.

This is my attempt to solve the problem. I should warn you though that I did not have much time to test it on too many databases. In any case - the source code is very well documented and easy to understand, so if you do have a problem it should be relatively easy to fix. (Please send me the fixed source code. If you do so, I can update the software so that everybody can enjoy it.)

## ***<u>Using the Code</u>***
The code is split between a dataaccess project (class library) that contains the conversion code itself and a converter project (WinForms) that drives the conversion code and provides a simple UI for user interaction.

The main class that performs the conversion is the sqlservertosqlite class. It does the conversion by doing the following steps:

Reading the designated SQL server schema and preparing a list of tableschema objects that contain the schema for each and every SQL server table (and associated structures like indexes).
Preparing an empty sqlite database file with the schema that was read from SQL server. In this step, the code may alter few SQL-server types that are not supported directly in sqlite.
Copying rows for each table from the SQL server database to the sqlite database.
Basically, that's it!

## ***<u>Points of Interest</u>***
In order to read the SQL server DB schema, I was mainly using the pseudo information_schema.table table. You can find more information about it on the Internet if you want.

## ***<u>History</u>***
* 29th August 2024:<br>
Added datetimeoffset type

* 18th May 2023: Released 2023.05.18.01<br>
Upgraded to .NET 6 as well as added ability to treat UUID/GUID as a string

* 14th January 2013: v1.20<br>
Fixed problem with column names<br>
Added more width to the database names combo box.

* 19th June 2012: v1.19<br>
Added support for ignoring views when creating the DB schema.<br>
Added support for blank characters inside column names.

* 15th Nov 2011: v1.17<br>
Fixed a bug that caused the software to crash when encountering NULL values in some of SQL Server meta data tables.

* 1st July 2011<br>
Updated binary zip as the earlier one was missing the DLL file needed by the application.

* 24th March 2011<br>
Attached compiled version of the project for anyone that doesn't have Visual Studio and still needs to use the utility.

* 4th December 2009: v1.16<br>
Fixed generation code to create GUID types for SQL-Server's uniqueidentifier type (instead of nvarchar as it was until now)<br>
Updated the solution to use the latest SQLite .NET provider library.

* 25th September 2009: v1.15<br>
Fixed a critical bug that caused the primary keys to be discarded<br>
Fixed trigger generation bug.

* 22nd September 2009: v1.14<br>
Fixed a critical bug that caused the conversion process to fail on some SQL Server databases that used the [dbo] notation.

* 20th September 2009: v1.13<br>
Fixed AUTOINCREMENT bug suggested by MAEP<br>
Fixed 64-bit support problem (thanks to Murry Gammash)<br>
Added support for converting SQL Server views (suggested by Richard Thurgood).

* 04th June 2009: v1.12<br>
Fixed a bug in trigger generation code that caused schema generation to fail when more than a single column is referencing the same column in a foreign table.

* 23rd May 2009: v1.11<br>
Added support for simulating foreign keys using triggers (contributed by Martijn Muurman)<br>
Added a small bugfix so that now an 'int' type is always converted to 'integer' type in SQLite. This was needed because SQLite will autoincrement only on 'integer' column types.

* 04th March 2009: v1.10<br>
Fixed a bug that caused the converter to crash when encountering a datetime field in the original SQL server schema. Thanks to bmcclint for sending me the bug with the correct bugfix.

* 21st February 2009: v1.9<br>
Added contribution from Johnny Dickson Cano that allows selecting using SQL server integrated security or using username/password instead<br>
Added support for converting IDENTITY columns to AUTOINCREMENT in SQLite (suggestion by Paul Shaffer).

* 14th December 2008: v1.8<br>
Integrated support for foreign keys from the revised version made by Yogesh Jagota<br>
Merged support for selective table import.

* 05th October 2008: v1.7<br>
Fixed information_schema references to use UPPER-CASE in order to resolve international character set issues (Turkish).

* 22nd July 2008: v1.6<br>
Added support for encrypting the resulting DB file (using the built-in encryption support that exists in the SQLite .NET provider).

* 20th July 2008: v1.5<br>
Added support for case-insensitive columns (COLLATE NOCASE).

* 17th July 2008: v1.4<br>
Fixed a bug that caused wrong columns to become primary keys on rare occasions and improved conversion performance.

* 08th July 2008: v1.3<br>
Fixed a bug that caused the utility to crash sometimes when processing index information.

* 08th July 2008: v1.2<br>
Fixed a bug that caused unique indexes to be generated as non-unique in some cases.

* 13th June 2008:<br>
Initial version.