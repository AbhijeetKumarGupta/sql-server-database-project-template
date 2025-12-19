# SQL Server Database Project Template

A modern SQL Server Database Project template demonstrating best practices for database development using SQL Server Data Tools (SSDT) and .NET build tools.

## 📋 Overview

This project serves as a starter template for SQL Server database development, showcasing:

- **Schema organization** - Proper schema separation
- **Database objects** - Tables, Views, Stored Procedures, and Functions
- **Build and deployment** - Automated .dacpac generation and deployment
- **Version control** - Database schema managed as code

## 🏗️ Project Structure

```
.
├── Schemas/          # Database schemas
│   └── EmployeeSchema.sql
├── Tables/           # Table definitions
│   └── Employees.sql
├── Views/            # Database views
│   └── EmployeeView.sql
├── StoredProcedures/ # Stored procedures
│   └── GetEmployees.sql
├── Functions/        # User-defined functions
│   └── GetEmployeeCount.sql
├── TSQLPOC.sqlproj   # SQL Server Database Project file
└── deploy.sh         # Deployment script
```

## 🚀 Getting Started

### Prerequisites

- [.NET SDK](https://dotnet.microsoft.com/download) (for building the project)
- [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) (local or remote instance)
- [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) (optional, for Visual Studio integration)
- [SqlPackage](https://docs.microsoft.com/sql/tools/sqlpackage/sqlpackage-download) (for deployment)

### Building the Project

Build the database project to generate a `.dacpac` file:

```bash
dotnet build TSQLPOC.sqlproj
```

The output will be generated in `bin/Debug/TSQLPOC.dacpac`.

### Deploying to SQL Server

#### Using the Deployment Script

1. Update the connection details in `deploy.sh`:

   - `TargetServerName`: Your SQL Server instance
   - `TargetDatabaseName`: Target database name
   - `TargetUser`: SQL Server username
   - `TargetPassword`: SQL Server password

2. Make the script executable and run it:
   ```bash
   chmod +x deploy.sh
   ./deploy.sh
   ```

#### Manual Deployment

Deploy using SqlPackage directly:

```bash
sqlpackage /Action:Publish \
    /SourceFile:bin/Debug/TSQLPOC.dacpac \
    /TargetServerName:localhost,1433 \
    /TargetDatabaseName:YourDatabase \
    /TargetUser:sa \
    /TargetPassword:YourPassword \
    /TargetEncryptConnection:False
```

## 📦 Database Objects

### Schema

- **Employee** - Schema for employee-related objects

### Tables

- **Employee.Employee** - Main employee table with:
  - `EmployeeId` (INT, Primary Key, Identity)
  - `FirstName` (NVARCHAR(100))
  - `LastName` (NVARCHAR(100))
  - `Age` (INTEGER)
  - `HireDate` (DATE)

### Views

- **Employee.EmployeeView** - View providing employee information

### Stored Procedures

- **Employee.GetEmployeeInfo** - Retrieves employee information by ID
  - Parameters: `@EmployeeId INT`

### Functions

- **Employee.GetEmployeeAge** - Calculates employee age based on hire date
  - Parameters: `@EmployeeId INT`
  - Returns: `INT`

## 🛠️ Development Workflow

1. **Make Changes** - Edit SQL files in their respective directories
2. **Build** - Run `dotnet build` to validate and generate .dacpac
3. **Deploy** - Use `deploy.sh` or SqlPackage to deploy changes
4. **Version Control** - Commit changes to track schema evolution

## 📝 Best Practices

- **Schema Organization** - Group related objects under appropriate schemas
- **Naming Conventions** - Use consistent naming (PascalCase for objects)
- **Version Control** - Always commit schema changes
- **Testing** - Test deployments in development before production
- **Documentation** - Document complex stored procedures and functions

## 🔧 Configuration

### Project Settings

Edit `TSQLPOC.sqlproj` to customize:

- Project name
- Target SQL Server version
- Collation settings

### Deployment Settings

Modify `deploy.sh` for:

- Connection strings
- Deployment options
- Target environments

## 📚 Resources

- [SQL Server Database Projects Documentation](https://docs.microsoft.com/sql/ssdt/sql-server-database-projects)
- [SqlPackage Documentation](https://docs.microsoft.com/sql/tools/sqlpackage/sqlpackage)
- [DACPAC Deployment Guide](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the build and deployment
5. Submit a pull request

## 📄 License

This project is private and proprietary.
