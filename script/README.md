# Script

#＃ myrocks_hotbackup
提供innodb目录不在datadir目录下的备份恢复支持
使用方式

###备份
```
./myrocks_hotbackup -uroot -S/var/lib/mysql/tmp/mysql.socket -P3306 --stream=tar --checkpoint_dir=/tmp/backup | ssh 192.168.1.100 'tar -xi -C /backup' -p
```

###恢复
```
# 删除数据目录
/bin/rm -rf /var/lib/mysql/data/mysql/data && /bin/rm -rf /var/lib/mysql/data/mysql/rocksdb/data && /bin/rm -rf /var/lib/mysql/data/mysql/innodb

# 执行恢复
./myrocks_hotbackup --move_back --datadir=/var/lib/mysql/data/mysql/data --innodb_datadir=/var/lib/mysql/data/mysql/innodb/data --innodb_logdir=/var/lib/mysql/data/mysql/innodb/logs --rocksdb_datadir=/var/lib/mysql/data/mysql/rocksdb/data --rocksdb_waldir=/var/lib/mysql/data/mysql/rocksdb/data --backup_dir=/backup
```

修改文件权限并重启服务
```
chown mysql:mysql -R /var/lib/mysql
```
