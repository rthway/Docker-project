## Define the project
### 1. Create an empty project directory.
For example, if you named your directory `my_wordpress`:
` $ mkdir my_wordpress`

### 2. Enter your project directory.
` $ cd my_wordpress`

### 3.Create a `docker-compose.yml` file that starts your `WordPress`.

```
version: '3'

services:
  mysql:
    image: 'mysql:5.7'
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

  wordpress:
    image: wordpress
    depends_on:
      - mysql
    links:
      - 'mysql:mysql'
    ports: 
      - '8080:80'
    restart: always
    environment:
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress

```
### 3. Now build the project
Now, run `$ docker compose up` from your project directory.
This runs docker compose up in detached mode, pulls the needed Docker images, and starts the wordpress and database containers.

### 4. Bring up WordPress in a web browser
At this point, WordPress should be running on port `8080` which we define on `docker-compose.yml`

**Final Result:**

![Image description](https://www-goglides-dev.s3.amazonaws.com/uploads/articles/hbog4cwmuheb2x2pl3xi.png)
