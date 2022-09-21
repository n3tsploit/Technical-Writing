# Scheduling Tasks in  Linux Using Cron
As you use your Linux system on your desktop or server, you may want certain repetitive tasks to be performed automatically by the system at a predetermined time. These tasks are usually custom scripts that you wrote to do things like upgrade or backup the system. Task scheduling in Linux can be accomplished using a variety of tools, including cron and at.

In this article, I'll concentrate on task scheduling with cron.

### What exactly is cron?
Cron is a daemon that allows us to run scheduled tasks in the background at specific intervals, such as hourly, monthly, daily, weekly, at reboot, and so on. Regular backups, system upgrades, emailing, system maintenance, and so on are examples of such tasks.

These scheduled tasks are saved in user-specific crontab files. Crontab files can be found in the directory `/var/spool/cron`.

### Setting up cron
Cron is included with almost all Linux distributions.Run the following commands to install it if you don't already have it:

````bash

sudo apt-get install cron

````

### Cron's Basics
Before we schedule a simple cronjob, let's review the basics of cron.
- Use the command `crontab -l` to inspect your crontab file.
- The `-u` option checks the crontab for a specific user. Type `sudo crontab -u mike -l` to view the crontab for the user mike.
- To edit the crontab for the current user, type `crontab -e`; to edit the crontab for another user, type `crontab -u mike -e`, replacing "mike" with the name of the user whose crontab you want to edit.
- Use the command `crontab -r` to remove the current user's crontab.

### Crontab Task Scheduling
##### Making a basic script
For this article, we will write a script that creates a file on the desktop called **hello.txt** and adds current date and time to it everytime it runs. To begin, open your favorite text editor, copy the code below, and save it as **example.sh**.
````bash

#!/bin/bash

  

date >> ~/Desktop/hello.txt

````

To make your script executable, enter the following command in the terminal where you saved it:
````bash

chmod +x example.sh 

`````

I usually like saving my scripts in `/usr/local/bin` , so let's move our script to that directory using the following command :

````bash

mv ./example.sh /usr/local/bin

````

###### Creating a new task
Let's now create a cronjob that will run our script on a regular basis. Let's open our crontab file by typing `crontab -e` into our terminal. If you're asked to choose an editor, go with nano because it's the easiest to get started with. The opened file should look like this:
![[opencron.png]]

At the bottom of the file, add the following line: ``* * * * * /usr/local/bin/example.sh
Before we go any further, let us define the significance of the new line. This line follows the cron syntax of   `a b c d e command/script`
- `a` represents a minute ranging from 0 to 59

- `b` represents the hour, ranging from 0 to 23

- `c` represents the day, ranging from 0 to 31

- `d` represents the month, ranging from 0 to 23

- `e` represents the weekday, which ranges from 0 to 7, with 0 being Sunday and 7 being Saturday.

- `command/script` represents the script or command that will be run.

The use of `*` in cron syntax indicates that it will match any value. So our line `* * * * * /usr/local/bin/example.sh`   means that the script will be run every minute, hour, day, week, and month.

If we wanted our script to run every hour, we would change it to `0 * * * * /usr/local/bin/example.sh` ,to be run every Monday at 12am we change it to `0 0 * * 1 /usr/local/bin/example.sh` and so on. It can be difficult to remember this syntax, so you can get the cron schedule expressions from this website [here](https://crontab.guru/#).

You can use the cron schedule macros in addition to the five-column syntax. If we want to:-
- run a script hourly we write `@hourly command/script`

- run a script daily we write `@daily command/script`

- run a script weekly we write `@weekly command/script`

- run a script monthly we write `@monthly command/script`

- run a script yearly we write `@yearly command/script` or `@annualy command/script`

- run a script at reboot we write `@reboot command/script`


Let us proceed with that in mind. Your crontab file should now appear as follows:
![[jobcron.png]]
Press ctrl+o to save the crontab file and ctrl+x to exit nano. 

##### Examining the output
We can see that a **hello.txt** file has been created in our desktop folder. When we examine the file's contents, we notice that the current date and time are appended every minute. This is proof that cron is running our script as expected.

![[output.png]]

### Conclusion
You should now be able to schedule tasks on your Linux desktop or server with confidence. You can use the preceding example to create a cronjob that executes a script to automate your repetitive tasks.
Thank you for your time.