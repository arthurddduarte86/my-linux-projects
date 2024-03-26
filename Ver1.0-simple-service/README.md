<h1 align="center">my-linux-projects</h1>
<h1 align="center">Hi 👋, I'm Arthur Duarte</h1>
<h3 align="center">My private TUX projects.</h3>


## Information about the version 1.0

```
Version 1.0
* SSH server already instaled and configured
* Creation of the service to monitor one/(or more than one) service(s) on the system
```

The project is composed by two scripts, building a 'systemd service' in order to monitor the ssh-service, 
ensuring that the SSH Server is always ON, avoiding interruptions of remote connections.
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


### Codes

Code of: Service (noc-mon.service)
```

[Unit]
Description=Service for: Keep ssh service always ON
After=ssh.service

[Service]
Type=simple
ExecStart=/usr/local/bin/NOC-MON.sh
Restart=always
RestartSec=30

[Install]
WantedBy=multi-user.target

```

Code of: Script NOC-MON.sh (executor)
```
#!/bin/bash


while true; do

        # Executa o comando systemctl status ssh, filtra as informações relevantes e extrai a primeira palavra após ":"
        status_info=$(systemctl status ssh | grep -E 'Active:|Main PID:' | grep -oP '(?<=: )[^\s]+')

        # Imprime as informações obtidas
        #echo "Status do serviço SSH:"
        #echo "$status_info"

        # Extrai o estado do serviço SSH
        service_status=$(echo "$status_info" | sed -n '1p')

        # Extrai o PID principal do serviço SSH
        main_pid=$(echo "$status_info" | sed -n '2p')


        # Verifica se o estado é diferente de "active"
        if [ "$service_status" != "active" ]; then
            echo "O serviço SSH não está ativo. Enviando sinal SIGTERM para o PID $main_pid..."
            kill -SIGTERM "$main_pid"
            echo "Sinal SIGTERM enviado para o PID $main_pid. Reiniciando o serviço SSH..."
            systemctl restart ssh
            status_info=$(systemctl status ssh | grep -E 'Active:|Main PID:' | grep -oP '(?<=: )[^\s]+')

            #Comando abaixo apenas pra verificar se imprimir o estado atual do servico
            #echo "$status_info" | sed -n '1p'

        fi
        #timer de 5segs
        sleep 5
done
```
