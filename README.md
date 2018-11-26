# EntityFrameworkPlayground

## Introduction

### What is Entity Framework ?
 
 In order to access a database from your application, you need a persistance framework. The entity framework is an example of a persistance framework.
 
 #### Advantages of such a framework:
 - No more stored procedures need to be written.
 - No need to manage database connections.
 - No need to manual map database tables to objects.

Entity framework takes cares of all of this for you.

### Building a model using the entity framework

#### There are three main workflows for building a model using the EF:

1) **Database First** - We start with the database. We design our tables using visual designer. Then we can use the EF to generate domain classes based on the database.
2) **Code First** - We start with the code. We simply create our domain classes and then have the EF generate the tables for us.
3) **Model First** - We create a UML diagram first and then use the EF to generate the domain classes and database.

### Database First Workflow

### Code First Workflow

Before doing anything else, you need to first install the EF in your app using **Package Manager Console** - ```install-package EntityFramework```.

Create a new class that will represent a table in your database and define all its fields. For example:

```
public class Post
{
  public int Id { get; set; }
  public DateTime DatePublished { get; set; }
  public string Title { get; set; }
  public string Body { get; set; }  
}
```
Now we need to define a **Dbcontext**. This is used to load or save data to a database. For example:
```
public class BlogDbContext : DbContext
{
    public DbSet<Post> Posts { get; set; }
}
```

Next we need to specify the database connection string in order to connect to the database. Go to **App.config** and create a new connectionString element:
```
<connectionStrings>
    <add name="BlogDbContext" connectionString="data source=...."/>
</connectionStrings>
```

We also need to **enable code first migrations**. Go back to Package Manager Console and type ```enable-migrations```.

Now everytime we want to make a change to our model, we start with the code. Everytime a change is made to the model, we need to create a migration. You can do this by going to package manager console and use the command ```add-migration nameOfMigrationHere```. The name represents the kind of change we have made. This as a result will create a new folder called **Migrations**. Inside this folder you will have two generated files:

1) The first file is the migration itself with a date-time stamp.
    - This file will have two methods: 1) Up and 2) Down. The Up method is used to updgrade the database and the second one is used to downgrade the database.

The next step is to actually run the migration
