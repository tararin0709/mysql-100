# mysql-100
現場で本当に使うものだけを厳選！✨

🌟【基本操作編】第1-20位：毎日使う

🌟1-5位：絶対の絶対

sql
1. SELECT    -- データを取得（最も使う）
   SELECT * FROM users;
   SELECT name, age FROM users WHERE id = 1;

2. INSERT    -- データを追加
   INSERT INTO users (name, age) VALUES ('田中', 25);

3. UPDATE    -- データを更新
   UPDATE users SET age = 26 WHERE name = '田中';

4. DELETE    -- データを削除
   DELETE FROM users WHERE id = 1;

5. WHERE     -- 条件指定（めっちゃ使う）
   SELECT * FROM users WHERE age >= 20;

   
🌟6-10位：条件系


sql


6. AND/OR    -- 複数条件
   SELECT * FROM users WHERE age >= 20 AND city = '東京';

7. IN        -- 複数の値に一致
   SELECT * FROM users WHERE city IN ('東京', '大阪', '名古屋');

8. BETWEEN   -- 範囲指定
   SELECT * FROM products WHERE price BETWEEN 1000 AND 5000;

9. LIKE      -- 部分一致検索
   
   SELECT * FROM users WHERE name LIKE '田%';
    -- 田で始まる
   
   SELECT * FROM users WHERE name LIKE '%子';
   -- 子で終わる

10. IS NULL   -- NULLの検索
    SELECT * FROM users WHERE deleted_at IS NULL;

    
🌟11-15位：並び替え系

sql

11. ORDER BY  -- 並び替え

     SELECT * FROM products ORDER BY price DESC;
    -- 高い順
     
     SELECT * FROM users ORDER BY created_at ASC;
    -- 古い順

13. DESC/ASC  -- 降順/昇順
     ORDER BY price DESC   -- 降順（高い→低い）
     ORDER BY price ASC    -- 昇順（低い→高い）

14. LIMIT     -- 取得件数制限
     SELECT * FROM users LIMIT 10;
    -- 10件だけ

15. OFFSET    -- 開始位置指定（ページネーション）
     SELECT * FROM users LIMIT 10 OFFSET 20;
    -- 21-30件目

16. DISTINCT  -- 重複排除
     SELECT DISTINCT city FROM users;
    -- ユニークな都市一覧

    
🌟16-20位：集計系

sql


16. COUNT     -- 件数カウント
     SELECT COUNT(*) FROM users;
     SELECT COUNT(DISTINCT city) FROM users;

17. SUM       -- 合計
     SELECT SUM(price) FROM orders WHERE user_id = 1;

18. AVG       -- 平均
     SELECT AVG(age) FROM users WHERE city = '東京';

19. MAX/MIN   -- 最大/最小
     SELECT MAX(price), MIN(price) FROM products;

20. GROUP BY  -- グループ化
     SELECT city, COUNT(*) FROM users GROUP BY city;


🌟【テーブル操作編】第21-40位：設計時に使う

🌟21-25位：テーブル作成・削除


sql

21. CREATE TABLE  -- テーブル作成
     CREATE TABLE users (
         id INT PRIMARY KEY,
         name VARCHAR(100)
     );

22. DROP TABLE    -- テーブル削除（注意！）
     DROP TABLE users;  -- テーブルごと消える

23. ALTER TABLE   -- テーブル変更
     ALTER TABLE users ADD COLUMN email VARCHAR(255);

24. TRUNCATE      -- 全データ削除（テーブルは残る）
     TRUNCATE TABLE users;  -- DELETEより速い

25. RENAME TABLE  -- テーブル名変更
     RENAME TABLE users TO members;

    
🌟26-30位：カラム操作


sql

26. ADD COLUMN    -- カラム追加
     ALTER TABLE users ADD COLUMN age INT;

27. DROP COLUMN   -- カラム削除
     ALTER TABLE users DROP COLUMN age;

28. MODIFY COLUMN -- カラム定義変更
     ALTER TABLE users MODIFY COLUMN name VARCHAR(200);

29. CHANGE COLUMN -- カラム名変更
     ALTER TABLE users CHANGE COLUMN name username VARCHAR(100);

30. RENAME COLUMN -- カラム名変更（MySQL 8.0以降）
     ALTER TABLE users RENAME COLUMN name TO username;

    
🌟31-35位：データ型


sql

31. INT           -- 整数

32. VARCHAR(n)    -- 可変長文字列（255までよく使う）

33. TEXT          -- 長い文章
 
34. DATETIME      -- 日時 '2024-01-01 10:30:00'

35. DATE          -- 日付 '2024-01-01'

36. TIMESTAMP     -- タイムスタンプ（自動更新できる）
 
37. BOOLEAN       -- 真偽値（実際はTINYINT(1)）

38. DECIMAL       -- 小数（金額とか）

39. FLOAT/DOUBLE  -- 浮動小数点数

40. JSON          -- JSON形式（MySQL 5.7以降）


🌟【制約・キー編】第41-55位：データ品質維持

🌟41-45位：制約


sql

41. PRIMARY KEY   -- 主キー（唯一のID）
     id INT PRIMARY KEY AUTO_INCREMENT


42. FOREIGN KEY   -- 外部キー（他テーブル参照）
     FOREIGN KEY (user_id) REFERENCES users(id)


43. UNIQUE        -- 重複禁止
     email VARCHAR(255) UNIQUE


44. NOT NULL      -- NULL禁止
     name VARCHAR(100) NOT NULL


45. DEFAULT       -- デフォルト値
     status INT DEFAULT 1
     created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    
    
🌟46-50位：キー関連


sql

46. AUTO_INCREMENT -- 自動連番
     id INT AUTO_INCREMENT

