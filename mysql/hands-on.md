# 項目
 * mysqlコマンド
 * SQL
 * ハンズオン

## mysqlコマンド
MySQLのユーザーインターフェース。  
シェルからMySQLに命令を送ったり、その結果を受け取ったり。  

### ログイン
  * my.ini を使って、MySQLにログイン
  * my.ini を使わずに、MySQLにログイン  

        -u : ユーザー名  
        -p : パスワード  
        -h : ホスト名 or IPアドレス  
        -P : ポート番号  
        -S : ソケットファイル名  

    [Unixドメインソケットの確認 - Qiita](http://qiita.com/nk_yohn3301/items/7aec184e290940052ed2)

### SQL実行
  * 以下を適当な場所に保存
    ```mysql:query.sql
    SELECT * FROM (スケジュール一覧);
    ```
  * mysqlコマンドで、query.sqlを実行
    ```zsh:run_query
    # ./mysql -u cbroot -p -h 127.0.0.1 -P 3770 -A cb_cbgrn < query.sql > result
    ```
  * resultを確認

## SQL
### 基本
 * データの検索、演算結果の抽出
    ```
    SELECT [カラム, ...] FROM [テーブル, ...] WHERE
    ```
 * データの挿入
    ```
    INSERT INTO [テーブル] VALUES (値, ...)
    ```
 * データの更新
    ```
    UPDATE [テーブル] SET [列=値, ...] WHERE
    ```
 * データの削除
    ```
    DELETE FROM [テーブル] WHERE
    ```

### SELECTの種類
 * Simple Query
    ```
    SELECT ... FROM ... WHERE ...
    ```
 * Join Query (結合)
    ```
    SELECT ... FROM t1 JOIN t2 ON ... WHERE ...
    ```
 * Nested Query (サブクエリー)
    ```
    SELECT ... FROM ... WHERE ... IN (SELECT ...）
    SELECT ... FROM (SELECT ... ) WHERE ...
    ```

### ハンズオン
 1. MySQLにログイン
 2. データベースの選択
    ```mysql
    USE xxx;
    ```
    ```mysql
    USE cb_cbgrn;
    ```
 3. テーブルの作成
    ```mysql
    CREATE TABLE xxx (yyy);  # xxx:テーブル名, yyy: カラム名
    ```
    ```mysql
    CREATE TABLE a (c CHAR(100));  # データ型CHAR(100)のカラムcを持つ、テーブルaを作成
    ```
 4. データの参照 & 挿入
    ```mysql
    SELECT xxx FROM yyy WHERE zzz;  # xxx: カラム名, yyy: テーブル名, zzz: 条件
    INSERT INTO xxx(yyy) VALUES ('zzz') # xxx: テーブル名, yyy: カラム名, zzz: 値
    ```
    ```mysql
    SELECT * FROM a;
    INSERT INTO a(c) VALUES ('123abc');
    SELECT * FROM a;
    ```
 5. テーブルの情報を確認
    ```mysql
    SHOW TABLE STATUS LIKE 'xxx'\G  # xxx: テーブル名, \G: 縦表示
    ```
 6. テーブルの変更
    ```mysql
    ALTER TABLE xxx ADD COLUMN yyy zzz;  # xxx: テーブル名, yyy: カラム名, zzz: データ型
    ```
    ```mysql
    ALTER TABLE a ADD COLUMN (id INT, dep INT, name CHAR(30));
    DESC a;
    ALTER TABLE a ADD COLUMN comment CHAR(10);
    ALTER TABLE a ADD hoge CHAR(50) AFTER name; # COLUMN は省略可能
    DESC a;
    ALTER TABLE a CHANGE hoge memo CHAR(20);
    DESC a;
    ALTER TABLE a DROP memo;
    DESC a;
    ```

    * フィールドの追加 : ADD COLUMN
    * フィールドの変更 : MODIFY, CHANGE
    * フィールドの削除 : DROP
    * テーブル名の変更 : RENAME
    * インデックスの追加 : ADD INDEX, ADD UNIQUE, ADD PRIMARY KEY
    * インデックスの削除 : DROP INDEX, DROP PRIMARY KEY

 7. テーブルの破棄
    ```mysql
    DROP TABLE xxx; # xxx: テーブル名
    ```

 8. データの挿入
    ```mysql
    INSERT INTO xxx (yyy) VALUES (zzz); # xxx: テーブル名, yyy: カラム名, zzz: 値
    ```
    ```mysql
    INSERT INTO a (id, name) VALUES (1, 'gyl');
    ```

 9. データの検索
   * WHERE
      ```mysql
      SELECT xxx FROM yyy WHERE zzz;  # zzz: 検索条件
      ```
      ```mysql: 基本的な検索条件
      SELECT xxx FROM yyy WHERE 'フィールド名' '演算子' '値'
      ```

   * 主な演算子  
      * =  
      * >, >=, <, =<  
      * !=, <>  
      * LIKE  
      * IN  
      * IS NULL  
      * IS NOT NULL  
      * AND  
      * OR  
      * BETWEEN a AND b  

   * LIKE
   * ORDER BY

 10. データの更新
   * UPDATE
      ```mysql  
      UPDATE xxx SET yyy=zzz WHERE ZZZ;  # xxx: テーブル名, yyy: フィールド名, zzz: 値, ZZZ: 条件;
      ``` 
      ```mysql
      UPDATE a SET dep=5, comment='agent' WHERE id=2; # WHEREを使用して絞り込み
      ```

 11. データの削除
      ```mysql
      DELETE FROM xxx WHERE yyy=zzz;
      ```
