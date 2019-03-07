; Example MySQL config file for medium systems.
;
; This is for a large system with memory of 1G-2G where the system runs mainly
; MySQL.
;
; MySQL programs look for option files in a set of
; locations which depend on the deployment platform.
; You can copy this option file to one of those
; locations. For information about these locations, see:
; http://dev.mysql.com/doc/mysql/en/option-files.html
;
; In this file, you can use all long options that a program supports.
; If you want to know which options a program supports, run the program
; with the "--help" option.

; The following options will be passed to all MySQL clients
[client]
;password = your_password
port = 3306
socket = /tmp/mysql.sock

; Here follows entries for some specific programs

; The MySQL server
[wampmysqld64]
;skip-grant-tables
default_authentication_plugin=mysql_native_password
port = 3306
socket = /tmp/mysql.sock
key_buffer_size = 256M
max_allowed_packet = 1M

;Added to reduce memory used (minimum is 400)
table_definition_cache = 600

sort_buffer_size = 2M
net_buffer_length = 8K
read_buffer_size = 2M
read_rnd_buffer_size = 2M
myisam_sort_buffer_size = 64M
;Path to mysql install directory
basedir="c:/wamp64/bin/mysql/mysql5.7.24"
log-error="c:/wamp64/logs/mysql.log"
;Verbosity Value  1 Errors only, 2  Errors and warnings , 3 Errors, warnings, and notes
log_error_verbosity=2
;Path to data directory
datadir="c:/wamp64/bin/mysql/mysql5.7.24/data"

;Path to the language
;See Documentation:
; http://dev.mysql.com/doc/refman/5.7/en/error-message-language.html
lc-messages-dir="c:/wamp64/bin/mysql/mysql5.7.24/share"
lc-messages=en_US

; The default storage engine that will be used when create new tables
default-storage-engine=MYISAM
; New for MySQL 5.6 default_tmp_storage_engine if skip-innodb enable
; default_tmp_storage_engine=MYISAM

;To avoid warning messages
secure_file_priv="c:/wamp64/tmp"
skip-ssl

explicit_defaults_for_timestamp=true

; Set the SQL mode to strict
;sql-mode=""
sql-mode="STRICT_ALL_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_ZERO_DATE,NO_ZERO_IN_DATE,NO_AUTO_CREATE_USER"

; Don't listen on a TCP/IP port at all. This can be a security enhancement,
; if all processes that need to connect to mysqld run on the same host.
; All interaction with mysqld must be made via Unix sockets or named pipes.
; Note that using this option without enabling named pipes on Windows
; (via the "enable-named-pipe" option) will render mysqld useless!
;
;skip-networking

; Disable Federated by default
skip-federated

; Replication Master Server (default)
; binary logging is required for replication
;log-bin=mysql-bin

; binary logging format - mixed recommended
;binlog_format=mixed

; required unique id between 1 and 2^32 - 1
; defaults to 1 if master-host is not set
; but will not function as a master if omitted
server-id = 1

; Replication Slave (comment out master section to use this)

; New for MySQL 5.6 if no slave
skip-slave-start

;
; To configure this host as a replication slave, you can choose between
; two methods :
;
; 1) Use the CHANGE MASTER TO command (fully described in our manual) -
;    the syntax is:
;
;    CHANGE MASTER TO MASTER_HOST=<host>, MASTER_PORT=<port>,
;    MASTER_USER=<user>, MASTER_PASSWORD=<password> ;
;
;    where you replace <host>, <user>, <password> by quoted strings and
;    <port> by the master's port number (3306 by default).
;
;    Example:
;
;    CHANGE MASTER TO MASTER_HOST='125.564.12.1', MASTER_PORT=3306,
;    MASTER_USER='joe', MASTER_PASSWORD='secret';
;
; OR
;
; 2) Set the variables below. However, in case you choose this method, then
;    start replication for the first time (even unsuccessfully, for example
;    if you mistyped the password in master-password and the slave fails to
;    connect), the slave will create a master.info file, and any later
;    change in this file to the variables' values below will be ignored and
;    overridden by the content of the master.info file, unless you shutdown
;    the slave server, delete master.info and restart the slaver server.
;    For that reason, you may want to leave the lines below untouched
;    (commented) and instead use CHANGE MASTER TO (see above)
;
; required unique id between 2 and 2^32 - 1
; (and different from the master)
; defaults to 2 if master-host is set
; but will not function as a slave if omitted
;server-id       = 2
;
; The replication master for this slave - required
;master-host     =   <hostname>
;
; The username the slave will use for authentication when connecting
; to the master - required
;master-user     =   <username>
;
; The password the slave will authenticate with when connecting to
; the master - required
;master-password =   <password>
;
; The port the master is listening on.
; optional - defaults to 3306
;master-port     =  <port>
;
; binary logging - not required for slaves, but recommended
;log-bin=mysql-bin

; Point the following paths to different dedicated disks
;tmpdir   = /tmp/
;log-update   = /path-to-dedicated-directory/hostname

; The InnoDB tablespace encryption feature relies on the keyring_file
; plugin for encryption key management, and the keyring_file plugin
; must be loaded prior to storage engine initialization to facilitate
; InnoDB recovery for encrypted tables. If you do not want to load the
; keyring_file plugin at server startup, specify an empty string.
early-plugin-load=""

;innodb_data_home_dir = C:/mysql/data/
innodb_data_file_path = ibdata1:12M:autoextend
;innodb_log_group_home_dir = C:/mysql/data/
;innodb_log_arch_dir = C:/mysql/data/
; You can set .._buffer_pool_size up to 50 - 80 %
; of RAM but beware of setting memory usage too high
innodb_buffer_pool_size = 256M
; Set .._log_file_size to 25 % of buffer pool size
innodb_log_file_size = 256M
innodb_log_buffer_size = 8M
innodb_flush_log_at_trx_commit = 1
innodb_lock_wait_timeout = 50
innodb_flush_method=normal

[mysqldump]
quick
max_allowed_packet = 16M

[mysql]
no-auto-rehash
; Remove the next comment character if you are not familiar with SQL
;safe-updates

[isamchk]
key_buffer_size = 20M
sort_buffer_size = 20M
read_buffer_size = 2M
write_buffer_size = 2M

[myisamchk]
key_buffer_size = 20M
sort_buffer_size_size = 20M
read_buffer_size = 2M
write_buffer_size = 2M

[mysqlhotcopy]
interactive-timeout

[mysqld]
default_authentication_plugin=mysql_native_password
port = 3306
