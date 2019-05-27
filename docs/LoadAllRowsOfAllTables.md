# Getting all tables' information including rows of each table in the database (取得資料庫所有資料表資料)
DECLARE @TABLE_NAME NVARCHAR(max)

DECLARE CUR CURSOR
FOR SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES ORDER BY TABLE_NAME
--declare a cussor (指定游標給資料表)

OPEN CUR FETCH NEXT FROM CUR INTO @TABLE_NAME
--open the cursor and start fetching the first row (開啟游標開始抓第一筆資料)

WHILE @@FETCH_STATUS = 0
--if the table have data (如果資料表一直有資料)

BEGIN
	EXEC('IF EXISTS(SELECT * FROM ' + @TABLE_NAME + ')
		  SELECT ''' + @TABLE_NAME + ''' AS TABLE_NAME , * FROM ' + @TABLE_NAME)
	FETCH NEXT FROM CUR INTO @TABLE_NAME
  --jump to next row (跳到下一筆資料)
END

CLOSE CUR
--close cursor (關閉游標)

DEALLOCATE CUR
--deallocate cursor (刪除游標)
