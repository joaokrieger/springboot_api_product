# Product Management API
This is a Java Spring Boot project that implements an API for product management. The API follows the Richardson Maturity Model principles and provides HTTP methods for creating, reading, updating, and deleting products.

## Richardson Maturity Model
The API adheres to the Richardson Maturity Model principles and aims to achieve level 3 of the model, which includes the following principles:
- **Resources:** Uses URIs to identify individual resources (products).
- **HTTP Verbs:** Utilizes the correct HTTP verbs (POST, GET, PUT, DELETE) to manipulate resources.
- **HATEOAS:** The API does not achieve level 3 of the model, which involves the use of hypermedia for guiding navigation. However, the framework is designed to be easily extended to include this functionality in the future.

# Request Examples
Here are some examples of how to make requests to the API:

## HTTP GET
### Get All Products

`GET /product`
```bash
curl --location 'http://localhost:8080/products'
```
### Response 200
```bash
[
    {
        "idProduct": "69f22e78-0265-4745-a08f-6acc2868db99",
        "name": "Lavadora LG",
        "value": 1600.00,
        "links": [
            {
                "rel": "self",
                "href": "http://localhost:8080/products/69f22e78-0265-4745-a08f-6acc2868db99"
            }
        ]
    },
    {
        "idProduct": "fff2f36e-4127-4a82-b6ff-add4d6d75183",
        "name": "Monitor Dell 27",
        "value": 5600.00,
        "links": [
            {
                "rel": "self",
                "href": "http://localhost:8080/products/fff2f36e-4127-4a82-b6ff-add4d6d75183"
            }
        ]
    }
]
```


### Get Product By UUID

`GET /product/{id}`
```bash
curl --location 'http://localhost:8080/products/69f22e78-0265-4745-a08f-6acc2868db99'
```
### Response 200
```bash
{
    "idProduct": "69f22e78-0265-4745-a08f-6acc2868db99",
    "name": "Lavadora LG",
    "value": 1600.00,
    "_links": {
        "Products List": {
            "href": "http://localhost:8080/products"
        }
    }
}
```
## HTTP POST
### Insert Product
`POST /product`
```bash
curl --location 'http://localhost:8080/products' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Monitor Dell 27",
    "value": 5600.00
}'
```
### Response 201
```bash
{
    "idProduct": "fff2f36e-4127-4a82-b6ff-add4d6d75183",
    "name": "Monitor Dell 27",
    "value": 5600.00
}
```
## HTTP PUT
### Update Product
`PUT /product`
```bash
curl --location --request PUT 'http://localhost:8080/products/491c4c86-52ac-47e0-b320-333068e3851d' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Monitor Dell 31",
    "value": 7600.00
}'
```
### Response 200
```bash
{
    "idProduct": "491c4c86-52ac-47e0-b320-333068e3851d",
    "name": "Monitor Dell 31",
    "value": 7600.00
}
```
## HTTP DELETE
### Delete Product
```bash
curl --location --request DELETE 'http://localhost:8080/products/491c4c86-52ac-47e0-b320-333068e3851d'
```
### Response 200
```bash
Product deleted successfully
```

# Database Configuration
The application uses PostgreSQL as the database. To configure the database connection, modify the application.properties file located in the src/main/resources directory. Update the following properties with your PostgreSQL database information:
```bash
spring.datasource.url= jdbc:postgresql://localhost:5432/products
spring.datasource.username=postgres
spring.datasource.password=123456
spring.jpa.hibernate.ddl-auto=update

spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
```

# Running the Project
Make sure you have Java and Maven installed on your machine. Follow the steps below to run the project:

1. Clone this repository: git clone https://github.com/joaokrieger/springboot_api_product
1. Navigate to the project directory: cd springboot
1. Run the project using Maven: mvn spring-boot:run
1. The API will be available at: http://localhost:8080
