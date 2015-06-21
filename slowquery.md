#MySQL’de SlowQuery Nasıl bulunur

`/etc/mysql/my.cnf` içinde

```
[mysqld]
long_query_time         = 1
log-slow-queries        = /var/log/mysql/mysql-slow.log
```

yapılır sonra mysql reload edilir (`service mysql reload`) ardından `tail -f /var/log/mysql/mysql-slow.log`
veya
mysql’in bunun için özel bir toolu var `mysqldumpslow` direkt konsoldan `$ mysqldumpslow -s c -t 10` çağırarak bu logu parse eden önünüze koyan bir komutla işinizi görebilirsiniz.

eğer canlı bir sistemde bu işi takip etmeniz gerekiyorsa burada tecrübe çalışacak.
`mysql -u root -p` yaptıktan sonra `use databaseismi` ardından `SHOW PROCESSLIST \G;` ile querylerden sürekli önünüze gelenleri deneyerek querylerin ne kadar sürede geldiğini izleyeceksiniz.

Bu query’i bulduktan sonraki diğer adımınız başına `explain` veye `desc` koyarak nedeni anlamalısınız. Eğer bir alanla ilgili problem verinin çok olmasıysa index koyarak bunu çözebilirsiniz.
