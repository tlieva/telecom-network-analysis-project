FILENAME REFFILE '/home/u59415283/Project/JPmorgan_chase.csv';
PROC IMPORT OUT=WORK.JPmorgan_chase
	DATAFILE=REFFILE
	DBMS=CSV REPLACE ;
	delimiter=',';guessingrows=5000;
	GETNAMES=YES;
RUN;

proc sql;
	create table Tab01 as
		select distinct *
	from JPmorgan_chase;
quit;

options validvarname=any;
data Tab01;
set Tab01;
rename 
'Institution Name'n = Institution_Name
'Main Office'n = Main_Office
'Branch Name'n = Branch_Name
'Branch Number'n = Branch_Number
'Established Date'n = Established_Date
'Acquired Date'n = Acquired_Date
'Street Address'n = Street_Address
'2010 Deposits'n = Deposits_2010
	'2011 Deposits'n = Deposits_2011
	'2012 Deposits'n = Deposits_2012
	'2013 Deposits'n = Deposits_2013
	'2014 Deposits'n = Deposits_2014
	'2015 Deposits'n = Deposits_2015
	'2016 Deposits'n = Deposits_2016;
run;
proc stdize data=work.Tab01
	out= work.tab01
	reponly missing=0;
	var Deposits_2010 Deposits_2011 Deposits_2012 Deposits_2013 Deposits_2014 Deposits_2015 Deposits_2016;
run;

/*Removing outliers*/
/* Calculating Total Deposits */
Proc sql;
 create table Tab02 as
 	select Tab01.*, Tab01.Deposits_2010+Tab01.Deposits_2011+Tab01.Deposits_2012+ Tab01.Deposits_2013+ Tab01.Deposits_2014+ Tab01.Deposits_2015+ Tab01.Deposits_2016 AS Total_Deposits
 	from Tab01;
 run;
/*Removing outliers*/
proc sql;
	Create table Tab03 as
	Select Tab02.*
	From Tab02
	Where Tab02.Total_Deposits>0;
QUIT;
proc contents DATA=WORK.Tab02;
RUN;
proc sql;
	Create table Tab04 as
	Select Tab03.*
	From Tab03
	Where Tab03.Total_Deposits Between 10 and 2000000;
QUIT;
proc contents DATA=WORK.Tab04;
RUN;
proc export data=WORK.Tab04 dbms=xlsx outfile="/home/u59415283/Project/AnalyticalfileTeam6.xlsx" replace; run;
