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

Dump all user created views. With the previous information you should have a decent idea of how to reconstruct the database

      SELECT
         sch.name,
         obj.name,
         col.name,
         sqlmod.definitation
      FROM
         sys.objects AS obj,
         sys.schemas AS sch,
         sys.columns AS col,
         sys.sql_modules AS sqlmod
      WHERE
            obj.type = 'V'
         AND
            obj.object_id = sqlmod.object_id
         AND
            obj.object_id = col.object_id
         AND
            obj.schema_id = sch.schema_id
