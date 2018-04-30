# ansible-confluence

Installs a confluence server as docker container.
This role is only tested on ubuntu 16.04.

## System requirements

* Docker
* docker-compose
* Systemd

## Role requirements

* python-docker package

## Tasks

* Build java docker image locally
* Build docker image locally
* Create volume paths for docker container
* Create docker-compose file
* Setup systemd unit file
* Start/Restart service

## Role parameters

| Variable      | Type | Mandatory? | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| version       | text | no         | 5.10.9  | Confluence version    |
| volumes.data  | text   | no       | <empty>  | Local path to confluence data volume |
| volumes.backups | text | no | <empty> | Local path to confluence backup volume      |
| volumes.database | text | no | <empty> | Local path to database data volume         |
| publish.port     | text | no | <empty> | Port to be published                       |
| publish.interface | text | no | 0.0.0.0 | Interface to be published                 |
| database.user     | text | no | <empty> | Database connection user name             |
| database.password | text | no | <empty> | Database connection password              |

## Usage

### requirements.yml

```
- name: install-docker-confluence
  src: git@github.com:flandiGT/ansible-docker-confluence.git
  scm: git
```

### Example Playbook

Usage (without parameters):

    - hosts: servers
      roles:
         - { role: install-docker-confluence }

Usage (with parameters):

    - hosts: servers
      roles:
      - role: install-docker-confluence
        version: 5.10.9
        volumes:
          confluence:
            data: /srv/docker/confluence/data
            backups: /srv/docker/confluence/backups
          database: /srv/docker/confluence/database
        publish:
          port: 8090
          interface: 0.0.0.0
        database:
          user: postgres
          password: my_super_secret_password
