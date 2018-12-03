DriverTripReport
======

<b>*To install and run the application please follow these instructions* </b>

1. Navigate to parent folder that contains the 'pom.xml' file
2. Run this code: `mvn install`
3. Navigate to the  'target folder 
4. Run this code: `java -cp RootDriverReport-1.0.jar main.java.RootDriverReport <arguments>`

And insert your file where <arguments> goes without the '<' and '>' on the ends.

***
### Project Summary

A command line application that reads a list of drivers and trips from a .txt file and returns a report with calculations of their total miles and average mph. 

The input file is read by the application with each line prompting one of two commands: 
+ Driver - registers a new driver
+ Trip - logs a trip that includes a driver's name, beginning time, end time, and miles driven.

Any trips with an average mph below 5 or above 100 are considered invalid and ignored.
***
### Process and Approach

My goals were to:
+ Write thorough tests for positive and negative outcomes 
+ To keep the code clean and easy to read
+ Maintain tight encapsulation within all the classes created.

###### Flow summary:

ReportReader reads file and ReportDataManager coverts it to list of drivers which is printed by ReportPrinter.
***

The firsts tests were written for the Driver class followed by Trip. The Driver method was designed with the output file in mind with the driver name, average MPH, and total miles driven but later on, a list of trips was added to be utilized by DriverStatCalculator class for reporting.

The Trip class was modeled with the input file in mind. To keep the conversion and calculation of minutes driven simple, the start and stop times were stored as LocalTime variables, leveraging Java's ChronoUnit class's built in method to calculate the time between start and stop time as well as being able to store a string containing time and avoid any parsing. 

I next created basic test cases for the ReportReader class that reads the input file and returns a List of Strings with each string containing the command and it's parameters. The list of strings is then used by the ReportDataManager class that checks to see if the trip is valid and then maps to the correct driver before returning a List of drivers. In order to check which driver the trip belonged to, an equals override was added to the Driver class with the driverName as the uniqueness identifier.

As functionality was added to the ReportDataManager the class grew harder to read and upon refactoring three private utility methods were extracted and tests for these methods were rewritten using method reflection. The ReportDataManager calls the DriverStatCalculator before returning the list of drivers. 

The final class, other than the main method, is the ReportPrinter which formats the list of drivers for output. Before formatting, this class's method leverages the use of the Comparator interface to sort the list of drivers by miles driven.


