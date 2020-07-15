## Usage
This is a Setup for Dockerizing a Laravel App with MySQL Database and NGINX Web Server.

To get started, make sure you have [Docker for Windows/Linux installed] on your system, and then clone this repository.

Copy your Laravel App Files in `laravelSite` folder

Configure your database credentials as given in the sample .env file

Open a terminal and from this cloned respository's root run following commands in order:
1. `docker-compose up -d --build`
2. `docker-compose exec app composer update`or  `docker-compose exec app composer install`
3. `docker-compose exec db bash`
4. `mysql -u root -p`
5. `password`
6. `CREATE USER 'mainuser'@'%' IDENTIFIED BY 'password';`   *If you change the Username and password, Do so in the .env file too*
7. `GRANT ALL ON *.* TO 'mainuser'@'%';`
8. `FLUSH PRIVILEGES;`
9. `exit`
10. `exit`

If you have migration tables and seeds, run `docker-compose exec app php artisan migrate --seed`

Other artisan commands can also be run in the format of `docker-compose exec app php artisan key:generate`

Open up your browser of choice to [http://localhost:4000](http://localhost:4000) and you should see your Laravel app running as intended.

Containers created and their ports (if used) are as follows:

- **nginx** - `:4000`
- **mysql** - `:3310`
- **php** - `:9000`

#Important Things to Know:

The ports given above should not be in use in your computer. If they **are** in use, Change the ports in `docker-compose.yml` file.

Site-Link: http://localhost:4000

## Persistent MySQL Storage
This App has Persistent Data Storage for MySQL such that the volume is mapped as:

```
volumes:
  - ./mysql/data:/var/lib/mysql
```
