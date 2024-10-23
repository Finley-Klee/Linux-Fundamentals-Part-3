# Linux-Fundamentals-Part-3

<h2>Description</h2>
This is the last part of 3 in the Linux fundamentals series on TryHackMe. Building on the skills in the last two rooms, this room introduced useful utilites and applications as well as automation, package management, and service/application logging.

<h2>Utilities Used</h2>

- <b>Linux Terminal</b> 
- <b>Nano text editor</b>

<h2>Environments Used </h2>

- <b>Linux Ubuntu</b>

<h2>Project walk-through:</h2>

- <b>Terminal Text Editors</b>
<p>In this first task, I read through some basic information about the Nano text editor, then opened the task 3 file located in tryhackme's home directory to find the flag.</p>
<br>
<p align="center">I used the list command "ls" to confirm for myself that I was in the correct directory and that the file was there. Then I used the command "nano" and the file name "task 3" to open the file in the text editor.<br/>
  <img src="https://github.com/user-attachments/assets/1d00e557-7ff4-40f7-bf1d-73dbad16f038" height="80%" width="80%" alt="navy blue background with white text. The top line reads tryhackme@linux3:~$ ls, the second line reads task 3, the next line reads tryhackme@linux3:~$ nano task3, and the last line has the tryhackme@linux3:~$ followed by the cursor."/>
  <br />
  <br />
  This opened the file in nano so that I could see the entire contents more easily than in the terminal. I found the flag, and it's THM{TEXT_EDITORS}<br />
  <img src="https://github.com/user-attachments/assets/70c6af0f-91b4-477f-a957-4d942ba9937f" height="80%" width="80%" alt="a window with a gray banner at the top and a navy blue background with white text. At the top of the window in the gray banner it says GNU Nano 4.8 on the left hand side, and in the middle it says task 3. Then below the banner in the main window it says THM{TEXT_EDITORS} at the top. Down at the bottom are the command options. In the center, the first line says [ Read 1 line ]. This is followed by two lines of 5 options each with the control symbol and a letter and then the name of the option. The first line from left to right reads: control G get help, control O write out, control K cut text, control J justify. The second line from left to right reads: control X exit, control R read file, control \ replace, control U paste text, and control T to spell."/>
</p>
<br />
<br />

- <b>General/Useful Utilities</b>
<p>In the next section I learned about the wget command, which is used to download a file over http, and the scp command, which provides a way to securely transfer files over the SSH protocol. I also learned that Ubuntu linux machines can use the "HTTPServer" module in Python3 to quickly and easily host files that others can download.</p>
<br>
<p align="center">To practice using these commands, I opened two terminal windows. In the top terminal window I have used SSH to connect to the linux3 machine, and the bottom terminal window is the attack box. On the linux3 machine I used the HTTP Server module from the home dirctory to give access to the file there, and then in the attack box terminal I used wget to download the flag.<br/>
  <img src="https://github.com/user-attachments/assets/f9f76bfb-e36c-48aa-810b-07c7e435c2db" height="80%" width="80%" alt="two terminal windows in linux with dark blue backgrounds and lime green and white text. The top window shows the command python3 -m http.server followed by the confirmation that it was successful and lastly a log of the attack box getting the flag.txt file. The bottom window shows the use of the wget command with the ip address and name of the file followed by confirmation of the file downloading."/>
  <br />
  <br />
Then, I wanted to confirm that the file was in the directory, so first I used the ls command because I didn't notice the "." before the word flag in the file name indicating that it's a hidden file, but when I didn't see the file in the list I realized my mistake and appended the -a flag to show the hidden files and directories and confirmed that the flag file was there. <br />
  <img src="https://github.com/user-attachments/assets/65d7f534-3654-46d9-be08-7335fc8cf904" height="80%" width="80%" alt="a linux terminal window with dark blue background and lime green, light blue and white text. The first command shows ls with a limited number of responses and the .flag.txt file is not seen. After that the ls -a command is shows with a red rectangle around it and the .flag.txt file is visible and also highlighted by a red rectangle."/>
  <br />
  <br />
 After that, I simply used the cat command to print the flag, which is THM{WGET_WEBSERVER} <br />
  <img src="https://github.com/user-attachments/assets/9ae4e91d-d8b8-4052-aa46-c3c1640090be" height="80%" width="80%" alt="A linux terminal window with dark blue background and lime green and white text. The top line shows the command cat .flag.txt and the next line shows the flag highlighted in white with contrasting dark font. The flag reads THM curly brace WGET underscore WEBSERVER curl brace"/>
</p>

- <b>Processes 101</b>
<p>In this section I learned what processes are, how to view a list of the processes running as our user session using the ps command, and that in order to see the processes running from other users or that don't run from a session you need to use ps aux.</p>

<p>Then I read that you can manage start and stop those processes using different commands. The kill command (used with the associated process ID) will terminate a process, the SIGTERM signal kills the process, but allows it to do some cleanup tasks beforehand, the SIGKILL signal kills the process and doesn't do any cleanup after the fact, and if you want to just stop or suspend a process you can use the SIGSTOP signal.</p>

<p>Next, I read about starting processes and services upon booting a system using the systemctl command. The systemctl command accepts an option like start, stop, enable, or disable and a service. The example given was launching an apache2 webserver  on boot using the command systemctl start apache2. </p>

