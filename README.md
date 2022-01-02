# cybersecurity-uod
This repo contains the artifacts related to cybersecurity course

## Accessing Kibana dashboard
```
http://<ELK.VM.External.IP>:5601/app/kibana
```


## Useful commands
```bash
# check the docker service status 
service docker status

# container status
docker ps -a

# start a container
docker start <container name>

# attack docker container
docker attach <container name>

# run ansible playbook
ansible-playbook ./main.yml
```
