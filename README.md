



This project implements a simplified database engine with support for fundamental operations such as creating tables, inserting, updating, deleting tuples, and searching in tables. Additionally, it provides functionality for building and utilizing B+ tree indices to optimize queries.

## Features

- **Table Creation**: Tables can be created dynamically, with support for multiple data types, including `java.lang.Integer`, `java.lang.String`, and `java.lang.Double`.
- **Page Storage**: Data is stored across multiple pages, each represented as serialized binary files to handle large datasets efficiently. Pages are loaded only when needed, reducing memory consumption.
- **Row Operations**: Insert, update, and delete operations are supported, with clustering on the primary key. Rows are stored as objects and serialized to disk to manage table partitions.
- **B+ Tree Indexing**: Indexes can be created on demand to improve search efficiency. The database engine supports querying with and without indices, using B+ trees to optimize queries.
- **Linear Search**: For columns without indices, linear searches are performed.
- **Index Persistence**: Both tables and their indices are persisted on disk, allowing the database to reload them upon startup without requiring a full scan.
- **Metadata Management**: Metadata, such as table schema, column types, and index information, is stored in a `metadata.csv` file, which is referenced for validation and efficient query execution.

## Example Usage

Below is a sample code that demonstrates how to use the engine:

```java
String strTableName = "Student";
DBApp dbApp = new DBApp();
Hashtable<String, String> htblColNameType = new Hashtable<>();
htblColNameType.put("id", "java.lang.Integer");
htblColNameType.put("name", "java.lang.String");
htblColNameType.put("gpa", "java.lang.Double");

dbApp.createTable(strTableName, "id", htblColNameType);

// Insert data into the table
Hashtable<String, Object> htblColNameValue = new Hashtable<>();
htblColNameValue.put("id", 2343432);
htblColNameValue.put("name", "Ahmed Noor");
htblColNameValue.put("gpa", 0.95);
dbApp.insertIntoTable(strTableName, htblColNameValue);

// Create an index
dbApp.createIndex(strTableName, "gpa", "GPAIndex");

// Select records using an SQL-like query
SQLTerm[] arrSQLTerms = new SQLTerm[1];
arrSQLTerms[0]._strTableName = "Student";
arrSQLTerms[0]._strColumnName = "gpa";
arrSQLTerms[0]._strOperator = "=";
arrSQLTerms[0]._objValue = 0.95;

Iterator resultSet = dbApp.selectFromTable(arrSQLTerms, new String[0]);
```

## Key Classes & Methods

- **DBApp.java**: The main class that implements core functionality including `createTable`, `insertIntoTable`, `updateTable`, `deleteFromTable`, and `createIndex`.
- **B+ Tree Index**: The engine integrates an open-source B+ tree implementation for index management.
- **Page Management**: Data is split into pages to ensure efficient storage and retrieval, with delayed loading and eviction from memory as needed.

Collaborators: Youssef Elshamy, Abdelrahman Mohammed, Omar Abdelhalim, Manuella Ehab, Radwa Ibrahim, Jana Zein


