1. MariaDB Installation
    1. Installed using `yum`
    `sudo yum install mariadb-server -y`

    1. Configured using the following
    `sudo /usr/bin/mysql_secure_installation`

    1. Replication setup
        1. On Master
        ```
        mysql -uroot -pcdh1234 -e "GRANT REPLICATION SLAVE ON *.* TO 'root'@'ip-172-31-28-1.ap-southeast-1.compute.internal' IDENTIFIED BY 'cdh1234';"
        mysql -uroot -pcdh1234 -e "GRANT REPLICATION SLAVE ON *.* TO 'root'@'172.31.19.97' IDENTIFIED BY 'cdh1234';"
        # revoke REPLICATION SLAVE ON *.* from 'root'@'ip-172-31-28-1.ap-southeast-1.compute.internal'; #
        mysql -uroot -pcdh1234 -e "SET GLOBAL binlog_format = 'ROW';"
        mysql -uroot -pcdh1234 -e "FLUSH TABLES WITH READ LOCK;"
        mysql -uroot -pcdh1234 -e "show master status;"
        mysql -uroot -pcdh1234 -e "UNLOCK TABLES;"
        ```

        1. On Slave
        ```
        mysql -uroot -pcdh1234 -e "GRANT REPLICATION SLAVE ON *.* TO 'root'@'ip-172-31-28-1.ap-southeast-1.compute.internal' IDENTIFIED BY 'cdh1234';"
        mysql -uroot -pcdh1234 -e "GRANT REPLICATION SLAVE ON *.* TO 'root'@'172.31.19.97' IDENTIFIED BY 'cdh1234';"
        # revoke REPLICATION SLAVE ON *.* from 'root'@'ip-172-31-28-1.ap-southeast-1.compute.internal'; #
        mysql -uroot -pcdh1234 -e "SET GLOBAL binlog_format = 'ROW';"
        mysql -uroot -pcdh1234 -e "FLUSH TABLES WITH READ LOCK;"
        mysql -uroot -pcdh1234 -e "show master status;"
        mysql -uroot -pcdh1234 -e "UNLOCK TABLES;"
        ```

            1. Replication is failing with the following error message
            ```
            MariaDB [(none)]> show slave status \G;
*************************** 1. row ***************************
               Slave_IO_State:
                  Master_Host: ip-172-31-30-141.ap-southeast-1.compute.internal
                  Master_User: root
                  Master_Port: 3306
                Connect_Retry: 60
              Master_Log_File: mysql_binary_log.000005
          Read_Master_Log_Pos: 15285
               Relay_Log_File: mariadb-relay-bin.000004
                Relay_Log_Pos: 4
        Relay_Master_Log_File: mysql_binary_log.000005
             Slave_IO_Running: No
            Slave_SQL_Running: Yes
              Replicate_Do_DB:
          Replicate_Ignore_DB:
           Replicate_Do_Table:
       Replicate_Ignore_Table:
      Replicate_Wild_Do_Table:
  Replicate_Wild_Ignore_Table:
                   Last_Errno: 0
                   Last_Error:
                 Skip_Counter: 0
          Exec_Master_Log_Pos: 15285
              Relay_Log_Space: 245
              Until_Condition: None
               Until_Log_File:
                Until_Log_Pos: 0
           Master_SSL_Allowed: No
           Master_SSL_CA_File:
           Master_SSL_CA_Path:
              Master_SSL_Cert:
            Master_SSL_Cipher:
               Master_SSL_Key:
        Seconds_Behind_Master: NULL
Master_SSL_Verify_Server_Cert: No
                Last_IO_Errno: 1593
                Last_IO_Error: Fatal error: The slave I/O thread stops because master and slave have equal MySQL server ids; these ids must be different for replication to work (or the --replicate-same-server-id option must be used on slave but this does not always make sense; please check the manual before using it).
               Last_SQL_Errno: 0
               Last_SQL_Error:
  Replicate_Ignore_Server_Ids:
             Master_Server_Id: 1
            ```
