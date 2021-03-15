# 項目
 * my.ini 
 * ログ

## my.ini
    MySQLの設定ファイル
### innodb_buffer_pool_size
    データとインデックスを、メモリ上にキャッシュする領域。搭載メモリの80%が目安。

### innodb_log_file_size
    InnoDBの更新ログを記録するディスク上のファイル。
    innodb_log_fileがいっぱいになると、メモリ上のinnodb_buffer_poolのデータのうち、更新された部分のデータをディスク上のInnoDBのデータファイルに書き出す。

### max_connections
    許可する接続数の最大値。これを来れるとToo Many Connectionsエラーに。

### innodb_lock_wait_timeout
    行ロックが解除されるまでInnoDBトランザクションが待機する秒数。デフォルトは50秒。
    これを超えるとタイムアウトして、次のエラーがerror.logに記録される。
    ```
    ERROR 1205 (HY000): Lock wait timeout exceeded; try restarting transaction
    ```

    デッドロックは InnoDB によってすぐに検出され、デッドロックになったトランザクションのいずれかがロールバックされるため、デッドロックにはロック待機のタイムアウト値が適用されない。

### long_query_time
    これを超えるクエリがslow.logに記録される。

### sort_buffer_size
    ORDER BY やGROUP BYに使われるメモリ上の領域。スレッドバッファ。

### read_rnd_buffer_size
    ソート後にレコードを読むときに使われるメモリ上の領域。スレッドバッファ。
    ディスクI/Oが減るのでORDER BYの性能向上が期待できる。

### join_buffer_size
    インデックスを使わないテーブル結合の時に使われる。スレッドバッファ。

### read_buffer_size
    インデックスを使わないテーブルスキャンの時に使われる。スレッドバッファ。

### key_buffer_size
    MyISAMのインデックスをキャッシュ。MyISAMをあまり使ってないなら小さくするのもアリ。

### thread_cache_size
    スレッドをいくつキャッシュしておくか。  

[DSAS開発者の部屋:5分でできる、MySQLのメモリ関係のチューニング！](http://dsas.blog.klab.org/archives/50860867.html)
[[ThinkIT] 第3回：max_connectionsとthread_cacheのチューニングを行う (2/3)](https://thinkit.co.jp/cert/article/0707/2/3/2.htm)
[MySQL :: MySQL 5.6 リファレンスマニュアル :: 14.12 InnoDB の起動オプションおよびシステム変数](https://dev.mysql.com/doc/refman/5.6/ja/innodb-parameters.html#sysvar_innodb_lock_wait_timeout)
[innodb_buffer_pool_sizeのチューニング：どれくらい割り当てる？](https://corporate.inter-edu.com/developper/1373)

## ログ
### error.log
    MySQLの開始/停止等、様々なエラーが記録される。
    ```
    2017-04-23 01:44:11 21935 [ERROR] /path/to/mysql/bin/mysqld: Incorrect key file for table './***/***.MYI'; try to repair it 
    ```

### slow.log
    すべてのロックが解放された後にログに書き込まれるので、ログの順序が実行順と異なることも。  

[MySQL :: MySQL 5.6 リファレンスマニュアル :: 5.2.5 スロークエリーログ](https://dev.mysql.com/doc/refman/5.6/ja/slow-query-log.html)

### クエリログ
#### my.iniに以下を追記  
  ```ini
  general_log = 1
  general_log_file = /path/to/mysql/data/query.log
  ```
### バイナリログ
   レプリケーションの時に使う。
  
### MySQL稼働状況出力プログラム
  ```mysql
  SHOW GLOBAL STATUS;
  SHOW ENGINE INNODB STATUS\G;
  SELECT NOW(); SHOW PROCESSLIST;
  SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS;
  SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS;
  SELECT * FROM INFORMATION_SCHEMA.INNODB_TRX;
  ```

[MySQLのログの種類とログの仕方を調べてみた（実施例） | レンタルサーバー・自宅サーバー設定・構築のヒント](https://server-setting.info/centos/mysql-log-type.html)
