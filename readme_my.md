# Postgresql 逻辑结构
## 数据库相关概念
- 数据库集群（database cluster）：一个数据库集群就是一组数据库服务器，它们共同承担着数据库的功能。
- 数据库实例（database instance）：一个数据库实例就是一个数据库服务器进程，它负责处理客户端的请求。
- 数据库（database）：一个数据库就是一个文件，里面包含了各种对象，比如表、视图、索引、触发器、存储过程等。
- 数据库模式（schema）是指数据库中定义的数据库对象集合，它包含了数据库中的所有对象。
- 数据库对象(table、view、index、trigger、stored procedure)：数据库对象是指数据库中的各种实体，比如表、视图、索引、触发器、存储过程等。
- 数据库角色(role)：数据库角色是指数据库中的用户，包括数据库管理员、数据库用户、数据库超级用户等。
- 数据库连接：数据库连接是指客户端与数据库服务器之间的连接，包括客户端程序、数据库服务器、数据库实例等。
- 数据库事务：数据库事务是指一组数据库操作，要么全部成功，要么全部失败。
## 数据库逻辑结构
- 数据库集群（database cluster）> 数据库实例（database instance）> 数据库（database）> 数据库模式（schema）> 数据库对象（table、view、index、trigger、stored procedure）

# Postgresql 系统表
## pg_stat_activity 系统表
- 列名：datid、datname、pid、usesysid、usename、application_name、client_addr、client_hostname、client_port、backend_start、xact_start、query_start、state_change、wait_event_type、wait_event、state、backend_xid、backend_xmin、query
- 说明：pg_stat_activity系统表记录了数据库集群中所有活动的连接的相关信息。
    - datid：连接所在的数据库OID。
    - datname：连接所在的数据库名称。
    - pid：连接的进程ID。
    - usesysid：连接的用户OID。
    - usename：连接的用户名。
    - application_name：连接的客户端程序名称。
    - client_addr：连接的客户端IP地址。
    - client_hostname：连接的客户端主机名。
    - client_port：连接的客户端端口号。
    - backend_start：连接的开始时间。
    - xact_start：当前事务的开始时间。
    - query_start：当前查询的开始时间。
    - state_change：连接状态改变的时间。
    - wait_event_type：等待事件类型。
    - wait_event：等待事件名称。
    - state：连接的状态。
    - backend_xid：当前事务的XID。
    - backend_xmin：当前事务的最早开始XID。
    - query：当前正在执行的查询。
## pg_stat_database 系统表
- 列名：datid、datname、numbackends、xact_commit、xact_rollback、blks_read、blks_hit、tup_returned、tup_fetched、tup_inserted、tup_updated、tup_deleted、conflicts、temp_files、temp_bytes、deadlocks、blk_read_time、blk_write_time
- 说明：pg_stat_database系统表记录了数据库集群中所有数据库的相关统计信息。
    - datid：数据库OID。
    - datname：数据库名称。
    - numbackends：当前连接到数据库的客户端数量。
    - xact_commit：事务提交数。
    - xact_rollback：事务回滚数。
    - blks_read：磁盘块读数。
    - blks_hit：缓存命中数。
    - tup_returned：从数据库返回的行数。
    - tup_fetched：从缓存中返回的行数。
    - tup_inserted：插入的行数。
    - tup_updated：更新的行数。
    - tup_deleted：删除的行数。
    - conflicts：冲突数。
    - temp_files：临时文件数。
    - temp_bytes：临时文件字节数。
    - deadlocks：死锁数。
    - blk_read_time：磁盘块读时间。
    - blk_write_time：磁盘块写时间。
## pg_database 系统表
- 列名：datname、datdba、encoding、datcollate、datctype、datistemplate、datallowconn、datconnlimit、datlastsysoid、datfrozenxid、datminmxid、dattablespace、datacl
- 说明：pg_database系统表记录了数据库集群中所有数据库的相关信息。
    - datname：数据库名称。
    - datdba：数据库所有者的OID。
    - encoding：数据库的字符编码。
    - datcollate：数据库的排序规则。
    - datctype：数据库的字符类型。
    - datistemplate：是否为模板数据库。
    - datallowconn：是否允许连接。
    - datconnlimit：数据库连接限制。
    - datlastsysoid：最后一个系统OID。
    - datfrozenxid：冻结的事务ID。
    - datminmxid：最小的多版本事务ID。
    - dattablespace：数据库的表空间。
    - datacl：数据库的访问控制列表。
