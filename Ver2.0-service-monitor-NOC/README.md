<h1 align="center">my-linux-projects</h1>
<h1 align="center">Hi 👋, I'm Arthur Duarte</h1>
<h3 align="center">My private TUX projects.</h3>


## Information about the version 2.0

```
* I created this aditional service due the necessity of;
a. Keep my raspberry-pi always connected to the internet
b. Find it´s IP address to easily connet
```

The project is composed by two scripts, building a 'systemd service' in order to restart the
'systemd-networkd.service' responsible for the interfaces (physical interfaces), 
ensuring that the IP addressing will be always ON, avoiding interruptions of remote connections.
The service is called "noc-mon-interface.service" and calls the script "NOC-MON-INTERFACE.sh" .



### Working Screens


[Services running before action] 
<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver2.0-service-monitor-NOC/noc-mon-interface_service01.JPG"></p>

<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver2.0-service-monitor-NOC/systemd-networkd_service01.JPG"></p>

[Testing]
<p float="left"><img src="https://github.com/arthurddduarte86/my-linux-projects/blob/main/Ver2.0-service-monitor-NOC/testing.JPG"></p>



### Codes

Code of: Service (noc-mon-interface.service)
```

[Unit]
Description=Service for: Keep physical interface and conn service always ON
After=systemd-networkd.service

[Service]
Type=simple
ExecStart=/usr/local/bin/NOC-MON-INTERFACE.sh
Restart=always
RestartSec=30

[Install]
WantedBy=multi-user.target

```

Code of: Script 'NOC-MON-INTERFACE.sh' (executor)
```
#!/bin/bash


while true; do

        # Verifica o status do serviço systemd-networkd.service
        status=$(systemctl is-active systemd-networkd.service)

        # Verifica se o status é diferente de "active"
        if [ "$status" != "active" ]; then
            echo "O serviço systemd-networkd.service não está ativo. Reiniciando o serviço..."
            systemctl restart systemd-networkd.service
            echo "Serviço reiniciado."
        fi
		# timer pra esperar 1segundo
        sleep 1
done
```
