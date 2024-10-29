java c
CSCI235 – Database Systems, SP424, Assignment 2
Assignment 2 (15% of total marks) 
Due date: Thursday, 7 November 2024 by 9:00 pm Singapore time Scope: 
The tasks of this assignment cover stored PL/pgSQL procedure, function, and trigger. The assignment covers the topics discussed in lecture 7, 8, and 9.
Assessment criteria: 
Marks will be awarded for:
•    Correct,
•    Comprehensive, and
•    Appropriate
application of the materials covered in this subject.
Assignment Specification: 
Preliminary actions 
Instruction: 
1. Download the SQL Script:
o  Obtain the SQL script. file named dbCreateTruck-2024S4.sql from Moodle.
2. Execute the Script:
o  Run the script. in your PostgreSQL environment to create and populate the sample database. This database contains information about:
Employees working for a transportation company
Drivers employed by the company
Trucks owned by the company
Trips made by the drivers and trucks
All legs of each trip
3. Database Exploration :
o  After  executing  the  script,  it  is strongly  recommended to  explore  the structure of the database by examining the conceptual schema. This can be represented as a  UML diagram to  help you  understand  the  relationships between different tables and entities within the database.
o  Note: No marks will be awarded for producing or submitting the conceptual schema.
Task 1 (7.0 marks) 
Stored PL/pgSQL Procedure 
Task Specification: 
Objective: You  are  required  to  implement  a stored  PL/pgSQL  procedure that  inserts  full information about an employee into the database. The employee's details will include the following attributes:
• E# : Employee number
• NAME : Employee name
• DOB: Date of birth
• ADDRESS: Residential address
• HIREDATE : Date of hire
• L# : License number (if applicable)
• STATUS: Employment status
• EXPERIENCE : Experience (only for mechanics)
Consistency Constraint: 
Your procedure must enforce the following logical consistency constraint:
•     The sets of drivers and mechanics must be disjoint.
o  This means that an employee cannot be both a driver and a mechanic.
o  It is not allowed for the same employee (with the same employee number E# and/or license number L#) to exist in both the MECHANIC and DRIVER tables.
Stored Procedure Requirements: 
•     The procedure should:
o Insert full information about the employee into the relevant table(s).
o Check  the   disjoint constraint:   Before  inserting,  ensure  that  the employee number E# and license number L# do not already exist in the other table (i.e., an employee cannot be both a driver and a mechanic).
o  If the consistency constraint is violated, the procedure should fail with an appropriate error message.
Execution Instructions:
1. First Execution :
o  Execute  the  procedure to  insert full information for a new employee (either a driver or a mechanic) who does not violate the consistency constraint.
2. Second Execution :
o  Execute the  procedure  again, attempting to insert an employee whose details (either E# or L#) will violate the consistency constraint (i.e., trying to insert an employee who is already in the other table).
o  This second execution should fail due to the constraint, demonstrating the procedure’s ability to enforce logical consistency.
3. PL/pgSQL Script.: 
o  Write and save the stored procedure implementation in a PL/pgSQL script. named solution3.sql.
4. Execution Output: 
o  Execute  the  script. twice  as  described  above  and  capture  the  output (including success and error messages) in a file named solution3.lst.
Submission Instructions: 
You are required to submit two files:
1. solution1.sql – This file should contain all the SQL statements.
2. solution1.pdf – A report containing screen captures of your SQL output.
Report Guidelines: 
•     Your report must include:
o Screenshots of the SQL output: Copy and paste the screen output from your terminal into a document, then save it as a PDF file.
o SQL statements processed : The report must list all SQL statements that were executed.
o  Ensure there are no errors in the output shown in your report.
SQL Script. Requirements: 
•     Include the following settings at the beginning of your script:
o  \set ECHO all – This will ensure that all SQL commands are echoed to the terminal.
o  \set ECHO none – Use this to stop echoing the commands when needed.
Important Notes: 
•     Your printouts must satisfy all the above requirements. Any report that fails to meet these requirements will receive no marks.
Task 2 (5.0 marks) 
Stored PL/pgSQL Trigger 
Task Specification: 
Objective: 
You  are  required  to  implement  a row-level trigger that  ensures  the  following consistency constraint:
•     The column totalTripMade in the DRIVER table is currently empty (i.e., does not contain any values).
•     You   need   to   create   a   row   trigger   that automatically updates the totalTripMade column when a new trip made by a driver is inserted into the TRIP table.
Trigger Details: 
•     The trigger will activate after each new trip is inserted into the TRIP table.
•     Once triggered, it will calculate the total number of trips made by the driver and update the totalTripMade column in the DRIVER table accordingly.
Important Notes: 
• PL/pgSQL Script.: 
•     Implement the trigger logic in a PL/pgSQL script. and save it as solution2.sql.
• No  need  to  handle  DELETE or  UPDATE cases : You  are only required to consider the scenario where new trips are inserted into the TRIP table.
•     Your trigger should only  update the totalTripMad代 写CSCI235 – Database Systems, SP424, Assignment 2SQL
代做程序编程语言e column  based on  newly inserted trips. Other operations (such as trip deletions or updates) do not need to be considered.
• Recording Results: 
•     Process the script. (solution2.sql) in PostgreSQL and record the output (results of processing) in a file named solution2 in pdf format.
• Output File: 
•     Ensure that your solution2.pdf file captures any messages or results from running the  script,  such  as  successful  trigger  creation  or  output  generated  during insertions into the TRIP table.
Submission Instructions: 
You are required to submit two files:
1. Solution2.sql – This file should contain all the SQL statements.
2. Solution2.pdf – A report containing screen captures of your SQL output.
Report Guidelines: 
•     Your report must include:
o Screenshots of the SQL output: Copy and paste the screen output from your terminal into a document, then save it as a PDF file.
o SQL statements processed : The report must list all SQL statements that were executed.
o  Ensure there are no errors in the output shown in your report.
SQL Script. Requirements: 
•     Include the following settings at the beginning of your script:
o  \set ECHO all – This will ensure that all SQL commands are echoed to the terminal.
o  \set ECHO none – Use this to stop echoing the commands when needed.
Important Notes: 
•     Your printouts must satisfy all the above requirements. Any report that fails to meet these requirements will receive no marks.
Task 3 (3.0 marks) Task Specification: 
Objective: You    are    required    to    implement    a stored     PL/pgSQL    function called LONGTRIP(DLNUM), which calculates the length (i.e., the total number of legs) of the longest trip performed by a driver. The driver is identified by their driving license number (L#), which corresponds to the DLNUM parameter passed to the function.
Function Details: 
1. Parameters:
o DLNUM :  The  driving  license number of the driver (L# in the DRIVER table).
2. Function Logic:
o  The function should find the length of the longest trip (i.e., the trip with the most legs) performed by the driver with the given driving license number (DLNUM).
o  The function should consider drivers who have not performed any trips. For such drivers, the function should return a length of 0.
o  The function should correctly handle cases where a driver exists in the DRIVER table but has no associated trips in the TRIP table.
Expected Output: 
•     For a driver who has performed trips, the function will return the total number of legs in their longest trip.
•     For a driver who has not performed any trips, the function should return 0.
Usage:After implementing the LONGTRIP(DLNUM) function, use it in a SELECT statement to generate a report listing the names of all drivers, along with the length of their longest trip (calculated using the LONGTRIP function).
Example Query: 
SELECT NAME, LONGTRIP(L#) AS LongestTrip FROM DRIVER;
This query should return the names of all drivers along with the length of their longest trip.
Execution Instructions: 
1. PL/pgSQL Function: 
o  Write  the  function  definition  and  save  it  in  a  PL/pgSQL  script. named solution3.sql.
2. Execution Output: 
o  Use the function in a SELECT statement (as demonstrated above) to list the names of all drivers and their longest trips.
o  Save  the  output  of  this  query  in  a  file  in  pdf  format,  and  name  it solution3.pdf.
Submission Instructions: 
You are required to submit two files:
3. Solution3.sql – This file should contain all the SQL statements.
4. Solution3.pdf – A report containing screen captures of your SQL output.
Report Guidelines: 
•     Your report must include:
o Screenshots of the SQL output: Copy and paste the screen output from your terminal into a document, then save it as a PDF file.
o SQL statements processed : The report must list all SQL statements that were executed.
o  Ensure there are no errors in the output shown in your report.
SQL Script. Requirements: 
•     Include the following settings at the beginning of your script:
o  \set ECHO all – This will ensure that all SQL commands are echoed to the terminal.
o  \set ECHO none – Use this to stop echoing the commands when needed.
Important Notes: 
•     Your printouts must satisfy all the above requirements. Any report that fails to meet these requirements will receive no marks.
Submissions 
This assignment is due by 9:00 pm (2100 hours) Thursday, 7 November 2024, Singapore time.
Submit the files solution1.sql, solution1.pdf, solution2.sql, solution2.pdf, solution3.sql, and solution3.pdf through Moodle in the following way:
1)   Zip all the files (solution1.sql, solution1.pdf, solution2.sql, solution2.pdf,
solution3.sql, and solution3.pdf into one zipped folder. Name your zipped file as YourPUStudentNumber-A3)
2) Access Moodle at http://moodle.uowplatform.edu.au/ 
3)   To login use a Login link located in the right upper corner the Web page or in the middle of the bottom of the Web page
4)   When successfully logged in, select a site CSCI235 (SP424) Database Systems
5)   Scroll down to a section Submissions of Assignments
6)   Click at Submit your Assignment 1 here link.
7)   Click at a button Add Submission
8) Move the zipped file created in Step 1 above into an area provided in
Moodle. You can drag and drop files here to add them. You can also use a link Add… 
9)   Click at a button Save changes,
10) Click at check box to confirm authorship of a submission,
11) When you are satisfied, remember to click at a button Submit assignment.





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
