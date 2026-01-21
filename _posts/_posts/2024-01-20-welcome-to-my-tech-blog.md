---
layout: post
title: "Welcome to My SQL Server & DevOps Blog"
date: 2024-01-20 12:00:00 +0530
categories: [announcement, sql-server, devops]
tags: [introduction, getting-started]
author: "Your Name"
---

## Why I'm Starting This Blog

After 5+ years working with SQL Server and DevOps practices, I've decided to share my knowledge. This blog will cover:

- **SQL Server**: Performance tuning, high availability, security
- **DevOps/SRE**: Monitoring, automation, CI/CD pipelines
- **Cloud**: Azure SQL, Kubernetes, infrastructure as code

## What to Expect

### SQL Server Content
```sql
-- Practical examples like this:
SELECT 
    query_stats.query_hash,
    SUM(query_stats.total_worker_time) / SUM(query_stats.execution_count) AS avg_cpu_time,
    MIN(query_stats.statement_text) AS sample_query_text
FROM 
    (SELECT 
        QS.*,
        SUBSTRING(ST.text, (QS.statement_start_offset/2) + 1,
            ((CASE statement_end_offset 
                WHEN -1 THEN DATALENGTH(ST.text)
                ELSE QS.statement_end_offset END 
                - QS.statement_start_offset)/2) + 1) AS statement_text
     FROM sys.dm_exec_query_stats AS QS
     CROSS APPLY sys.dm_exec_sql_text(QS.sql_handle) AS ST) AS query_stats
GROUP BY query_stats.query_hash
ORDER BY 2 DESC;
