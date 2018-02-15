# 項目
 * 特徴
 * RDB(リレーショナルデータベース)
 * SQL

## 特徴
### お手軽なDBMS
    * MyISAMなら16MBから動作。
    * 設定ファイルが一つ(my.ini or my.cnf)。
    * 多くのOSで動作。プラットフォームに依存しない。

### いろいろできる
    - 各種文字コードに対応。
    - C. Ruby, PHP, Perl, Python など、多くの開発言語に対応。
    - マルチスレッド方式。
    - マルチストレージエンジン。

### 冗長性 / 負荷分散
    - レプリケーション機能

### オープンソース

### 2種類のライセンス
    - 無料のGPL
    - 商用のもの

### Oracleが管理/メンテナンス
    - 有料のサポートも

## RDB(リレーショナルデータベース)
この資料を基に説明します。  
[リレーショナルデータベース入門](https://www.sraoss.co.jp/event_seminar/2008/what_is_rdb.pdf)

 * データとデータに関連を持たせ、2次元の表で表現する
 * 数学の集合と同じ！

### トランザクション
 * 複数のSQL文を、１つの処理単位にまとめたもの。  
 * [1トランザクション内のSQL] -> [全て成功] or [全て失敗] のいずれかであることが保証される！

     ```
     BEGIN #開始
     ... #処理
     ... #処理
     ... #処理
     COMMIT #終了
     ```

### 排他制御
 * 複数のユーザー(スレッド)が同じデータを操作した際に、矛盾が生じないようにする
    * 行ロック: 1行をロック(例: MyISAM)
    * テーブルロック: テーブル全体をロック(例: InnoDB)

### アーキテクチャ
  スライド5がわかりやすい。  
  [MySQLアーキテクチャ図解講座](https://www.slideshare.net/nippondanji/mysql-64455514)

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
