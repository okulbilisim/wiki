# MySQL’de SlowQuery Nasıl Bulunur?

`/etc/mysql/my.cnf` dosyasına
```
[mysqld]
long_query_time         = 1
log-slow-queries        = /var/log/mysql/mysql-slow.log
```
satırlarını ekleyin ve ardından MySQL reload edin (`# service mysql reload` ile). Sonrasında `tail -f /var/log/mysql/mysql-slow.log` komutunu kullanarak ya da MySQL’in bu işe özel aracı olan `mysqldumpslow`u komut satırında `$ mysqldumpslow -s c -t 10`' şeklinde çalıştırarak, veyahut logu parse edip önünüze koyan herhangi bir komutla işinizi görebilirsiniz.

Eğer canlı bir sistemde bu işi takip etmeniz gerekiyorsa burada tecrübeniz konuşmalı. `$ mysql -u root -p` ile giriş yaptıktan sonra `use database_ismi` ile veritabanınızı seçip, ardından `SHOW PROCESSLIST \G;` komutu ile sorgulardan sürekli önünüze gelenleri deneyerek sorguların ne kadar sürede çalıştığını izlemelisiniz.

Bu sorguyu bulduktan sonraki diğer adımınız, sorgunun başına `explain` veye `desc` koyarak sorunu teşis etmek olmalı. Eğer bir alanla ilgili problem verinin çok olmasıysa, index kullanarak bu problemi çözebilirsiniz.
