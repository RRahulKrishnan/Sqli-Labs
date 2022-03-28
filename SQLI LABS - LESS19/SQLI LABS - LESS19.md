![](Aspose.Words.cbe4a8bd-12c2-4d4d-a055-7e2a157b72e2.001.png)

This is the PHP code of the website” http://localhost/sqli/Less-18/ “, we have opened it up to analyse and understand why we can’t simply break the query and extract data from the present fields on the webpage.

![](Aspose.Words.cbe4a8bd-12c2-4d4d-a055-7e2a157b72e2.001.png)

This part of the PHP code is basically a function that makes sure that the username and the password fields of the database are non-injectable.

![](Aspose.Words.cbe4a8bd-12c2-4d4d-a055-7e2a157b72e2.001.png)

Here we find an insert query where there is an insert into the:

Uagents

Ip\_address

Unlike the last lesson here we are going to be using the referrer field other than the user agent or the uagent field.

![](Aspose.Words.cbe4a8bd-12c2-4d4d-a055-7e2a157b72e2.001.png)

**PAYLOAD:** INSERT INTO `security`.`referers` (`referer`, `ip\_address`) VALUES ('$uagent', '$IP')

**MYSQL:** 

**+----+------------------------------------------------------------------------------+------------+----------+**

**| id | uagent                                                                   	| ip\_address | username |**

**+----+------------------------------------------------------------------------------+------------+----------+**

**|  1 | mozilla                                                                  	| 127.0.0.1  | test 	|**

**|  2 | Mozilla/5.0 (X11; Ubuntu; Linux x86\_64; rv:98.0) Gecko/20100101 Firefox/98.0 | 127.0.0.1  | admin	|**

**|  3 | Mozilla/5.0 (X11; Ubuntu; Linux x86\_64; rv:98.0) Gecko/20100101 Firefox/98.0 | 127.0.0.1  | admin	|**

**+----+------------------------------------------------------------------------------+------------+----------+**

**+----+---------+------------+**

**| id | referer | ip\_address |**

**+----+---------+------------+**

**|  1 | $uagent | $IP    	|**

**+----+---------+------------+**

![](Aspose.Words.cbe4a8bd-12c2-4d4d-a055-7e2a157b72e2.001.png)

Now using burp suite we edit the user agent value so that we can use sql injection payloads and fuzz the database to extract some data from the database.

**PAYLOAD:** ‘ or ‘1’ = ’1