<p>Lastly, I read about how to change the state of a process between the foreground and background using the & operator or Ctrl + Z to send things to the background, and then using the fg command to bring them back to the foreground.</p>
<br>
<p align="center">Since this section was quite reading focused, the tasks mainly were answering questions. The first answer comes from the overview of processes. We know that the process ID increments in the order the process starts, so the next process after 300 would have a process ID (PID) of 301.<br/>
<p align="center">Then, if we wanted to cleanly kill a process, we would want to use the SIGTERM signal, because, according to the reading, this kills the process but allows it to do some cleanup tasks beforehand.<br/>
  <img src="https://github.com/user-attachments/assets/54f814a4-a8d8-43a1-acd0-13db2d77cdea" height="80%" width="80%" alt="white background with questions in black text, gray rounded corner rectangles with the answers, and a lime green button to the right with a check mark and correct answer. The top question reads If we were to launch a process where the previous ID was 300, what would the ID of this new process be? and the answer reads 301. The second question reads If we wanted to cleanly kill a process, what signal would we send it? and the answer reads SIGTERM."/>
  <br />
  <br />
  The next questions asks me to locate a process that is running the deployed machine that provides me with a flag, so I ran the "ps aux" command to see a list of all the processes running on the machine. Then I scrolled through the list looking for the TryHackMe flag format, and I found a process running from root with a PID of 481 that had the flag THM{PROCESSES}.<br />
  <img src="https://github.com/user-attachments/assets/bf9b2a8c-0db7-4b34-a537-9abfff5de762" height="80%" width="80%" alt="dark blue background with white text. The top line shows the command ps aux followed by many lines of all the processes running."/>
  <img src="https://github.com/user-attachments/assets/d2d85e51-f765-495d-9862-cdb7b8b2d64f" height="80%" width="80%" alt="dark blue background with white text and the colors inverted for highlight. The list of running processes is shown with a single line highlighted. To the far right in the command column the text reads THM curly brace open processes curly brace close."/>
  <br />
  <br />
  The last three questions in this section all check for understanding of the reading. The first asks "What command would we use to stop the service 'myservice'?" For this we would start with the "systemctl" command, which allows us to interact with the systemd process/daemon. Then we would pass it the "stop" option followed by the name of the service, which in this case is "myservice". <br />
  Then, if we wanted to restart the same service on the boot-up of the system, we would use the same basic command "systemctl" but we would use the "enable" option followed by the service name. <br />
  Lastly, the command to bring a previously backgrounded process to the foreground is "fg". <br />
  <img src="https://github.com/user-attachments/assets/c449426e-45fd-4caf-a7e1-6bc2f27a782d" height="80%" width="80%" alt="white background with questions in black text, gray rounded corner rectangles with the answers, and a lime green button to the right with a check mark and correct answer."/>
</p>

- <b>Maintaining Your System: Automation</b>
<p>This section introduces us to crontabs, which allow us to schedule tasks like opening programs on boot or backing up files.</p>
<br>
<p align="center">I learned that in order to successfully schedule a task in crontabs, you must put in information for 6 values, but you can use the asterisk as a wildcard. So, for example, if you wanted to back up "cmnatic"'s "Documents" every 12 hours, you would write that like this: 0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/ <br/>
  <img src="https://github.com/user-attachments/assets/fbcaf8de-d79f-40a5-9b89-92bd0c8eeaa5" height="80%" width="80%" alt="A white table explaining the different values in order for crontabs, including minutes, hours, day of the month, month of the year, day of the week, and the command to execute."/>
  <br />
  <br />
 To answer the question in this task, I used the command crontab -e to edit the crontab file in nano. I scrolled to the bottom of the file and found the crontab running on the deployed instance, which runs on reboot.<br />
  <img src="https://github.com/user-attachments/assets/1ca2a1a6-55f7-48a8-8765-26666fe43a8f" height="80%" width="80%" alt="a nano text editor window with crontab information. The last line is highlighted and reads @reboot /var/opt/processes.sh"/>
</p>

- <b>Maintaining Your System: Package Management</b>
<p>The package management section does not have any activities, so I will summarize what I read.</p>
<br>
<p align="center">Step One: <br/>
  <img src="" height="80%" width="80%" alt="image one"/>
  <br />
  <br />
  Step Two: <br />
  <img src="" height="80%" width="80%" alt="image two"/>
  <br />
  <br />
  Step Three: <br />
  <img src="" height="80%" width="80%" alt="image three"/>
   <br />
  <br />
  Step Four: <br />
  <img src="" height="80%" width="80%" alt="image four"/>
   <br />
  <br />
  Step Five: <br />
  <img src="" height="80%" width="80%" alt="image five"/>
</p>

- <b>Maintaining Your System: Logs</b>
<p>Description</p>
<br>
<p align="center">Step One: <br/>
  <img src="" height="80%" width="80%" alt="image one"/>
  <br />
  <br />
  Step Two: <br />
  <img src="" height="80%" width="80%" alt="image two"/>
  <br />
  <br />
  Step Three: <br />
  <img src="" height="80%" width="80%" alt="image three"/>
   <br />
  <br />
  Step Four: <br />
  <img src="" height="80%" width="80%" alt="image four"/>
   <br />
  <br />
  Step Five: <br />
  <img src="" height="80%" width="80%" alt="image five"/>
</p>

