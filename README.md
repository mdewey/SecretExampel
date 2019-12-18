# Secret Example. 

 This code sample is the most basic example of keep secrets in .NET core.

 _NOTE_: All commands must be run in the project directory



## Set up 

First, we need to init secrets in our code base. 

``` sh
dotnet user-secrets init 
```

This command sets up a secrets reference to your project. 


## Add the secrets to the secrets store

Next, you want to add the actual values. These values are stored on your machine in a plain text, key-value structure. 

``` sh
dotnet user-secrets set "ConnectionString" "server=localhost;database=MyApiDatabase" 
```

The above command will add new key called `ConnectionString` with the value:`server=localhost;database=MyApiDatabase`

## Using the value

To get a value, we must use [dependency injection](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-3.1). That is because our server is loading the configuration when the server starts. This configuration is accessible in our apps when we inject the configuration into our code where needed. 

To use DI in our code, go to the class where the configuration setting is needed and a constructor (or modify the existing one) to accept a parameter of `IConfiguration configuration`. Your constructor should look like this: 


```C# 
public DatabaseContext(IConfiguration configuration)
{
 
}
```

With the configuration being injected we can now access the setting we need by using the the bracket notation. So our full constructor should look like this: 


``` C#
public DatabaseContext(IConfiguration configuration)
{
 this.ConnectionString = configuration["ConnectionString"];
}
```

In this constructor, we are setting a property on our class to the connection string in the configuration. This statement allows us to use `this.ConnectionString` anywhere in this class with the value that is in our user-secrets


## Full example

[Full Example here](https://github.com/mdewey/SecretExampel)


## Read More

Checkout the latest [documentation](https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=linux)