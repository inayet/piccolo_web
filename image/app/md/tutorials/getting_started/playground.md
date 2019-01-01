# Playground

Piccolo ships with a handy command called `playground`, which is a great way to learn the basics.

<pre><code class="language-bash">
piccolo playground --help

</code></pre>

It will create an example schema for you, and populate it with data, then launches an [iPython](https://ipython.org/) shell.

You can follow along with the tutorials without first learning advanced concepts like migrations.

It's a nice place to experiment with querying / inserting / deleting data using Piccolo, no matter what stage you're at.

<em>Each time you launch the playground it flushes out the existing tables and rebuilds them, so don't use it for anything permanent!</em>

## Create database

By default the playground expects a local database to exist with the following credentials:

<pre><code class="language-bash">
user: "piccolo"
password: "piccolo"
host: "localhost"  # or 127.0.0.1
database: "piccolo_playground"
port: 5432

</code></pre>

You can create a database using [pgAdmin](https://www.pgadmin.org/).

If you want to use different credentials, you can pass them into the `playground` command (TODO).