# Fun-With-Microsoft-SQL
Inspecting a MS sql server



Dump all user created schemas, tables, and columns.
   SELECT
      sch.name,
      obj.name,
      col.name,
      typ.name,
      typ.collation_name,
      typ.max_length,
      typ.is_nullable,
      typ.is_user_defined,
      obj.type
    FROM sys.objects AS obj
          JOIN sys.schemas AS sch
              ON sch.schema_id = obj.schema_id
          JOIN sys.columns AS col
              ON obj.object_id = col.object_id
          JOIN sys.types AS typ
              ON col.system_type_id = typ.system_type_id
   WHERE
      obj.type = 'U'
