# Product Management System

A RESTful API-based Product Management System built with Spring Boot, providing comprehensive CRUD operations with pagination, sorting, and exception handling capabilities.

## 🚀 Features

- **CRUD Operations**: Create, Read, Update, and Delete products
- **Pagination & Sorting**: Efficient data retrieval with customizable page size and sorting options
- **DTO Pattern**: Clean separation between entity and data transfer objects using ModelMapper
- **Global Exception Handling**: Centralized error handling with custom error responses
- **RESTful API Design**: Well-structured endpoints following REST principles
- **MySQL Database Integration**: Persistent data storage using JPA/Hibernate

## 🛠️ Technology Stack

- **Java 17**
- **Spring Boot 3.3.2**
- **Spring Data JPA**
- **MySQL Database**
- **Lombok** - Reduces boilerplate code
- **ModelMapper 3.2.1** - Object mapping
- **Maven** - Dependency management

## 📋 Prerequisites

Before running this application, ensure you have:

- Java 17 or higher installed
- MySQL Server installed and running
- Maven (or use the included Maven Wrapper)
- Your favorite IDE (IntelliJ IDEA, Eclipse, VS Code)

## ⚙️ Configuration

1. **Database Setup**

   Create a MySQL database:
   ```sql
   CREATE DATABASE rest_api_db;
   ```

2. **Application Properties**

   Update `src/main/resources/application.properties` with your MySQL credentials:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/rest_api_db
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   ```

3. **Database Schema**

   Set `spring.jpa.hibernate.ddl-auto=update` for the first run to auto-create tables, or manually create the product table:
   ```sql
   CREATE TABLE product (
       id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(255),
       description TEXT,
       price DOUBLE,
       quantity INT
   );
   ```

## 🚀 Running the Application

### Using Maven Wrapper (Recommended)

**Linux/Mac:**
```bash
./mvnw spring-boot:run
```

**Windows:**
```bash
mvnw.cmd spring-boot:run
```

### Using Maven

```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## 📡 API Endpoints

### Create Product
```http
POST /save-product
Content-Type: application/json

{
  "name": "Laptop",
  "description": "High-performance laptop",
  "price": 999.99,
  "quantity": 10
}
```

### Get All Products
```http
GET /products
```

### Get Product by ID
```http
GET /product/{id}
```

### Delete Product
```http
DELETE /product/{id}
```

### Get Products with Pagination
```http
GET /page-products?pageNo=0&pageSize=10&sortBy=name&sortDir=asc
```

**Query Parameters:**
- `pageNo` (default: 0) - Page number
- `pageSize` (default: 2) - Number of items per page
- `sortBy` (default: id) - Field to sort by
- `sortDir` (default: asc) - Sort direction (asc/desc)

## 📦 Project Structure

```
src/main/java/com/becoder/
├── config/
│   └── ProjectConfig.java          # Configuration beans
├── controller/
│   └── ProductController.java      # REST endpoints
├── dto/
│   ├── ProductDto.java             # Data Transfer Object
│   ├── ProductResponse.java        # Paginated response wrapper
│   └── ErrorResponse.java          # Error response structure
├── exception/
│   └── GlobalExceptionHandler.java # Centralized exception handling
├── model/
│   └── Product.java                # Entity class
├── repository/
│   └── ProductRepository.java      # JPA repository
└── service/
    ├── ProductService.java         # Service interface
    └── impl/
        └── ProductServiceImpl.java # Service implementation
```

## 🎯 API Response Examples

### Success Response
```json
{
  "id": 1,
  "name": "Laptop",
  "description": "High-performance laptop",
  "price": 999.99,
  "quantity": 10
}
```

### Paginated Response
```json
{
  "products": [...],
  "totalElements": 50,
  "totalPages": 5,
  "isFirst": true,
  "isLast": false,
  "pageNo": 0,
  "pageSize": 10
}
```

### Error Response
```json
{
  "status": 500,
  "message": "You doing operation with Null value"
}
```

## 🔧 Development

### Building the Project
```bash
./mvnw clean install
```

### Running Tests
```bash
./mvnw test
```
