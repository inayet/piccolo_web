# Why use an ORM?

## Benefits of an ORM

### Convenience

...

### Passing around partial queries

With Piccolo, you can pass around queries, and keep on chaining methods onto it.

```python
query = Pokemon.select('name')

if some_param == True:
    query = query.where(Pokemon.power >= 100)

results = await query.run()
```

Doing this with raw SQL strings quickly becomes unmanageable.

### Migrations

One of the most useful things an ORM comes bundled with is migrations. Handling migrations manually can be tedious and error prone.

## Downsides of an ORM

ORMs aren't without their issues.

### Performance

When you use an ORM, there is inevitable extra overhead in generating the SQL.

You'll sometimes hear people complain that an ORM generates inefficient SQL. This is usually only for very complex queries.

There's nothing wrong with writing raw SQL, but with Piccolo it means you don't have to write it 90% of the time.

Piccolo also makes it easy to see the SQL being executed - just print any query.

### Can be tedious to learn

A lot of ORMs have their own terminology which doesn't match closely to SQL.

Over time, learning an ORM can feel tedious - you know SQL, but you're having to re-learn concepts over and over for each ORM you use.

### Some database features aren't available

The Piccolo ORM covers the most common interactions an app will have to make with a database.

In cases where it's not possible, you can just drop down into raw SQL.

Trying to encapsulate every possible database features within an ORM is very challenging, and can lead to an unmanageable code base.