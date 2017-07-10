# -mysql 查看表索引使用情况 

select object_type,
       object_schema,
       object_name,
       index_name,
       count_star,
       count_read,
       COUNT_FETCH
  from performance_schema.table_io_waits_summary_by_index_usage
 where object_name= 'cs_order' ;