## pg_class 系统表
- 列名：oid、relname、relnamespace、reltype、reloftype、relowner、relam、relfilenode、reltablespace、relpages、reltuples、relallvisible、reltoastrelid、reltoastidxid、relhasindex、relisshared、relpersistence、relkind、relnatts、relchecks、relhasoids、relhaspkey、relhasrules、relhastriggers、relhassubclass、relispopulated、relreplident、relfrozenxid、relminmxid、relacl
- 说明：pg_class系统表记录了数据库集群中所有表、视图、索引、触发器、存储过程的相关信息。
    - oid：对象OID。
    - relname：对象名称。
    - relnamespace：对象所在的命名空间OID。
    - reltype：对象类型。
    - reloftype：对象类型的OID。
    - relowner：对象所有者的OID。
    - relam：索引访问方法的OID。
    - relfilenode：对象在磁盘上的文件节点。
    - reltablespace：对象所在的表空间OID。
    - relpages：对象占用的磁盘页数。
    - reltuples：对象中行的数量。
    - relallvisible：对象是否对所有会话可见。 
    - reltoastrelid：对象中的toast表的OID。
    - reltoastidxid：对象中的toast索引的OID。
    - relhasindex：对象是否有索引。
    - relisshared：对象是否为共享对象。
    - relpersistence：对象持久性类型。
    - relkind：对象类型。'r'表示表，'v'表示视图，'i'表示索引，'S'表示序列，'t'表示toast表，'c'表示复合类型，'f'表示函数，'p'表示过程，'n'表示模式，'y'表示类型。
    - relnatts：对象中属性的数量。
    - relchecks：对象中检查约束的数量。
    - relhasoids：对象是否有OID。
    - relhaspkey：对象是否有主键。
    - relhasrules：对象是否有规则。
    - relhastriggers：对象是否有触发器。
    - relhassubclass：对象是否有子类。
    - relispopulated：对象是否已填充。
    - relreplident：对象复制标识符。
    - relfrozenxid：对象冻结的事务ID。
    - relminmxid：对象最小的多版本事务ID。
    - relacl：对象访问控制列表。
## pg_namespace 系统表
- 列名：oid、nspname、nspowner、nspacl
- 说明：pg_namespace系统表记录了数据库集群中所有命名空间的相关信息。
    - oid：命名空间OID。
    - nspname：命名空间名称。
    - nspowner：命名空间所有者的OID。
    - nspacl：命名空间访问控制列表。
## pg_stat_user_tables 系统表
- 列名：relid、schemaname、relname、seq_scan、seq_tup_read、idx_scan、idx_tup_fetch、n_tup_ins、n_tup_upd、n_tup_del、n_tup_hot_upd、n_live_tup、n_dead_tup、n_mod_since_analyze、last_vacuum、last_data_changed、last_autovacuum、last_analyze、last_autoanalyze
- 说明：pg_stat_user_tables系统表记录了数据库集群中所有用户表的相关统计信息。
    - relid：表的OID。
    - schemaname：表所在的模式名称。
    - relname：表名称。
    - seq_scan：顺序扫描数。
    - seq_tup_read：顺序扫描读的行数。
    - idx_scan：索引扫描数。
    - idx_tup_fetch：索引扫描读的行数。
    - n_tup_ins：插入的行数。
    - n_tup_upd：更新的行数。
    - n_tup_del：删除的行数。
    - n_tup_hot_upd：热更新的行数。
    - n_live_tup：活跃行数。
    - n_dead_tup：死行数。
    - n_mod_since_analyze：自上次分析以来修改的行数。
    - last_vacuum：最后一次清理的时间。
    - last_data_changed：最后一次数据修改的时间。
    - last_autovacuum：最后一次自动清理的时间。
    - last_analyze：最后一次分析的时间。
    - last_autoanalyze：最后一次自动分析的时间。
