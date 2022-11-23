# Docker-Ansible-Pull
Using Ansible-pull to set up Docker container in my server(s)


```
git clone git@github.com:vichanzo/Docker-Ansible-Pull.git

nano local.yml
```

content of local.yml:
```
- hosts: localhost
  connection: local
  become: true

  tasks:
    - include tasks/containers.yml
```

create tasks/containers.yml:
```
cd ~/Docker-Ansible-Pull
mkdir tasks
cd tasks
nano containers.yml
```

contents of containers.yml:
```
   - name: Install MeTube
     docker_container:
      name: metube
      ports:
       - 8081:8081
      env:
       PUID: "1000"
       PGID: "1000"
       TZ: "America/Los_Angeles"
      restart_policy: unless-stopped
      volumes:
       - '/home/opc/data/yt:/downloads'
      image: alexta69/metube
```

## Running ansible-pull
On a different system you can run the local.yml playbook

```
sudo ansible-pull -U https://github.com/vichanzo/Docker-Ansible-Pull.git
```
