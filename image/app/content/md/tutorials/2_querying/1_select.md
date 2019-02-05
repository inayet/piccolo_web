# Select

Using this schema:

```python
from piccolo.table import Table
from piccolo.columns import ForeignKey, Varchar


class Manager(Table):
    name = Varchar(max_length=100)


class Band(Table):
    name = Varchar(max_length=100)
    manager = Varchar(max_length=100)
```

Here are some simple queries:

```python
"""
All of these work with .run() as well inside co-routines.
"""

# To get all rows:
Band.select.run_sync()
[{'id': 1, 'name': 'Pythonistas', 'manager': 1, 'popularity': 1000},
{'id': 2, 'name': 'Rustaceans', 'manager': 2, 'popularity': 500}]


# To get certain rows:
Band.select.columns(Band.name).run_sync()
[{'name': 'Rustaceans'}, {'name': 'Pythonistas'}]


# Or making an alias to make it shorter
b = Band
b.select.columns(b.name).run_sync()
```

The advantage of using column objects over say strings, is your text editor can provide code completion, and a linter can help catch errors.

<em>Following along - install Piccolo and run `piccolo playground`.</em>

## Data returned

You use a select query when you want to get data back in the form of a list of dictionaries (where each dictionary represents a row).

## Columns

By default all columns are returned from the queried table.

```python
b = Band
# Equivalent to SELECT * from band
b.select.run_sync()
```

To restrict the returned columns, used the `columns` method.

```python
b = Band
# Equivalent to SELECT name from band
b.select.columns(b.name).run_sync()
```

The `columns` method is additive, meaning you can chain it to add additional columns.

```python
b = Band
b.select.columns(b.name).columns(b.manager).run_sync()

# Or just define it one go:
b.select.columns(b.name, b.manager).run_sync()
```

## Joins

One of the most powerful things about select is it's support for joins.

```python
b = Band
b.select.columns(
    b.name,
    b.manager.name
).run_sync()
```

The joins can go several layers deep.

```python
c = Concert
c.select.columns(
    c.id,
    c.band_1.manager.name
).run_sync()

```

## Order by

To order the results by a certain column (ascending):

```python
b = Band
b.select.order_by(
    b.name
).run_sync()
```

To order by descending:

```python
b = Band
b.select.order_by(
    b.name,
    ascending=False
).run_sync()
```

You can order by multiple columns, and even use joins:

```python
b = Band
b.select.order_by(
    b.name,
    b.manager.name
).run_sync()
```

## Where clauses

There are lots of different options for where clauses.

### Like

The percentage operator is required to designate where the match should occur.

```python
b = Band
b.select.where(
    b.name.like('Py%')  # Matches the start of the string
).run_sync()

b.select.where(
    b.name.like('%istas')  # Matches the end of the string
).run_sync()

b.select.where(
    b.name.like('%is%')  # Matches anywhere in string
).run_sync()
```

### Not like

Usage is identical to 'like' excepts it excludes matching rows.

```python
b = Band
b.select.where(
    b.name.not_like('Py%')
).run_sync()
```