## pg_tablespace 系统表
- 列名：oid、spcname、spclocation、spcacl
- 说明：pg_tablespace系统表记录了数据库集群中所有表空间的相关信息。

## pg_authid 系统表
- 列名：oid、rolname、rolsuper、rolinherit、rolcreaterole、rolcreatedb、rolcanlogin、rolreplication、rolconnlimit、rolvaliduntil、rolpassword、rolconfig
- 说明：pg_authid系统表记录了数据库集群中所有用户的相关信息。

## pg_roles 系统表
- 列名：oid、rolname、rolinherit、rolcreaterole、rolcreatedb、rolcanlogin、rolreplication、rolconnlimit、rolvaliduntil、rolpassword、rolconfig
- 说明：pg_roles系统表是pg_authid系统表的别名。

## pg_tables 系统表
- 列名：tablename、schemaname、tableowner、tablespace、hasindexes、hasrules、hastriggers、rowsecurity
- 说明：pg_tables系统表记录了数据库集群中所有表的相关信息。
   - tablename：表名称。
   - schemaname：表所在的模式名称。
   - tableowner：表的所有者的名称。
   - tablespace：表所在的表空间名称。
   - hasindexes：表是否有索引。
   - hasrules：表是否有规则。
   - hastriggers：表是否有触发器。
   - rowsecurity：表是否支持行级安全性。       


## pg_indexes 系统表
- 列名：tablename、indexdef、schemaname
- 说明：pg_indexes系统表记录了数据库集群中所有索引的相关信息。

