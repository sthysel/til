Here's a handy PostgreSQL feature for testing things such as migrations,
data munging scripts, etc.

When you create a new database, it can be created from a template
database. This is usually a lot faster than remaking the database from
scratch.

For example:

  createdb -O myuser -T myapp myapp2
  DBNAME=myapp2 django-admin my_script
  dropdb myapp2

You can also rename databases with psql:

  echo "alter database myapp rename to myapp_template;" | psql postgres


References:

https://www.postgresql.org/docs/9.5/static/app-createdb.html
https://www.postgresql.org/docs/9.5/static/sql-createdatabase.html
https://www.postgresql.org/docs/9.5/static/sql-alterdatabase.html
