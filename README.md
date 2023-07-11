# docker-oracle
 
Quick Start
Run a new database container (data is removed when the container is removed, but kept throughout container restarts): <br>
docker run -d -p 1521:1521 -e ORACLE_PASSWORD=<your password> gvenzl/oracle-free <br><br>

Run a new persistent database container (data is kept throughout container lifecycles): <br>
docker run -d -p 1521:1521 -e ORACLE_PASSWORD=<your password> -v oracle-volume:/opt/oracle/oradata gvenzl/oracle-free <br><br>

Reset database SYS and SYSTEM passwords: <br>
docker exec <container name|id> resetPassword <your password> <br><br>

How to use this image
Environment variables
Environment variables allow you to customize your container. Note that these variables will only be considered during the database initialization (first container startup).

ORACLE_PASSWORD
This variable is mandatory for the first container startup and specifies the password for the Oracle Database SYS and SYSTEM users.

ORACLE_RANDOM_PASSWORD
This is an optional variable. Set this variable to a non-empty value, like yes, to generate a random initial password for the SYS and SYSTEM users. The generated password will be printed to stdout (ORACLE PASSWORD FOR SYS AND SYSTEM: ...).

ORACLE_DATABASE
This is an optional variable. Set this variable to a non-empty string to create a new pluggable database with the name specified in this variable.
Note: creating a new database will add to the initial container startup time. If you do not want that additional startup time, use the already existing FREEPDB1 database instead.

APP_USER
This is an optional variable. Set this variable to a non-empty string to create a new database schema user with the name specified in this variable. For 18c and onwards, the user will be created in the default FREEPDB1 pluggable database. If ORACLE_DATABASE has been specified, the user will also be created in that pluggable database. This variable requires APP_USER_PASSWORD or APP_USER_PASSWORD_FILE to be specified as well.

APP_USER_PASSWORD
This is an optional variable. Set this variable to a non-empty string to define a password for the database schema user specified by APP_USER. This variable requires APP_USER to be specified as well.