# Postgresql 用户表
## 用户表的隐藏属性
- oid： 对象标识符，生成的值是全局唯一的，表、索引、视图都带有oid，如果需要在用户创建的表中使用oid字段，需要显示指定“with oids”选项。 PostgreSQL 12 及更高版本中，WITH OIDS 语法已经被移除
- ctid：每条记录（称为一个tuple）在表中的物理位置标识。(page number, offset)。
- cmin：最小的命令标识符。
- cmax：最大的命令标识符。
- xmin：创建一条记录（tuple）时，记录此值为当前事务ID。
- xmax：创建tuple时，默认为0，删除tuple时，记录此值为当前事务ID。
- xip_list：事务标识符列表。
- gp_segment_id：分区标识符。
- gp_segment_count：分区数量。
- gp_replication_factor：复制因子。
- gp_partition_policy：分区策略。
- gp_policy_name：策略名称。
- gp_policy_type：策略类型。
- gp_num_contents_in_cluster：集群中内容的数量。
- gp_num_contents_in_partition：分区中内容的数量。
- gp_distribution_policy：分布策略。
- gp_persistent_relation_node：持久化关系节点。
- gp_persistent_relation_node_count：持久化关系节点数量。
- gp_persistent_relation_dist_rank：持久化关系分布排名。
- gp_persistent_relation_num_children：持久化关系子节点数量。
- gp_persistent_relation_children：持久化关系子节点。
- gp_persistent_relation_relfrozenxid：持久化关系冻结的事务ID。
- gp_persistent_relation_freeze_min_xid：持久化关系最小的事务ID。
- gp_persistent_relation_freeze_max_xid：持久化关系最大的事务ID。
- gp_persistent_relation_freeze_table_name：持久化关系冻结的表名。
- gp_persistent_relation_toast_oid：持久化关系的toast表OID。
- gp_persistent_relation_toast_index_oid：持久化关系的toast索引OID。
- gp_fastsequence_last_value：快速序列的最后一个值。
- gp_fastsequence_is_called：快速序列是否被调用。
- gp_fastsequence_is_distributed：快速序列是否分布式。
- gp_fastsequence_last_distributed_xid：快速序列的最后一个分布式事务ID。
- gp_fastsequence_last_distributed_xid_context：快速序列的最后一个分布式事务ID的上下文。
- gp_fastsequence_last_distributed_xid_epoch：快速序列的最后一个分布式事务ID的时代。
- gp_fastsequence_next_distributed_xid：快速序列的下一个分布式事务ID。
- gp_fastsequence_next_distributed_xid_context：快速序列的下一个分布式事务ID的上下文。
- gp_fastsequence_next_distributed_xid_epoch：快速序列的下一个分布式事务ID的时代。
- gp_fastsequence_cache_value：快速序列的缓存值。
- gp_fastsequence_cache_next_xid：快速序列的缓存下一个事务ID。
- gp_fastsequence_cache_next_xid_epoch：快速序列的缓存下一个事务ID的时代。
- gp_fastsequence_cache_next_xid_context：快速序列的缓存下一个事务ID的上下文。
- gp_fastsequence_cache_last_xid：快速序列的缓存最后一个事务ID。
- gp_fastsequence_cache_last_xid_epoch：快速序列的缓存最后一个事务ID的时代。
- gp_fastsequence_cache_last_xid_context：快速序列的缓存最后一个事务ID的上下文。
- gp_fastsequence_cache_last_distributed_xid：快速序列的缓存最后一个分布式事务ID。
- gp_fastsequence_cache_last_distributed_xid_epoch：快速序列的缓存最后一个分布式事务ID的时代。
- gp_fastsequence_cache_last_distributed_xid_context：快速序列的缓存最后一个分布式事务ID的上下文。
- gp_fastsequence_cache_is_called：快速序列的缓存是否被调用。
- gp_fastsequence_cache_is_distributed：快速序列的缓存是否分布式。
- gp_fastsequence_cache_last_distributed_xid_epoch_offset：快速序列的缓存最后一个分布式事务ID的时代偏移。
- gp_fastsequence_cache_next_xid_epoch_offset：快速序列的缓存下一个事务ID的时代偏移。
- gp_fastsequence_cache_last_xid_epoch_offset：快速序列的缓存最后一个事务ID的时代偏移。
- gp_fastsequence_cache_last_distributed_xid_epoch_offset：快速序列的缓存最后一个分布式事务ID的时代偏移。
- gp_fastsequence_cache_next_xid_context_offset：快速序列的缓存下一个事务ID的上下文偏移。
- gp_fastsequence_cache_last_xid_context_offset：快速序列的缓存最后一个事务ID的上下文偏移。
- gp_fastsequence_cache_last_distributed_xid_context_offset：快速序列的缓存最后一个分布式事务ID的上下文偏移。
- gp_fastsequence_cache_next_xid_epoch_wraparound：快速序列的缓存下一个事务ID的时代是否发生回绕。
- gp_fastsequence_cache_last_xid_epoch_wraparound：快速序列的缓存最后一个事务ID的时代是否发生回绕。
- gp_fastsequence_cache_last_distributed_xid_epoch_wraparound：快速序列的缓存最后一个分布式事务ID的时代是否发生回绕。
- gp_fastsequence_cache_next_xid_context_wraparound：快速序列的缓存下一个事务ID的上下文是否发生回绕。
- gp_fastsequence_cache_last_xid_context_wraparound：快速序列的缓存最后一个事务ID的上下文是否发生回绕。


# Postgresql 索引
## 索引的创建
```
CREATE [ UNIQUE ] INDEX index_name ON table_name [ USING method ] ( column_name | ( expression ) ) [ COLLATE collation ] [ opclass ] [ ASC | DESC ] [ NULLS { FIRST | LAST } ] [ INCLUDE ( column_name [, ...] ) ] [ WITH ( storage_parameter = value [, ... ] ) ]
```
- UNIQUE：创建唯一索引。
- USING method：指定索引的类型，目前支持BTREE、HASH、GIN、BRIN、SPGIST、GIST。
- COLLATE collation：指定索引的排序规则。
- opclass：指定索引的操作符类。
- ASC：指定索引的升序排序。
- DESC：指定索引的降序排序。
- NULLS { FIRST | LAST }：指定索引的NULL值排序顺序。
- INCLUDE ( column_name [, ...] )：指定索引包含的列。
- WITH ( storage_parameter = value [, ... ] )：指定索引的存储参数。

