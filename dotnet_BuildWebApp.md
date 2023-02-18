# Dating App

## List of Commands

```
dotnet dev-certs https --trust
```

allows browser to trust the certificate provided by .NET sdk

```
dotnet watch run
```

- in place of `dotnet run` , automatically detects a change in a file and then automatically rebuild and run the application

  

## Controller

* controller provides routing end point for application

### Controller class

* ```C#
  namespace API.Controllers
  {
      [ApiController]
      [Route("[controller]")]
      public class WeatherForecastController : ControllerBase
      {
          private static readonly string[] Summaries = new[]
          {
              "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
          };
  
          private readonly ILogger<WeatherForecastController> _logger;
  
          public WeatherForecastController(ILogger<WeatherForecastController> logger)
          {
              _logger = logger;
          }
  
          [HttpGet]
          public IEnumerable<WeatherForecast> Get()
          {
              var rng = new Random();
              return Enumerable.Range(1, 5).Select(index => new WeatherForecast
              {
                  Date = DateTime.Now.AddDays(index),
                  TemperatureC = rng.Next(-20, 55),
                  Summary = Summaries[rng.Next(Summaries.Length)]
              })
              .ToArray();
          }
      }
  }
  ```

  

  * ` [Route("[controller]")]` is  a placeholder.  It gets replaced by the first part (**WeatherForecast**) of the controller name `WeatherForecastController`
    * https://localhost:5001/weatherforecast

### Controller endpoint

* ```C#
          [HttpGet]
          public IEnumerable<WeatherForecast> Get()
          {
              var rng = new Random();
              return Enumerable.Range(1, 5).Select(index => new WeatherForecast
              {
                  Date = DateTime.Now.AddDays(index),
                  TemperatureC = rng.Next(-20, 55),
                  Summary = Summaries[rng.Next(Summaries.Length)]
              })
              .ToArray();
          }
  ```



## Logging

### appsettings.Development.json

* contains configurable app settings for the environment specified in launch settings

  ```c#
  {
    "Logging": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft": "Information",  //changed from Warning to Information to get more logging info for the application
        "Microsoft.Hosting.Lifetime": "Information"
      }
    }
  }
  
  ```



### launchSettings.json

* notably has the **environmentVariables** setting specifies the environment name

* ```C#
  {
    "$schema": "http://json.schemastore.org/launchsettings.json",
    "iisSettings": {
      "windowsAuthentication": false,
      "anonymousAuthentication": true,
      "iisExpress": {
        "applicationUrl": "http://localhost:28628",
        "sslPort": 44397
      }
    },
    "profiles": {
      "IIS Express": {
        "commandName": "IISExpress",
        "launchBrowser": true,
        "launchUrl": "swagger",
        "environmentVariables": {
          "ASPNETCORE_ENVIRONMENT": "Development"
        }
      },
      "API": {
        "commandName": "Project",
        "dotnetRunMessages": "true",
        "launchBrowser": true,
        "launchUrl": "swagger",
        "applicationUrl": "https://localhost:5001;http://localhost:5000",
        "environmentVariables": {
          "ASPNETCORE_ENVIRONMENT": "Development"  //enviroment specified
        }
      }
    }
  }
  ```



## Startup

### ConfigureServices

```C#
        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {

            services.AddControllers();
            services.AddSwaggerGen(c =>
            {
                c.SwaggerDoc("v1", new OpenApiInfo { Title = "API", Version = "v1" });
            });
        }
```

* aka **Dependency Injection Container** - if you want to make available a class or service to other areas in the application you would add them to this container

### Configure (middleware)

* used to configure the HTTP request pipeline - request goes through a series of middleware on way in and way out
* Middleware - 
  *  It’s sometimes called plumbing, as it connects two applications together so data and databases can be easily passed between the “pipe.” Using middleware allows users to perform such requests as submitting forms on a web browser, or allowing the web server to return dynamic web pages based on a user’s profile.

```C#
        // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
        public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
        {
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
                app.UseSwagger();
                app.UseSwaggerUI(c => c.SwaggerEndpoint("/swagger/v1/swagger.json", "API v1"));
            }

            app.UseHttpsRedirection();

            app.UseRouting();

            app.UseAuthorization();

            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();
            });
        }
```

* Middleware in Configure class - 
  * **checks if development mode** - if problem DeveloperExceptionPage
  * **HttpsRedirection** - http address gets redirected to Https
  * **UseRouting** - browser to weatherforecast controller
  * **UseAuthorization** - checks authorization
  * **UseEndpoints** - 
    * **MapControllers** - looks at controllers and see what endpoints are available (e.g. HttpGet)



## Entity Framework

### What Is It?

#### Object Relational Mapper

