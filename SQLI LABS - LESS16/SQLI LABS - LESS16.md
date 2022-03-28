Here we are greeted with a form or a login page that asks us to insert the username and password that is necessary for logging into the website.

![](Aspose.Words.16190a18-191a-405e-a590-90d6f6a3959d.001.png)

We proceed by fuzzing with the inputs of the following fields and find that “admin” works in this case as both username and password.

![](Aspose.Words.16190a18-191a-405e-a590-90d6f6a3959d.001.png)![](Aspose.Words.16190a18-191a-405e-a590-90d6f6a3959d.001.png)

**PAYLOAD:** ") or 1=1 #

Now as we see that the error or any iterative message is not visible on the web page, thereby we will be using sleep parameter we will extract information one by one from the database.

![](Aspose.Words.16190a18-191a-405e-a590-90d6f6a3959d.001.png)

**PAYLOAD:** ") or sleep(15) #

When we use this payload to check if the condition is true or not it will either sleep(or load) for the number of seconds that is mentioned within the payload.

![](Aspose.Words.16190a18-191a-405e-a590-90d6f6a3959d.001.png)

**PAYLOAD:** admin") and if(1=1, sleep(10),null) # 

When we apply this payload we see that the page loads or sleeps for exactly 10 seconds and then gives the above screen as the output.

**PAYLOAD:** admin") and if(database()=’security’, sleep(10),null) # 

Similar to the previous payload and with a minimal modification we get the same output after a certain period of the wait which is basically the sleep time or the loading period.