## pg_amop 表存储与索引访问方法相关的操作符信息。
- oid：操作符OID。
- amopfamily：操作符所属的操作符族OID。
- amoplefttype：操作符的左操作数类型OID。
- amoprighttype：操作符的右操作数类型OID。
- amopstrategy：操作符的策略号。
- amoppurpose：操作符的用途。
- amopopr:操作符的操作符号。(比如：=、<、>、~~等)指向一个pg_operator表的oid。
- amopmethod：操作符所属的访问方法OID。
- amopsortfamily：操作符的排序操作符族OID。


## pg_amproc 表用于存储与索引访问方法（access methods）相关的过程（functions）信息。
- oid：操作符过程OID。
- amprocfamily：操作符过程所属的操作符族OID。
- amproclefttype：操作符过程的左操作数类型OID。
- amprocrighttype：操作符过程的右操作数类型OID。
- amprocnum：
- amproc：存储与该索引操作相关的支持函数的标识符，通常是函数的名称。

## pg_type系统表记录了数据库集群中所有数据类型（包括复合类型）的相关信息。
- oid：数据类型OID。
- typname：数据类型名称。
- typnamespace：数据类型所属的模式OID。
- typowner：数据类型所有者的OID。
- typlen：数据类型长度。
- typbyval：数据类型是否以值传递。
- typtype：数据类型类型。
- typcategory：数据类型类别。
- typispreferred：数据类型是否为首选类型。
- typisdefined：数据类型是否已定义。
- typdelim：数据类型分隔符。
- typrelid：数据类型所属的关系OID。
- typelem：数组元素类型OID。




## pg_operator系统表记录了数据库集群中所有操作符的相关信息。
- oid：操作符OID。
- oprname：操作符名称。
- oprnamespace：操作符所属的模式OID。
- oprowner：操作符所有者的OID。
- oprkind：操作符的类型。
- oprcanmerge：操作符是否可以合并。
- oprcanhash：操作符是否可以哈希。
- oprleft：操作符的左操作数类型OID。
- oprright：操作符的右操作数类型OID。
- oprcom：操作符的commutator操作符OID。
- oprnegate：操作符的反操作符OID。
- oprcode：操作符的内部代码。
- oprrest：操作符的restriction操作符OID。
- oprjoin：操作符的join操作符OID。
- oprcanorder：操作符是否可以排序。


## pg_opclass系统表记录了数据库集群中所有操作符类的相关信息。
- oid：操作符类OID。
- opcname：操作符类名称。
- opcmethod：操作符类所属的访问方法OID。
- opcnamespace：操作符类所属的模式OID。
- opcowner：操作符类所有者的OID。
- opcdefault：操作符类是否为默认操作符类。
- opcfamily：操作符类所属的操作符族OID。
- opcintype：操作符类所属的输入类型OID。
- opckeytype：操作符类所属的键类型OID。

## pg_opfamily系统表记录了数据库集群中所有操作符族的相关信息。
- oid：操作符族OID。
- opfname：操作符族名称。
- opfnamespace：操作符族所属的模式OID。
- opfowner：操作符族所有者的OID。
- opfmethod：操作符族所属的访问方法OID。

## pg_am系统表记录了索引访问方法的相关信息。
- oid：访问方法OID。
- amname：访问方法名称。
- amhandler：访问方法的处理函数OID。（该方法返回一个IndexAmRoutine结构,这个结构定义了该索引访问方法的所有相关函数，比如索引扫描、插入、删除、构建索引、重构索引等操作。）
- amtype：访问方法的类型。(i表示索引访问方法，a表示表访问方法)




## 索引的删除
```
DROP INDEX [ CONCURRENTLY ] index_name [ CASCADE | RESTRICT ]
```
- CONCURRENTLY：并发删除索引。
- CASCADE：级联删除依赖于该索引的对象。
- RESTRICT：如果有依赖对象，则拒绝删除索引。

