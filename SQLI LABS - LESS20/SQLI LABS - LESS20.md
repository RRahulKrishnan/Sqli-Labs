Similar to the previous challenges here we are greeted with a form or a login page which asks us to insert the username and password that is necessary for logging into the website.

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

We proceed by fuzzing with the inputs of the following fields and find that “admin” works in this case as both username and password.

But here as we can see mysql helps us in looking into the data that is present within the database or tables.

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

Now using one of the credentials that we saw in the mysql database we will login to the page.

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

These credentials are then stored as cookies within the webpage we can access them and change their values and try breaking the query.

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

We proceed by invalidating the first part of the payload by eliminating “Dumb” from the payload.

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

**PAYLOAD**: ’ union select 1,group\_concat(column\_name),3 from information\_schema.columns where table\_schema='security' #

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

**PAYLOAD**: ' union select 1,group\_concat(table\_name),3 from information\_schema.tables where table\_schema='security' #

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

**PAYLOAD**: ' union select 1,group\_concat(username),3 from users #

![](Aspose.Words.19c32a14-8bc3-439b-b209-dcfc8a9063be.001.png)

**PAYLOAD**: ‘ union select 1,group\_concat(username),group\_concat(password) from users #
