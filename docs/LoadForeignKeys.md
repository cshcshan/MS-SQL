# Getting all primary keys in database (取得資料庫所有Primary Key)
SELECT OBJECT_NAME(constraint_object_id) AS [FK Name], COL_NAME(constraint_object_id, constraint_column_id),
	OBJECT_NAME(parent_object_id) AS [Table], COL_NAME(parent_object_id, parent_column_id) AS [Col],
	OBJECT_NAME(referenced_object_id) AS [RefTable], COL_NAME(referenced_object_id, referenced_column_id) AS [RefCol]
FROM sys.foreign_key_columns
ORDER BY OBJECT_NAME(parent_object_id), COL_NAME(parent_object_id, parent_column_id)
