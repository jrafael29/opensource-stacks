**Quando for rodar alguma stack, não esqueça de trocar o dominio**


# Plataformas OpenSources

* __N8N__               (Automação de fluxos, selhante ao make.com)
* __EvolutionAPI__      (whatsapp api)
* __Minio__             (Serviço de Storage, semelhante ao S3)
* __Portainer__         (Gerenciador visual-interativo para docker)
* __Typebot Viewer__    (Frotend do typebot)
* __Typebot Builder__   (Backend do typebot)
* __Traefik__           (Webserver, utilizado para proxy reverso)
* __Chatwoot__          (Serviço de suporte via chat)

# Extra

* __Postgresql__
* __Redis__



For N8N: 

run this: 
```
psql -U postgres
create database n8n_queue;
```



No caso de não possuir docker na maquina:

Instalação Docker
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