## 索引的重命名
```
ALTER INDEX index_name RENAME TO new_name
```

## 索引的修改
```
ALTER INDEX index_name [ SET TABLESPACE tablespace_name ] [ SET ( storage_parameter = value [, ... ] ) ]
```
- SET TABLESPACE tablespace_name：修改索引的表空间。
- SET ( storage_parameter = value [, ... ] )：修改索引的存储参数。

## 索引的使用
```
EXPLAIN SELECT statement
```
- EXPLAIN：显示SQL语句的执行计划。




# Postgresql 常用命令
## 数据库服务相关命令

```
/usr/local/pgsql/bin/pg_ctl -D /usr/local/pgsql/data [start|stop|restart|status]
```
- -D：指定数据库实例的路径。
- start：启动数据库服务器。
- stop：停止数据库服务器。
- restart：重启数据库服务器。
- status：查看数据库服务器的状态。

## 数据库相关命令
### 查看数据库列表
```
\l
```

### 查看当前数据库
```
\c
```

### 创建数据库
```
CREATE DATABASE database_name;
```

### 删除数据库
```
DROP DATABASE database_name;
```


### 连接数据库
```
psql -h host -p port -U username -d database
```
- -h：指定数据库服务器的主机名或IP地址。
- -p：指定数据库服务器的端口号。
- -U：指定数据库用户的名称。
- -d：指定要连接的数据库名称。
### 退出数据库
```
\q
```

## 表相关命令
### 查看表列表
```
\d
```

### 查看表结构
```
\d table_name
```

### 创建表
```
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```

### 删除表
```
DROP TABLE table_name;
```

## 常用SQL语句
### 插入数据
```
INSERT INTO table_name (column1, column2,...)
VALUES (value1, value2,...);
```

### 更新数据
```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

### 删除数据
```
DELETE FROM table_name
WHERE condition;
```
### 查询数据
```
SELECT column1, column2, ...
FROM table_name
WHERE condition;
``` 
## 其他命令
### 显示当前会话的SQL语句
```
\s
```
### 显示当前会话的事务状态
```
\z
```
### 显示当前会话的连接信息
```
\conninfo
```
### 查询当前连接的进程ID
```
SELECT pg_backend_pid();
```

### begin 开始事务
```
BEGIN [ WORK | TRANSACTION ] [ transaction_mode [, ...] ]

```
begin 开始事务后，如果执行失败，则会回滚事务。
WORK 或者 TRANSACTION 关键字可以省略。WORK 关键字表示该事务为工作事务，TRANSACTION 关键字表示该事务为用户事务。

### commit 提交事务
```
COMMIT;
```

### rollback 回滚事务
```
ROLLBACK;
```

### 查询事务ID
```
SELECT txid_current();
```
### 查询快照
```
SELECT txid_snapshot_xmin(txid_current_snapshot()), txid_snapshot_xmax(txid_current_snapshot()), txid_snapshot_xip_list(txid_current_snapshot());
```
### 清空表数据
```
TRUNCATE TABLE table_name;
```


### 查询用户表
```
select pg_class.oid,pg_class.relname,relkind,relfilenode,n_live_tup,pg_size_pretty(pg_relation_size(pg_stat_user_tables.relid)) AS table_size,nspname 
from pg_class 
join pg_namespace on pg_class.relnamespace=pg_namespace.oid 
join pg_stat_user_tables on pg_class.oid=pg_stat_user_tables.relid 
where 
    pg_class.relkind='r' 
    and 
    pg_namespace.nspname='public'
order by pg_class.relname;
``` 
### 查询表大小
```
SELECT pg_size_pretty(pg_total_relation_size('my_table')) AS total_size;
SELECT pg_size_pretty(pg_relation_size('my_table')) AS table_size;
SELECT pg_size_pretty(pg_indexes_size('my_table')) AS indexes_size;
```
### 查询表的字段信息
```
SELECT column_name, data_type, character_maximum_length, numeric_precision, is_nullable 
FROM information_schema.columns 
WHERE table_name = 'table_name';
``` 
