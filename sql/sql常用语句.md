
1. 向表中添加字段

```sql
Alter table [表名] add [列名] 类型
```

2. 删除字段

```sql
Alter table [表名] drop column [列名]
```

3. 修改表中字段类型 (可以修改列的类型，是否为空)

```sql
Alter table [表名] alter column [列名] 类型
```

4. 添加主键

```sql
Alter table [表名] add constraint [ 约束名] primary key( [列名])
```

5. 添加唯一约束

```sql
Alter table [表名] add constraint [ 约束名] unique([列名])
```

6. 添加表中某列的默认值

```sql
Alter table [表名] add constraint [约束名] default(默认值) for [列名]
```

7. 添加约束

```sql
Alter table [表名] add constraint [约束名] check (内容)
```

8. 添加外键约束

```sql
Alter table [表名] add constraint [约束名] foreign key(列名) referencese 另一表名(列名)
```

9. 删除约束

```sql
Alter table [表名] drop constraint [约束名]
```

10. 重命名表

```sql
exec sp_rename '[原表名]','[新表名]'
```

11. 重命名列名

```sql
exec sp_rename '[表名].[列名]','[表名].[新列名]'
```

12. 打开查询分析器的IO统计和时间统计：

```sql
SET STATISTICS IO ON;
SET STATISTICS TIME ON;
```



