<h1 align="center">my-linux-projects</h1>
<h1 align="center">Hi 👋, I'm Arthur Duarte</h1>
<h3 align="center">My private TUX projects.</h3>


## Information about the version 1.0

```
Version 1.0
* SSH server already instaled and configured
* Creation of the service to monitor one/(or more than one) service(s) on the system
```

The project is composed by two scripts, building a 'systemd service' in order to monitor the ssh-service, ensuring that the SSH Server is always ON, avoiding interruptions of remote connections.
The service is called "noc-mon.service" and calls the script "NOC-MON.sh" .



### Working Screens


[Services running before action] 
<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver1.0-simple-service/noc-mon01.JPG"></p>

[Services running after action (SSH Service manually stopped), automatic restart] 
<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver1.0-simple-service/noc-mon02.JPG"></p>

[Services running (ssh.service with new PID)] 
<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver1.0-simple-service/noc-mon03.JPG"></p>

[LOG file] 
<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver1.0-simple-service/noc-mon04.JPG"></p>