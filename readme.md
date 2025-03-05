# Book Store Web Application

## Project Overview
This is a **Book Store Web Application** built using **ASP.NET Core MVC** with **N-Tier Architecture**. The project aims to provide an online platform to manage and sell books, including categories, authors, and book information.

## Technologies Used
- ASP.NET Core MVC (.NET 8)
- Entity Framework Core
- SQL Server
- Bootstrap 5
- HTML, CSS
- JavaScript
- jQuery
- Dependency Injection
- Repository Pattern
- N-Tier Architecture
- AutoMapper
- Microsoft Identity

## Architecture
The project follows the **N-Tier Architecture** which consists of three layers:

### 1. Presentation Layer
- ASP.NET Core MVC
- Razor Views
- Bootstrap for UI Design
- JavaScript for client-side interactions

### 2. Business Logic Layer
- Service Layer
- Data Transfer Objects (DTO)
- Business Validation

### 3. Data Access Layer
- Entity Framework Core
- Repository Pattern
- SQL Server Database

## Features
- User Authentication (Login, Register)
- Manage Books (CRUD)
- Manage Categories
- Shopping Cart
- Order Management
- Responsive Design with Bootstrap
- Client-Side Validation
- Pagination
- Search Functionality

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/duongminh318/Bulky_MVC_myweb.git
   ```

2. Navigate to the project folder:
   ```bash
   cd bookstore
   ```

3. Configure the **appsettings.json** file:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=YOUR_SERVER_NAME;Database=BookStoreDB;User Id=sa;Password=YOUR_PASSWORD;"
   }
   ```

4. Apply Migrations:
   ```bash
   dotnet ef database update
   ```

5. Run the application:
   ```bash
   dotnet run
   ```

6. Open the browser and navigate to:
   ```
   http://localhost:5000
   ```

## Folder Structure
```
├── BulkyWeb (Presentation Layer)
├── Bulky.Business (Business Logic Layer)
├── Bulky.DataAccess (Data Access Layer)
└── Bulky.Models (Models & DTOs)
```

## Contributing
Contributions are welcome! Feel free to submit pull requests.

## License
This project is licensed under the MIT License.

## Contact
- Email: duongminh318@gmail.com
- GitHub: https://github.com/duongminh318/Bulky_MVC_myweb