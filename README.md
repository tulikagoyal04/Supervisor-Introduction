# Supervisor-Introduction
In this repo I'm going to talk about how to run/manage a python script using superviosr.

# Overview of supervisor
Supervisor is a client/server system that allows its users to control a number of processes on UNIX-like operating systems. [For more details](http://supervisord.org/introduction.html)

**Componets of supervvisor...***
**(i)** Supervisord: Server piece of supervisor which responsible for... <br>
    **(a)** starting child program at its own invocation <br>
    **(b)** responding to commands from clients <br>
    **(c)** restarting crashed or exited subprocesses <br>
    **(d)** logging stdout and stderr output of its subprocess <br>
    **(e)** generating and handling events corresponding to points in subprocess lifetimes. <br>
**(ii)** Supervisorctl: command-line client piece of the supervisor which provides a shell-like interface to the features provided by supervisord.

# Installation of supervisor
open terminal and then run the following command <br>
  ```sudo apt-get install supervisor```
  
# Run supervisor
After installing the supervisor, to run it (run the following command in terminal) <br>
  ```sudo supervisord```
  
Before running the above command please make sure you using system python, not anaconda python
(how to check which python you are using--- run ```which python``` or ```which python3``` in terminal and see the output.)

# Some other command to restart, stop and check status of supervisor
```
#Checking the status of supervisor
  sudo service supervisor status
#Staring supervisor
  sudo service supervisor start
#Stopping supervisor
  sudo service supervisor stop
#Restarting supervisor
  sudo service supervisor restart
```
  
# Creating a simple python program
You may create this script earlier also. there is no hard-and-fast rule to create the python script after running the supervisor
I have created a 'demo.py' file i.e. basically print a message after 1 second.

# Configuration
To get supervisor to execute a certain program or script, we can configure it in the ```/etc/supervisor/conf.d/ directory```. As a recommendation, it would be best to keep a single conf file per process.

So to create a configuration file I have sued 'vim'. Just type the following command in terminal

  ```sudo vim /etc/supervisor/conf.d/demo.conf```
  
  (change 'demo' with your conf file name. I have given my conf file name 'demo') <br>
  
after running the above command press i (that will take in insert mode), now you can write your configuration
```
  [program:demo]
  command=python -u demo.py
  directory=/home/my_username
  #where output log will store
  stdout_logfile=/var/log/demo.out.log
  #where error log will store
  stderr_logfile=/var/log/demo.err.log
  redirect_stderr=true
  #if processes should start when supervisor starts
  autostart=true
  #if proceses should restart when they stop while running
  autorestart=true
 ```
  
Now press ```esc``` key and then wrire ```:w``` press ENTER and then write ```:q``` press ENTER.

######Now run the following command
```sudo systemctl restart supervisor.service```

# Next step
To get into supervisorctl, use the following command

  ```sudo supervisorctl```
  
if you are getting ```unix:///tmp/supervisor.sock no such file``` error then try to run supervisorctl with ```-c``` parameter-

```sudo supervisorctl -c /etc/supervisor/supervisord.conf```
  
Now a supervisorctl prompt will open, try to run the following
```
supervisor > reread #Reloads conf files
supervisor > add test_process #Adds a newly created conf file and starts the process
supervisor > status # Checks all status of programs managed by supervisor
```

# Additional 
If you want to see your supervisord.conf file then you can see it here
  ```/etc/supervisor/supervisord.conf```




