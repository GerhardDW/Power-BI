# Beginning Dax with PBI by Phillip Seamark
-------
## Chapter 1

### What is Dax
- page 2
- functional designed to enhance data modelling (in pbi, power pivot or ssas tabular)
- you use functions to either filter or query results, no similar equivalent to INSERT, UPDATE, DELETE.
- functions can be nested and used as inputs to one another.
- functions use parameters as input and can return a single value (scalar) or table value (many rows and columns).

### What is a data model
- page 3
- a unit of collection of various objects (data, calculations, formatting rules etc) that can be used to explore, query and better understand an existing dataset. The data can be from various sources.
- More basic: its that data and measures.
- data is in the form of tables (similar to database tables)
- calculations (measures over the tables like rowcounts, summing a column values)

### Components of a DAX data model
- page 4 to 5
- 6 key components: (1) Data, (2) Tables, (3) Columns, (4) Relationships, (5) Measures; (6) Hierarchies
- (1) Data: imported data. Can be various types but once imported will be in two dimensional structure called table.
- (2) Tables: to store and organize data.  Made up of the source data or via results DAX Calculations
- (3) Columns: Table have 1 or more; data engine behind DAX stores data in columns, unlike SQL Server which stores in rows. Each column have separate index. Once data is loaded in the column it is static/cannot be changed.
- (4) Relationships: 2 tables can be connected; via 1 column from both; 1-1, 1-*, *-* (recently). used more to provide filtering instead of normalization of OLTP systems.
- (5) Measures: dax calculations; returns single value used in visuals or other measures; can respond to user interaction and recalcs when report used; returns new values based on the updates to the selection of slicers and filters.
- (6) Hierarchies: groupings of columns in a table; used for drilling up and down it.

### Your first DAX calculation
- page 5 to 7
- 3 types: (1) calculated columns, (2) calculated measures, (3) calculated tables.
- Use natural language (spaces etc, avoid underscores and not spaces), when naming.
- a calculated measure can only ever return a single value, not a list or table.

### Formatting
- page 10
- dax studio useful in writing dax. Alternative to using the native formula bar.

### Second & Third DAX calculation
- page 11-12
- second is a calculated column.
- third is a calculated table, can be done by referencing another table or writing dax from scratch and is only available in PBI desktop and SSAS tabular not Excel PowerPivot. When referencing another table, modifications typically flow through to it.
- It is common to use dax calculated tables for summary tables which then can give performance gains if you add calculations to these summary tables.

### Datatypes
- page 13
- Power Query quesses the datatypes upon loading, so beware of configuring correctly.
- Decimal datatype are correct to 15 significant values and the values on the integer side take priority, be aware.
- Date, DateTime, Time also available.

### Operators
- page 18
- 4 sets of operators: 1) arithmetic; 2) comparison; 3) concatenation; 4) logical.
- careful to compare like 1 = '1' will cause error either make sure the one is a string FORMAT(); or integer via VALUE().
- concatenate is &
- and is &&
- there is operator precedence in dax, not necessary to remember by heart but beware, or you can force operator precedence by ().
- important, dax will try to convert both elements to the same type, sometimes it succeeds but is unexpected sometimes it outright fails.

### Relationships
- page 22
- basically allow to tables to be associated with one another.
- mainly for the purpose of two things 1) to automatically filter rows on another table via the relationship 2) to allow calcs to use rows from another table and understand how the rows should be connected
- Types of relationships: 1-* (preferred), 1-1, *-*. (side note: also a directionfilter).
- The value selected will filter through via the filter direction (can then affect others as well).
- trick is to place one-side relationships higher than many-side table to visually help with the trickle down effect of the relationship.
- RELATED() used to fetch values from the many side in a calculated column.
- RELATEDTABLE() used to fetch values from the one side in a calculated column.
- Two tables can have more than one relationship but only 1 active. If you want to use the inactive relationship use: USERELATIONSHIP().

### Hierarchies
- Basically configured on a table to provide column level drilling (you have a starting point in the hierarchy and can drill down to the next level, then to the next etc, then back up to the starting point)
- Not all visuals understand it but most allow it to be the grouping.

----
## Chapter 2: Variables

