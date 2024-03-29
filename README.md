**Quando for rodar alguma stack, não esqueça de trocar o dominio**


# Plataformas OpenSources

* __Chatwoot__          (Serviço de suporte via chat)
* __EvolutionAPI__      (whatsapp api)
* __Mautic__            (Serviço de disparo de email)
* __Minio__             (Serviço de Storage, semelhante ao S3)
* __N8N__               (Automação de fluxos, selhante ao make.com) [Modo fila com redis]
* __Portainer__         (Gerenciador visual-interativo para docker)
* __Typebot Viewer__    (Frotend do typebot)
* __Typebot Builder__   (Backend do typebot)
* __Traefik__           (Webserver, utilizado para proxy reverso)


# Banco de dados

* __Mysql__
* __Postgresql__
* __Redis__


## Para o Typebot: 

Necessario criar um database typebot
```
psql -U postgres
create database typebot;
```

## Para o Chatwoot White-Label: 

Necessario rodar as migrates no container da aplicação
(utilize o /ash ou /sh para se conectar)
```
bundle exec rails db:chatwoot_prepare
```

Para "desbloquear" funcionalidades do super admin
Se conecte ao postgres, usando o database correto, execute a instrução
```
psql -U postgres #conecta ao pg
\c chatwoot; # altera database
update installation_configs set locked = false; #atualizar tabela
```


## Para o N8N: 

Necessario **Redis**
Necessario criar um database n8n_queue
```
psql -U postgres
create database n8n_queue;
```

## Para o Mautic 

Necessario **MySql**
Necessario criar um database mautic
```
mysql -u root -p
CREATE DATABASE mautic;
```

## No caso de não possuir docker na maquina

__Guia de Instalação Docker__
```
sudo apt-get update ; apt-get install -y apparmor-utils
hostnamectl set-hostname meuservidor1
```

Altera 
```
127.0.0.1 localhost 
```

para
```
127.0.0.1 meuservidor1
nano /etc/hosts
```

```
curl -fsSL https://get.docker.com | bash
```

Inicia o Docker Swarm
```
docker swarm init
```

Cria uma rede no docker
```
docker network create --driver=overlay minha_rede
```


Sobe o traefik
```
docker stack deploy --prune --resolve-image always -c traefik.yaml traefik
```


Sobe o portainer 
```
docker stack deploy --prune --resolve-image always -c portainer.yaml portainer
```

Agora poderá subir o restante pelo portainer