47. INDEX          -- インデックス作成
     CREATE INDEX idx_name ON users(name);

48. PRIMARY/UNIQUE -- キーの種類
49. KEY            -- インデックスの別名
50. CONSTRAINT     -- 制約に名前をつける
     CONSTRAINT fk_user_id FOREIGN KEY (user_id) REFERENCES users(id)

    
🌟【結合・応用編】第51-70位：複雑なクエリ

🌟51-55位：JOIN（超重要！）


sql

51. INNER JOIN  -- 内部結合（両方にあるデータのみ）
     SELECT * FROM orders 
     INNER JOIN users ON orders.user_id = users.id;

52. LEFT JOIN   -- 左外部結合（左テーブルは全部）
     SELECT * FROM users 
     LEFT JOIN orders ON users.id = orders.user_id;

53. RIGHT JOIN  -- 右外部結合（右テーブルは全部）
54. FULL JOIN   -- 完全外部結合（MySQLは非対応）
55. CROSS JOIN  -- 交差結合（全組み合わせ）


🌟56-60位：サブクエリ


sql

56. スカラサブクエリ  -- 1行1列の結果
     SELECT name, (SELECT AVG(age) FROM users) AS avg_age FROM users;

57. 相関サブクエリ    -- 外部クエリを参照
     SELECT * FROM products p1 
     WHERE price > (SELECT AVG(price) FROM products p2 WHERE p2.category = p1.category);

58. EXISTS       -- 存在確認
     SELECT * FROM users u 
     WHERE EXISTS (SELECT 1 FROM orders o WHERE o.user_id = u.id);

59. IN/ANY/ALL   -- サブクエリと組み合わせ
60. AS           -- エイリアス（別名）


🌟61-65位：便利機能


sql

61. CASE         -- 条件分岐
     SELECT 
         name,
         CASE 
             WHEN age < 20 THEN '未成年'
             WHEN age < 65 THEN '成人'
             ELSE '高齢者'
         END AS category
     FROM users;

62. COALESCE    -- NULLを別の値に
     SELECT COALESCE(phone, '未登録') FROM users;

63. IFNULL      -- NULL置き換え（MySQL）
64. DATE_FORMAT -- 日付フォーマット
     SELECT DATE_FORMAT(created_at, '%Y年%m月%d日') FROM users;

65. CONCAT      -- 文字列結合
     SELECT CONCAT(last_name, first_name) AS full_name FROM users;

    
🌟【集計応用編】第66-80位：分析系

66-70位：HAVINGとウィンドウ関数


sql

66. HAVING      -- GROUP BYの後の条件
     SELECT city, COUNT(*) FROM users 
     GROUP BY city 
     HAVING COUNT(*) > 10;

67. ウィンドウ関数 -- 行間計算（MySQL 8.0）
68. ROW_NUMBER()  -- 行番号
69. RANK()        -- ランキング
70. LAG/LEAD      -- 前後の行を参照


🌟71-75位：便利な集計


sql

71. ROLLUP      -- 小計/合計を追加
72. GROUP_CONCAT -- グループ内の値を連結
     SELECT city, GROUP_CONCAT(name) FROM users GROUP BY city;

73. REGEXP      -- 正規表現
74. LIKE        -- パターンマッチ
75. SOUNDEX     -- 発音で検索


🌟【管理・設定編】第81-95位：運用系

81-85位：ユーザー管理


sql

81. CREATE USER  -- ユーザー作成

82. GRANT        -- 権限付与

83. REVOKE       -- 権限削除

84. SHOW GRANTS  -- 権限確認

85. DROP USER    -- ユーザー削除


🌟86-90位：データベース操作

sql

86. CREATE DATABASE  -- DB作成

87. DROP DATABASE    -- DB削除

88. USE database_name -- DB選択

89. SHOW DATABASES   -- DB一覧

90. SHOW TABLES      -- テーブル一覧


🌟91-95位：トランザクション


sql

91. BEGIN/START TRANSACTION  -- トランザクション開始

92. COMMIT        -- 確定

93. ROLLBACK      -- キャンセル

94. SAVEPOINT     -- 途中セーブ

95. LOCK TABLES   -- テーブルロック


🌟【トラブルシューティング編】第96-100位：デバッグ


sql

96. EXPLAIN      
-- 実行計画確認（チューニングに必須）
     EXPLAIN SELECT * FROM users WHERE name = '田中';

97. SHOW WARNINGS -- 警告表示
98. SHOW ERRORS   -- エラー表示
99. SHOW PROCESSLIST -- 実行中のプロセス
100. KILL [process_id] -- プロセス強制終了


🌟101. 
【最重要！】絶対に覚えるべきトップ10


sql

1. SELECT * FROM table;
2. INSERT INTO table VALUES (...);
3. UPDATE table SET col = value WHERE condition;
4. DELETE FROM table WHERE condition;
5. WHERE column = value
6. ORDER BY column DESC/ASC
7. LIMIT n
8. JOIN other_table ON condition
9. GROUP BY column
10. COUNT(*), SUM(column), AVG(column)


🌟初心者がよく間違えるポイント


sql

-- ❌ 間違い
DELETE FROM users;  -- 全データ消える！（WHERE忘れ）

-- ⭕ 正しい
DELETE FROM users WHERE id = 1;

-- ❌ 間違い
SELECT * FROM users LIMIT 10, 20;  -- 古い書き方

-- ⭕ 正しい
SELECT * FROM users LIMIT 20 OFFSET 10;

-- ❌ 間違い
UPDATE users SET age = 30;  -- 全員30歳になる！

-- ⭕ 正しい
UPDATE users SET age = 30 WHERE id = 1;

これだけ押さえれば、実務で困ることはほぼありません！
最初は20-30個から少しずつ覚えていけばOKです👍






    
