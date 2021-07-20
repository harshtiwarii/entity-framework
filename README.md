# entity-framework
EF Core is a modern object-database mapper for .NET. It supports LINQ queries, change tracking, updates, and schema migrations. EF Core works with SQL Server, Azure SQL Database, SQLite, Azure Cosmos DB, MySQL, PostgreSQL, and other databases through a provider plugin API.

Installation
EF Core is available on NuGet. Install the provider package corresponding to your target database. See the list of providers in the docs for additional databases.

dotnet add package Microsoft.EntityFrameworkCore.SqlServer
dotnet add package Microsoft.EntityFrameworkCore.Sqlite
dotnet add package Microsoft.EntityFrameworkCore.Cosmos
Use the --version option to specify a preview version to install.

Daily builds
We recommend using the daily builds to get the latest code and provide feedback on EF Core. These builds contain latest features and bug fixes; previews and official releases lag significantly behind.

Basic usage
The following code demonstrates basic usage of EF Core. For a full tutorial configuring the DbContext, defining the model, and creating the database, see getting started in the docs.

using (var db = new BloggingContext())
{
    // Inserting data into the database
    db.Add(new Blog { Url = "http://blogs.msdn.com/adonet" });
    db.SaveChanges();

    // Querying
    var blog = db.Blogs
        .OrderBy(b => b.BlogId)
        .First();

    // Updating
    blog.Url = "https://devblogs.microsoft.com/dotnet";
    blog.Posts.Add(
        new Post
        {
            Title = "Hello World",
            Content = "I wrote an app using EF Core!"
        });
    db.SaveChanges();

    // Deleting
    db.Remove(blog);
    db.SaveChanges();
}
Build from source
Most people use EF Core by installing pre-build NuGet packages, as shown above. Alternately, the code can be built and packages can be created directly on your development machine.

Contributing
We welcome community pull requests for bug fixes, enhancements, and documentation. See How to contribute for more information.

Getting support
If you have a specific question about using these projects, we encourage you to ask it on Stack Overflow. If you encounter a bug or would like to request a feature, submit an issue. For more details, see getting support.

Microsoft.Data.Sqlite
latest version preview version downloads

Microsoft.Data.Sqlite is a lightweight ADO.NET provider for SQLite. The EF Core provider for SQLite is built on top of this library. However, it can also be used independently or with other data access libraries.

Installation
The latest stable version is available on NuGet.

dotnet add package Microsoft.Data.Sqlite
Use the --version option to specify a preview version to install.

Daily builds
We recommend using the daily builds to get the latest code and provide feedback on Microsoft.Data.Sqlite. These builds contain latest features and bug fixes; previews and official releases lag significantly behind.

Basic usage
This library implements the common ADO.NET abstractions for connections, commands, data readers, and so on. For more information, see Microsoft.Data.Sqlite on Microsoft Docs.

using (var connection = new SqliteConnection("Data Source=Blogs.db"))
{
    connection.Open();

    var command = connection.CreateCommand();
    command.CommandText = "SELECT Url FROM Blogs";

    using (var reader = command.ExecuteReader())
    {
        while (reader.Read())
        {
            var url = reader.GetString(0);
        }
    }
}
Build from source
Most people use Microsoft.Data.Sqlite by installing pre-build NuGet packages, as shown above. Alternately, the code can be built and packages can be created directly on your development machine.

Contributing
We welcome community pull requests for bug fixes, enhancements, and documentation. See How to contribute for more information.

Getting support
If you have a specific question about using these projects, we encourage you to ask it on Stack Overflow. If you encounter a bug or would like to request a feature, submit an issue. For more details, see getting support.

See also
Documentation
Roadmap
Weekly status updates
Release planning process
How to write an EF Core provider
Security
Code of conduct.
