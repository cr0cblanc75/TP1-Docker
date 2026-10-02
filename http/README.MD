# DOCKER Commands
```cmd
docker build -t eugene/tp1-front .
```

```cmd
docker run -d --name tp1-front -p 8080:80 eugene/tp1-front
```

```cmd
docker cp tp1-front:/usr/local/apache2/conf/httpd.conf ./httpd.conf
```