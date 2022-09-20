As you use your linux system in your desktop or server there comes a time when you want certain repetitive tasks to be done at a atomatically by the system at a specified time.These tasks more often that not are some custom scripts that you made to do things like upgrading or backing up the system.Task scheduling in the linux system can be done using various tools among them is cron and at.

In this article I'll be focusing on scheduling of tasks using cron.This article is intended for beginners as well as proffesionals who want a refresher on scheduling tasks using cron.

### What is cron
Cron is a daemon that enables you to run scheduled tasks in the background at specific times  be it  houry, every minte, daily, weekly , at reboot etc. Examples of such tasks are regular backups,system upgrade,sending emails, system maintenance and so on.
These scheduled tasks are stored in crontab files which are different for each user. Crontab files are located at `/var/spool/cron`.

### Installing cron
Cron comes preinstalled in almost all linux distributions. If by chance you don't have it in your system , install it using the commands below:
````bash
sudo apt-get update & apt-get -y upgrade
sudo apt-get install cron
````

### Basic Usage of Cron
Let's first look at the basics of cron before going on to schedule a simple cronjob.
- To show the crontab for the current user , type command `crontab -l` .
- To check the crontab for a specific user you use the `-u` flag.For example you want to check the crontab for the a user named mike, you do `sudo crontab -u mike -l` .
- To edit the cron tab for the current user type in the following command `crontab -e`, whereas if you want to edit the crontab for a different user you use the following command `crontab -u mike -e` , replace "mike" with the name of the user you wish to edit their crontab.
- To remove the crontab of the current user you use the following command `crontab -r`
### Task Scheduling using crontab
##### Creating a simple script
For this article we will write a script at creates a file named **hello.txt** on the desktop, it will contain the current date and time. To begin with, open your favourite text editor, copy the code below in it and save it as **example.sh** .
````bash
#!/bin/bash

date >> ~/Desktop/hello.txt
````

To make the file you've created executable type the following command in your terminal where you've saved your script:
````bash
chmod +x example.sh 
```` 

I usually like saving my personal scripts in `/usr/local/bin` , so lets move our script to that directory using the following command :
````bash
mv ./example.sh /usr/local/bin
````

##### Adding a new task 
Now lets create a cronjob that will execute our script periodically. Lets open our crontab file by entering the command `crontab -e`  our terminal. If you are prompted to select an editor choose nano since it's the easiest to get started with.The file opened should look similar to this:
![[opencron.png]]

Scroll to the bottom of the file and add the following line `* * * * * /usr/local/bin/example.sh` 
Before going forward, let us first understand what the meaning of the line that we've added. This line follows the cron syntax which is `a b c d e command/script`.
- `a` represents minute which ranges from 0-59
- `b` represents the hour which ranges from 0-23
- `c` represents the day which ranges from 0-31
- `d` represents the month which ranges from 0-23
- `e` represents the day of the week which ranges from 0-7. 0 and 7 being sunday
- `command/script` represents the script or command to be executed.
When you use `*` in cron syntax means it will match any value. So our line `* * * * * /usr/local/bin/example.sh`  means that the script will be executed every minute of every hour of every day of the week in every month.
If we wanted our script to be executed  every hour we change it to `0 * * * * /usr/local/bin/example.sh` , every monday  at 12am we change it to `0 0 * * 1 /usr/local/bin/example.sh` and so on. It can be complicated remembering this syntax so to simplify it you can use this website [here](https://crontab.guru/#) to get the cron schedule expressions.
Apart from the five-column systax you can use the cron schedule macros.For this, if we want to :
- run a script hourly we write `@hourly command/script`
- run a script daily we write `@daily command/script`
- run a script weekly we write `@weekly command/script`
- run a script monthly we write `@monthly command/script`
- run a script yearly we write `@yearly command/script` or `@annualy command/script`
- run a script at reboot we write `@reboot command/script`

With that in mind let us carry on.Your crontab file should now look like this:
![[jobcron.png]]
Press ctrl+o to save the crontab file and ctrl+x to exit nano.

##### Checking the output
Heading over to our desktop folder we see that  a **hello.txt** file has been created.Checking the contents of the file we see the current date and time is being appended every minute. Sure enough this is proof that cron is running our script as scheduled.

![[output.png]]
### Conclusion
You now have a good understanding of how you can schedule your tasks in your linux desktop or server. Using the example given you can create a cronjob that executes a script to automate your repetitive tasks.
Thank you for your time.





