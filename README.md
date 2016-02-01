# dsantiago/docker-magento-1.9.2.3

A idéia deste repositório é rodar todo um ambiente magento com apenas um comando. A base de dados é persistida localmente na pasta `.mysqldata` (com uma configuração extremamente inicial), logo o repositório tem tamanho maior que o comum.


## Ferramentas utilizadas
* **Front:** 
  * **Nginx** 
  * **PHP 5.6**
  * **PHP5-FPM**
  * **HHVM**
  * **XDebug (Já Ativo)**

* **Mysql 5.6:**

* **Redis**


## Utilizando
* Rode os comandos:
```bash
    >docker-compose up -d  #Roda o compose em modo daemon
    >docker ps  #Verificamos se os 3 containers estão rodando...
```
Isso irá montar todo seu ambiente, expor as portas e shard nas pastas (natureza de persistir os dados do banco localmente)

* A url padrão é a seguinte `http://ds.magento.com.br/` para o **frontend** e `http://ds.magento.com.br/admin` para o **backend**. Será necessários adicionar ao seu `/etc/hosts` esta url. (Como uso mac, que infelizmente utiliza-se de uma VM para rodar o docker aponto para o ip da mesma, geralmente 192.168.99.100)

* A conexão com a com o banco de dados, junto aos dados de conexão, consta em `www/app/etc/local.xml` (confira)

* Os acessos do admin são usuário `admin` e senha `docker123`


## Dicas
* Caso precise verificar algum container isoladamente faça o seguinte:

```bash
>docker ps  #Para verificar os containers em execução

CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                                                              NAMES
ebe9c5f42db4        dockermagentocommunity_front   "/usr/bin/supervisord"   About an hour ago   Up About an hour    0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp, 0.0.0.0:9000->9000/tcp   dockermagentocommunity_front_1
8b17a6c2cffb        mysql:5.6                      "/localdb-run.sh"        About an hour ago   Up About an hour    0.0.0.0:3306->3306/tcp                                             dockermagentocommunity_mysql_1
8895af23c10b        redis                          "/entrypoint.sh redis"   About an hour ago   Up About an hour    0.0.0.0:6379->6379/tcp                                             dockermagentocommunity_redis_1

>docker exec -it 8b17a6c2cffb /bin/bash  # Por exemplo aqui rodamos o container de mysql a partir de sua hash para acessar verificar algum dados
```
* Para stopar os containers só fazer o seguinte comando:

```bash
>docker-compose stop
```

![alt text](https://media.giphy.com/media/zsdlritBT7QhW/giphy.gif "Muito torço por você com o docker amiguinhos :)")