* it is an **Object Relational Mapper** (ORM)

  * [Object-Relational Mapping](https://en.wikipedia.org/wiki/Object-relational_mapping) (ORM) is a technique that lets you query and manipulate data from a database using an object-oriented paradigm. When talking about ORM, most people are referring to a *library* that implements the Object-Relational Mapping technique, hence the phrase "an ORM".

    An ORM library is a completely ordinary library written in your language of choice that encapsulates the code needed to manipulate the data, so you don't use SQL anymore; you interact directly with an object in the same language you're using.

  * ORM Libraries:
    * Java: [Hibernate](https://en.wikipedia.org/wiki/Hibernate_(Java)).
    * PHP: [Propel](https://en.wikipedia.org/wiki/Propel_(PHP)) or [Doctrine](https://en.wikipedia.org/wiki/Doctrine_(PHP)) (I prefer the last one).
    * Python: the Django ORM or [SQLAlchemy](https://en.wikipedia.org/wiki/SQLAlchemy) (My favorite ORM library ever).
    * C#: [NHibernate](https://en.wikipedia.org/wiki/NHibernate) or [Entity Framework](https://en.wikipedia.org/wiki/Entity_Framework)
  * More info: https://stackoverflow.com/questions/1279613/what-is-an-orm-how-does-it-work-and-how-should-i-use-one

* Translates our code into SQL commands that update our tables in the database

* Replaces cumbersome process of having to always have to open a connection to the database, fetch the database, etc. whenever you need to interact with the DB

#### Use-case and Features

![image-20211116212318011](C:\Users\PJMLEARNER\AppData\Roaming\Typora\typora-user-images\image-20211116212318011.png)

* AppUser Class
* Add Entity Framework
  * create a class that derives from the DbContext class that comes with Entity Framework
    * this class acts as a bridge between Entity classes and the Database

* Entity Framework Features
  * Query - using LINQ
  * Change Tracking
  * Saving - saves to the DB (DbContext has save changes method)
  * Concurrency
  * Transactions
  * Caching - repeated querying will return from the cache
  * Built-in conventions - default rules that automatically configures the Entity Framework schema/model
  * Configurations - ways to override the conventions
  * Migrations - automatically generate db

### Installation

* Steps to use NuGet to install

  * install NuGet from Extensions
  * CMD + Shift + P => Show All Commands
  * Search for Nuget
  * Within NuGet search for Microsoft.EntityFrameworkCore.Sqlite
  * flag API.csproj install > install

* view API.csproj file

  * Package Reference is now added to item group

    ```c#
      <ItemGroup>
        <PackageReference Include="Microsoft.EntityFrameworkCore.Sqlite" Version="5.0.12" />
      </ItemGroup>
    ```

### DbContext class

```C#
namespace API.Data
{
    public class DataContext : DbContext
    {
        public DataContext(DbContextOptions options) : base(options)
        {
        }

        public DbSet<AppUser> Users { get; set; }
    }
}
```



* DbSet
  *   Can be used to query and save instances of an Entity. LINQ queries against a DbSet will be translated into queries against the database.

#### Services Injection of DbContext Class

* we inject DbContext class (DataContext) in <u>Startup</u> services so that we can use it anywhere in our application

  ```C#
          public void ConfigureServices(IServiceCollection services)
          {
              //injection
              services.AddDbContext<DataContext>(options =>  //lambda - parameter
              {
                  options.UseSqlite("Connection string");  //lambda - expression
              });
          }
  ```

  

* lambda - passing an expression as a parameter

  

### Connection String

#### appSettings

* Add the connection string to the json configuration file - appSettings (we have two, because no credentials will use appSettings.Development.json)

* ```C#
  {
    "ConnectionStrings" : {
      "DefaultConnection": "Data source=dataingapp.db"
    },
    "Logging": {
      "LogLevel": {
        "Default": "Information",
        "Microsoft": "Information",
        "Microsoft.Hosting.Lifetime": "Information"
      }
    }
  }
  ```

#### Startup

```C#
        private readonly IConfiguration _config;
        public Startup(IConfiguration config)
        {
            _config = config;
        }

        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddDbContext<DataContext>(options => 
            {
                options.UseSqlite(_config.GetConnectionString("DefaultConnection"));
            });
        }
```



### Migrations

* what this does is take our entities and creates the folder Migrations and will have code that will automatically create our entities as Db objects



## Adding a new API Controller

* to get data from our Database, we use Dependency Injection

  ```C#
  using System;
  using System.Collections.Generic;
  using System.Linq;
  using System.Threading.Tasks;
  using API.Data;
  using API.Entities;
  using Microsoft.AspNetCore.Mvc;
  
  namespace API.Controllers
  {
      [ApiController]
      [Route("api/[controller]")]
      public class UsersController : ControllerBase
      {
          private readonly DataContext _context;
  
          public UsersController(DataContext context)
          {
              _context = context;
          }
  
          [HttpGet]
          public ActionResult<IEnumerable<AppUser>> GetUsers()
          {
              return _context.Users.ToList();
          }
          [HttpGet("{id}")]
          public ActionResult<AppUser> GetUser(int id)
          {
              return _context.Users.Find(id);;
          }
          
      }
  }
  ```

  

## Asynchronous Code

* With synchronous code a request that goes out will use a thread and any other request can potentially be blocked if the initial request is not yet fulfilled.  Asynchronous code helps to resolve this issue as is used for scaling (helps to run when application/database becomes large)

  ```C#
          [HttpGet]
          public async Task<ActionResult<IEnumerable<AppUser>>> GetUsers()
          {
              return await _context.Users.ToListAsync();
          }
          [HttpGet("{id}")]
          public async Task<ActionResult<AppUser>> GetUser(int id)
          {
              return await _context.Users.FindAsync(id);;
          }
  ```

  

  * `asnyc` - keyword needs to be specified before the method
  * `Task<>` - Task is used to wrap around the method in angle brackets
  * `await` - await operator is needed
  * `ToListAsync` and `FindAsync` - need to use the Async methods for each of these methods