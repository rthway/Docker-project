You can easily make your  [nextcloud](https://nextcloud.com/) system at home using a few easy and simple steps. NextCloud is an open-source cloud-making platform with all the features like google cloud and Microsoft One Drive. Just take the docker to compose code and execute it with simple commands. And your nextcloud is ready to rock.

```
services:
  nextcloud:
    image: nextcloud
    ports:
      - 8080:80
    volumes:
      - nextcloud:/var/www/html
    environment:
      - MYSQL_HOST=database
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=nextcloud
      - MYSQL_DATABASE=nextcloud
    depends_on:
      - database

  database:
    image: mariadb
    environment:
      - MYSQL_ROOT_PASSWORD=rootpassword
      - MYSQL_USER=nextcloud
      - MYSQL_PASSWORD=nextcloud
      - MYSQL_DATABASE=nextcloud
    volumes:
      - database:/var/lib/mysql

volumes:
  nextcloud:
  database:
```

To use this Docker Compose file, save it to a file (e.g.,  `docker-compose.yml`) and run the following command:

```
docker-compose up
```