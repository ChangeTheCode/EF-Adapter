# EF-Adapter
Entity Framework Adapter for [Casbin](https://github.com/casbin/casbin). With this library, Casbin can load policy from EF supported database or save policy to it.

This adapter is based on the [EF-Core Adapter](https://github.com/casbin-net/EFCore-Adapter)

The current version supported all databases which EF supported, there is a part list:

- SQL Server 2012 onwards
- SQLite 3.7 onwards
- Azure Cosmos DB SQL API
- PostgreSQL
- MySQL, MariaDB
- Oracle DB
- Db2, Informix
- And more...

## Installation

> Todo

## Simple Example

```csharp
using Casbin.NET.Adapter.EF;
using Microsoft.EntityFramework;
using NetCasbin;
namespace ConsoleAppExample
{
    public class Program
    {
        public static void Main(string[] args)
        {

            var dbConncetionString = "<ConnectionStringOfTheDB>";
            var context = new CasbinDbContext<Guid>(dbConncetionString);

            // Initialize a EF Core adapter and use it in a Casbin enforcer:
            var efCoreAdapter = new CasbinDbAdapter<Guid>(context);
            var e = new Enforcer("examples/rbac_model.conf", efCoreAdapter);

            // Load the policy from DB.
            e.LoadPolicy();

            // Check the permission.
            e.Enforce("alice", "data1", "read");
            
            // Modify the policy.
            // e.AddPolicy(...)
            // e.RemovePolicy(...)
	
            // Save the policy back to DB.
            e.SavePolicy();
        }
    }
}
```

## Getting Help

- [Casbin.NET](https://github.com/casbin/Casbin.NET)

## License

This project is under Apache 2.0 License. See the [LICENSE](LICENSE) file for the full license text.