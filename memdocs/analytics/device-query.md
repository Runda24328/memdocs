---
# required metadata

title: Device query in Microsoft Intune
description: Learn how to gain on-demand information about the state of your devices using device query.
keywords: 
ms.author: smbhardwaj
author: smritib17 
manager: dougeby
ms.date: 02/01/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Elizabeth cox 
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier2
- M365-identity-device-management
---

# Device query

Device query allows you to quickly gain on-demand information about the state of your devices. When you enter a query on a selected device, Device query runs a query in real time. The data returned can then be used to respond to security threats, troubleshoot the device, or make business decisions.

## Prerequisites

To use Device query in your tenant, you must have a license that includes Microsoft Intune Advanced Analytics. Advanced Analytics features are available with:

- The Intune Advanced Analytics Add-on
- Microsoft Intune Suite

To use Device query on a device, the device must be enrolled in Endpoint Analytics. Learn [how to enroll a device in Endpoint Analytics](enroll-intune.md).

For a user to use Device query, you must assign the **Managed Devices** - **Query** permission to them.  

To use Device query, devices must be Intune managed and corporate owned.

## Supported platforms

Device query is currently only supported on devices running Windows 10 and later.

## How to use Device query

To use Device query, navigate to **Devices** and select the device on which you want to use Device query. Select **Device Query** under the **Monitor** section.

The supported properties you can query are listed in the **Properties** section. To run a query, enter a Kusto Query Language (KQL) query, and select **Run**. Results are displayed in the **Results** tab area.

For more information on Kusto Query Language, see [Learn more about Kusto Query Language](/azure/data-explorer/kusto/query/).

## Supported Operators  

Device query supports only a subset of the operators supported in the Kusto Query Language (KQL). The following operators are currently supported:

[Table operators](#table-operators)

[Scalar operators](#scalar-operators)

[Aggregation functions](#aggregation-functions)

[Scalar functions](#scalar-functions)

### Table operators

Table operators can be used filter, summarize, and transform data streams. Currently the following operators are supported:

|Table operators|Description|
|---|---|
|count|Returns a table with a single record containing the number of records|
|distinct|Produces a table with the distinct combination of the provided columns of the input table|
|join|Merge the rows of two tables to form a new table by matching row for the same device|
|order by|Sort the rows of the input table into order by one or more columns|
|project|Select the columns to include, rename or drop, and insert new computed columns|
|take|Return up to the specified number of rows|
|top|Returns the first N records sorted by the specified columns|
|where|Filters a table to the subset of rows that satisfy a predicate|

### Scalar operators

The following table summarizes operators:

|Operators|Description|Example
|---|---|---|
|==|Equal|`1 == 1, 'aBc' == 'AbC'`|
|!=|Not Equal|`1 != 2, 'abc' != 'abcd'`|
|< |Less|`1 < 2, 'abc' < 'DEF'`|
|> |Greater|`2 > 1, 'xyz' > 'XYZ'`|
|<=|Less or Equal|`1 <= 2, 'abc' <= 'abc'`|
|>=|Greater or Equal|`2 >= 1, 'abc' >= 'ABC'`|
|+|Add|`2 + 1, now() + 1d`|
|-|Subtract|`2 - 1, now() - 1h`|
|*|Multiply|`2 * 2`|
|/|Divide|`2 / 1`|
|%|Modulo|`2 % 1`|
|like|Left Hand Side (LHS) contains a match for Right Hand Side (RHS)|`'abc' like '%B%'`|
|!like|LHS doesn't contain a match for RHS|`'abc' !like '_d_'`|
|contains|RHS occurs as a subsequence of LHS|`'abc' contains 'b'`|
|!contains|RHS doesn't occur in LHS|`'team' !contains 'i'`|
|startswith|RHS is an initial subsequence of LHS|`'team' startswith 'tea'`|
|!startswith|RHS isn't an initial subsequence of LHS|`'abc' !startswith 'bc'`|
|endswith|RHS is a closing subsequence of LHS|`'abc' endswith 'bc'`|
|!endswith|RHS isn't a closing subsequence of LHS|`'abc' !endswith 'a'`|
|and|True if and only if RHS and LHS are true|`(1 == 1) and (2 == 2)`|
|or|True if and only if RHS or LHS is true|`(1 == 1) or (1 == 2)`|

### Aggregation functions

Aggregation functions can be used with the summarize table operator to calculate summarized values. Currently the following aggregation functions are supported:

|Function|Description|
|---|---|
|avg()|Returns the average of the values across the group|
|count()|Returns a count of the records per summarization group|
|countif()|Returns a count of rows for which Predicate evaluates to true|
|dcount()|Returns the number of distinct values in the group|
|max()|Returns the maximum value across the group|
|maxif()|Starting in version 2107, you can use [maxif](/azure/data-explorer/kusto/query/maxif-aggfunction) with the summarize table operator. <!--9966861--> </br></br>Returns the maximum value across the group for which *Predicate* evaluates to `true`. |
|min()|Returns the minimum value across the group|
|minif()|Starting in version 2107, you can use [minif](/azure/data-explorer/kusto/query/minif-aggfunction) with the summarize table operator. <!--9966861--> </br></br>Returns the minimum value across the group for which *Predicate* evaluates to `true`. |
|percentile()|Returns an estimate for the specified nearest-rank percentile of the population defined by Expr|
|sum()|Returns the sum of the values across the group|
|sumif()|Returns a sum of Expr for which Predicate evaluates to true|

### Scalar functions

Scalar functions can be used in expressions. Currently the following scalar functions are supported:

|Function|Description|
|---|---|
|ago()|Subtracts the given timespan from the current UTC clock time|
|bin()|Rounds values down to many datetime multiple of a given bin size|
|case()|Evaluates a list of predicates and returns the first result expression whose predicate is satisfied|
|datetime_add()|Calculates a new datetime from a specified datepart multiplied by a specified amount, added to a specified datetime|
|datetime_diff()|Calculates the difference between two date time values|
|iif()|Evaluates the first argument and returns the value of either the second or third arguments depending on whether the predicate evaluated to true (second) or false (third)|
|indexof()|Function reports the zero-based index of the first occurrence of a specified string within input string|
|isnotnull()|Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a non-null value|
|isnull()|Evaluates its sole argument and returns a Boolean value indicating if the argument evaluates to a null value|
|now()|Returns the current UTC clock time|
|strcat()|Concatenates between 1 and 64 arguments|
|strlen()|Returns the length, in characters, of the input string|
|substring()|Extracts a substring from a source string starting from some index to the end of the string|
|tostring()|Converts input to a string representation|

## Supported Properties

Device query supports the following entities. To learn more about what properties are supported for each entity, see [Intune Data Platform Schema](data-platform-schema.md).

- BiosInfo

- Certificate

- Cpu

- DiskDrive

- EncryptableVolume

- FileInfo

- LocalGroup

- LocalUserAccount

- LogicalDrive

- MemoryInfo

- OsVersion

- Process

- SystemEnclosure

- SystemInfo

- Tpm

- WindowsAppCrashEvent

- WindowsDriver

- WindowsEvent

- WindowsQfe

- WindowsRegistry

- WindowsService

## Known limitations

- The result string of any query is limited to 148 K characters. If the result of your query is longer than 148 K characters, the result is truncated. An error message informs you about how many rows are truncated.  

- You can only send 15 queries a minute. If you run into a **query limit exceeded** error, wait for a minute and try again.  

- Query inputs have a length limit of 2048 characters. If you encounter a *query too long* error, then refine your query to have fewer characters and try again.

- The now() scalar function doesn't support the offset parameter.

- The input window auto-recommends double quotes when only single quotes are supported on the following operators:
  - contains
  - !contains
  - startswith
  - !startswith
  - endswith

- The WindowsRegistry entity fails to return the RegistryKey for root.

- The WindowsRegistry entity fails to return 64-bit shared registry keys.

- The WindowsRegistry entity fails to return binary ValueData.  

- If you’re querying devices that are running on Windows 10, they must be on a minimum quality version.

  - If running Windows 10 21H2, ensure that it's running version 10.0.19044.3393.  

  - If running Windows 10 22H2, ensure that it's running version 10.0.19045.3393.

- If there are multiple network cards available on the machine, then only the first configured domain is returned.

- If TPM 2.0 is present on the device, then activated and enabled is always returned as TRUE.

- If a file is currently in use on the machine, then FileInfo queries returns an error.

## Next Steps

For more information, go to:

- [What is Intune Advanced Analytics](advanced-endpoint-analytics.md)
