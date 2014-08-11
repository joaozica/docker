Docker Lamp
- Supervisor - ok
- SSH - ok
- Apache - ok
- Mysql - ok
- PHP - ok
- Phpmyadmin - ok

Run container

```
docker run -d --name lamp-full --dns 8.8.8.8 -p 49160:22 -p 49161:80 -p 49162:3306 -v /diretorio_project:/var/www lamp-full
```