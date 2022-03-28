This is the PHP code of the website” http://localhost/sqli/Less-18/ “, we have opened it up to analyse and understand why we can’t simply break the query and extract data from the present fields on the webpage.

![](Aspose.Words.f33c7222-47bf-4945-9077-eb72898fa366.001.png)

This part of the PHP code is basically a function that makes sure that the username and the password fields of the database are non-injectable.

![](Aspose.Words.f33c7222-47bf-4945-9077-eb72898fa366.001.png)

Here we find an insert query where there is a insert into the:

Uagents

ip\_address

username 

![](Aspose.Words.f33c7222-47bf-4945-9077-eb72898fa366.001.png)

**PAYLOAD:** INSERT INTO `security`.`uagents` (`uagent`, `ip\_address`, `username`) VALUES ('mozilla', '127.0.0.1', 'test');

Now we will be changing the parameters of the values using the SQL query to mozilla, 127.0.0.1, test.

![](Aspose.Words.f33c7222-47bf-4945-9077-eb72898fa366.001.png)

` `Now lets tru to fuzz the login page

![](Aspose.Words.f33c7222-47bf-4945-9077-eb72898fa366.001.png)

We get a message that we had edited earlier![](Aspose.Words.f33c7222-47bf-4945-9077-eb72898fa366.002.jpeg)

Now using burp suite we edit the user agent value so that we can use sql injection payloads and fuzz the database to extract some data from the database.

**PAYLOAD:** ‘ or ‘1’ = ’1
