# Flyway
Flyway is a popular open-source database migration tool that helps manage and track database changes, often used in continuous integration and deployment workflows. It supports versioned migrations, allowing teams to apply incremental changes to the database schema sequentially, ensuring consistency and traceability. Flyway also supports undo migrations, which can be invaluable for quickly backing out changes in a production environment if needed. Additionally, it integrates seamlessly with build tools like Maven, Gradle, and others, facilitating automation in development pipelines and reducing the risk of human error during database changes.

## Exercies

### Set up
Install Flywat CLI or use the Docker wrapped Flyway CLI (`redgate/flyway`)
Start up a database (we are going to use Docker to reduce OS overhead)
```
$ docker run --name mysql -e MYSQL_USER=flyway -e MYSQL_PASSWORD=123456 -e MYSQL_DATABASE=example -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:8.1
```
Create a Flyway config directory
```
$ mkdir -p ~/flyway/config
```
Get the IP of the mysql container
```
$ docker inspect mysql | grep IPAddress
```
Create a file there named `flyway.conf`
```
flyway.driver=com.mysql.jdbc.Driver
flyway.url=jdbc:mysql://<<IP address of the mysql container>>:3306/example?autoreconnect=true&allowPublicKeyRetrieval=true
flyway.user=flyway
flyway.password=123456
flyway.cleanDisabled=false
```
Create a migrations directory
```
$ mkdir -p ~/flyway/migrations
```
Create a database file directory
```
$ mkdir -p ~/flyway/db
```

### Create a migration
Create a file in the migrations direcory named `V0__Create_person_table.sql`
```
create table PERSON (
    ID int not null,
    NAME varchar(100) not null
);
```
Run the migration
```
$ docker run --rm -v "{absolute path to folder to store SQLite db file}:/flyway/db" -v "{absolute path to folder containing sql migrations}:/flyway/sql" -v "{absolute path to folder containing conf file}:/flyway/conf" redgate/flyway migrate
```

### Verify the migration was successful
Run the following command
```
$ docker run --rm -v "{absolute path to folder to store SQLite db file}:/flyway/db" -v "{absolute path to folder containing sql migrations}:/flyway/sql" -v "{absolute path to folder containing conf file}:/flyway/conf" redgate/flyway info
```

### Create a new migration
Create a new migration file named `V1__create_email.sql`
```
create table email (
  email_id          int not null auto_increment primary key,
  email_address     varchar(100),
  email_type        char(1) not null,
  person_id         int not null
);
```
Run the new migration
```
$ docker run --rm -v "{absolute path to folder to store SQLite db file}:/flyway/db" -v "{absolute path to folder containing sql migrations}:/flyway/sql" -v "{absolute path to folder containing conf file}:/flyway/conf" redgate/flyway migrate
```

### Clean up the database
You can remove all database objects with the `clean` command
```
$ docker run --rm -v "{absolute path to folder to store SQLite db file}:/flyway/db" -v "{absolute path to folder containing sql migrations}:/flyway/sql" -v "{absolute path to folder containing conf file}:/flyway/conf" redgate/flyway clean
```
You can then apply all migrations with the `migrate` command

### Validate migrations
You can validate that your local files correspond to the run migrations
```
$ docker run --rm -v "{absolute path to folder to store SQLite db file}:/flyway/db" -v "{absolute path to folder containing sql migrations}:/flyway/sql" -v "{absolute path to folder containing conf file}:/flyway/conf" redgate/flyway validate
```

### Baseline
If you want to introduce Flyway to an already existing database with data, you can create a baseline and add newer migarations 
```
$ docker run --rm -v "{absolute path to folder to store SQLite db file}:/flyway/db" -v "{absolute path to folder containing sql migrations}:/flyway/sql" -v "{absolute path to folder containing conf file}:/flyway/conf" redgate/flyway baseline
```

## Further reading
- [Flyway Docs](https://documentation.red-gate.com/fd)
