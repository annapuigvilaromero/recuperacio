# Dades
url = http://127.0.0.1:3000/
x-token = C0UsWlYxXrMx81TKN2Eq
# Routes API
~~~
    GET      /api/v1/alumnes
    GET      /api/v1/alumne/:id
    POST     /api/v1/alumne
    PUT      /api/v1/alumne/:id
    DELETE   /api/v1/alumne/:id
    GET      /api/v1/assignatures
    GET      /api/v1/assignatura/:id
    POST     /api/v1/assignatura
    PUT      /api/v1/assignatura/:id
    DELETE   /api/v1/assignatura/:id
    POST     /api/v1/nota
    POST     /api/v1/vincular
~~~

# Deploy over Centos07
### Install
    yum update
    yum install mariadb
### Configure mysql
~~~
nano /etc/my.cnf
>bind-address = 0.0.0.0
firewall-cmd --zone=public --add-service=mysql --permanent  
firewall-cmd --reload  
systemctl enable mariadb  
systemctl start mariadb  
mysql_secure_installation  
~~~
### MySQL Database (podeu fer-ho amb el Workbench)
~~~

mysql -u root -p  
CREATE DATABASE nom_base_dades;  
CREATE USER 'nom'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'nom_usuari'@'%';    
FLUSH PRIVILEGES;  
~~~
### Lanch API!
~~~
npm install  
npm update  
cp config/config.example.json config/config.json  
edit config/config.json  

    "development": {  
    "username": "xxxxxxxxx",  
    "password": "xxxxxxxxx",   
    "database": "xxxxxxxxxxx",  
    "host": "xxxxxxxxxxx",  
    "dialect": "mysql"  
    },  

.\node_modules\.bin\sequelize db:create
node node_modules\sequelize-auto-migrations\bin\runmigration.js  
npm start  
~~~
# Altres notes :: DEV ::
### Per si ens carreguem la base de dades...
> node node_modules/.bin/sequelize db:drop  
> node ./node_modules/.bin/sequelize db:create  
> node ./node_modules/sequelize-auto-migrations/bin/runmigration.js  
### Apunts varis
#### autoreload
> node node_modules/nodemon/bin/nodemon.js bin/www  
#### Sequelize-auto-migrations
> node ./node_modules/sequelize-auto-migrations/bin/makemigration.js --name Init  
> node ./node_modules/sequelize-auto-migrations/bin/runmigration.js  