# Commands Docker

1.
```cmd
cd /db
```

2.
```cmd
docker build -t eugene/tp1-db .
```

3.
```cmd
docker network create tp1network
```

4.
```cmd
docker run \
  --name postgres \
  --network tp1network \
  -e POSTGRES_DB=db \
  -e POSTGRES_USER=usr \
  -e POSTGRES_PASSWORD=pwd \
  -p 5432:5432 \
  -v $(pwd)/postgres-data:/var/lib/postgresql/data \
  -d \
  eugene/tp1-db 
```
or
```cmd
docker run --name postgres --network tp1network -e POSTGRES_DB=db -e POSTGRES_USER=usr -e POSTGRES_PASSWORD=pwd -p 5432:5432 -v "$(pwd)/postgres-data:/var/lib/postgresql/data" -d eugene/tp1-db
```

5.
```cmd
docker run \
  -p "8080:8080" \
  --network tp1network \
  --name=adminer \
  -d \
  adminer
```
or 
```
docker run -p "8080:8080" --network tp1network --name=admnier -d adminer
```

6.
Connect to --> http://localhost:8080 <br>
And enter the connection params to "Adminer"
```
sys = PostgresSQl
Serveur = postgres
User = usr
Mdp = pwd
BDD = db
```


