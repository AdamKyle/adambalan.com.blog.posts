Ice Cream Database is a very simple connector to a database that returns, at the end of the day, a PDO object.

I really wanted to understand how PDO works, how database connectors work in frameworks like [Laravel](https://laravel.com/) and [Symfony](https://symfony.com/). I also wanted to keep the complexity to a minimum.

I wanted to keep everything simple. While one might argue this is not a fully flushed out Database connector and that there could be even more abstractions and additions made, I didn't want to over complicate things.

The most important aspect is how we configure the Database Connector:

```php
use IceCreamDatabase\Connect;

// Similar to that of Laravel if you are familiar.
$connections = [
  'mysql' => [
    'host' => '127.0.0.1',
    'port' => 3306,
    'database' => '',
    'username' => 'root',
    'password' => 'root',
    'charset' => 'utf8',
  ],
  'pgsql' => [
    'host' => '127.0.0.1',
    'port' => 5432,
    'dbname' => 'scotchbox',
    'username' => 'root',
    'password' => 'root',
    'charset' => 'utf8',
  ],
  'sqlite' => [
    'temp_file' => ':memory'
  ]
]

// At this time I have made the choice to only support mysql and pgsql as well as sqlite connections.
// More can be added in the future, simplicity was the game here.

$con = new Connect($connections);
```

You can see more in depth information in the [README](https://github.com/AdamKyle/ice-cream-database). For now we will keep things in this blog post simple.

The above has made a connection to `sqlite`, `pgsql` and `mysql`. You can then get any of the databases by doing:

`$con->db('pgsql')->exec('...');`

Notice how we pass in the db name. This tells the connection manage which database we should connect to.

## Why Did You Build This?

I built it to learn how people abstract the layer between the database and their framework. I wanted to better understand what they were doing and how PDO played a part of it.

I feel that I have a better understanding of this concept now and have, over time, made changes to better suit the needs of this component.

## Is The Component Maintained?

All Ice Cream Components are maintained, although not on a regular or consistent basis, how ever they are maintained and updated every so often. Most of the times its just updating dependencies, running tests and seeing if anything broke.
