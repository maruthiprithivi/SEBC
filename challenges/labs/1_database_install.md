## <center> Challenge 1: Install a MySQL/MariaDB server

* Create the Issue `Install Database`
* Assign the Issue to yourself and label it `started`
* Install MySQL 5.5 or MariaDB 5.5 on the first node listed in `0_setup.md`
  * Use a YUM repository to install the package
  `sudo yum install mariadb-server -y`
  * Copy the repo configuration you use to `challenges/labs/1_my-database-server.repo.md`
  ![MariaDB](maria_db.png)
* On all cluster nodes
  * Install the database client package and JDBC connector jar on all nodes
  ```
  sudo wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.46.tar.gz
  tar -xvf mysql-connector-java-5.1.46.tar.gz
  sudo mkdir -p /usr/share/java/
  sudo cp mysql-connector-java-5.1.46/mysql-connector-java-5.1.46-bin.jar /usr/share/java/mysql-connector-java.jar
  ```
* Start the server and create these databases:
  * `scm`
  * `rman`
  * `hive`
  * `oozie`
  * `hue`
  * `sentry`
* Record the following in `challenges/labs/1_db-server.md`
  * The command `hostname -f` and its output
  `ip-172-31-28-114.ap-southeast-1.compute.internal`
  * The command `mysql -u <user> -p<password> -e "status;"` and its output
  ![Database STATUS](db_status.png)
  * The command `mysql -u <user>  -p<password> -e "show databases;"` and its output
  ![Databases](databases.png)
* Push this work to GitHub
* Label the Issue `review` and assign it to the instructor
