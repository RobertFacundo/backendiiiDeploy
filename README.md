# Data Generation and Management Project

This project contains several essential endpoints for generating and storing data in the database. The main ones are:

### 1. **`/api/mocks/mockingpets`**  
Generates a set of random pets using the faker.js package to simulate attributes such as name, species, breed, age, and adoption status.

### 2. **`/api/mocks/mockingusers`**  
Generates a set of random users, assigning a first name, last name, email, and an encrypted password. A role (admin or user) is also assigned, and a pet field is left empty.

### 3. **`/api/mocks/generateData`**  
Allows inserting the specified number of users and pets into the database according to the parameters in the request. The generated data is inserted into the corresponding collections in MongoDB.

## Additional Features (implemented in previous class challenges)

### Logger and Error Logging  
The project also implements a logger system to record key events and errors during server operation. These logs facilitate debugging by providing a detailed track of actions such as data insertion into the database or the execution of specific functions.

### Error Handling Middleware  
Additionally, custom error-handling middlewares have been integrated to manage any issues during data generation or interactions with the database. These middlewares capture and respond with clear and consistent messages, enhancing the server's robustness and the developer experience when facing errors.

#### PRE-DELIVERY CHANGES 
I changed my local database connection and updated the main JS file with the MongoDB Atlas database.
Additionally, I modified the command to run the application => "start": "node src/app.js".

--------------------------

## Practical Activity Towards Final Project Delivery

### Implementation of Swagger and YAML Files

Swagger has been integrated to facilitate the documentation and testing of our API. The YAML configuration files (within the /docs directory) are used to define and structure the API documentation clearly, describing each endpoint, parameters, responses, and potential errors. These files are used by Swagger to automatically generate the interactive user interface and ensure the API is easily accessible and understandable.

The corresponding URL is => https://backendiiideploy.onrender.com/docs/    //* let it load *//

### Test Implementations (Mocha, Chai)

`Users.test.js`: Includes tests for the user model using an in-memory database with MongoMemoryServer. The tests cover the creation of a new user, ensuring that it is created with an empty pet array by default, and retrieving a user by their email.

`chaiTest.test.js`: Implements the same tests as Users.test.js but uses the Chai assertion library for a more readable and structured syntax. It also adds tests for updating and deleting a user, verifying that these actions are performed correctly in the database.

`bcryptTest.test.js`: Includes tests to verify the correct functioning of bcrypt in the password hashing and comparison process. It ensures that the hashed password is different from the original value and that password comparison works correctly, both when they match and when they do not.

`useDtoTest.test.js`: Tests transformations applied to the UserDTO objects. The tests verify that the first name and last name are merged into a single "name" property and that unnecessary properties like password, first_name, and last_name are properly removed during the object transformation.

`superTestPets.test.js`: Includes tests for the pet endpoints and tests to create a pet with an image.

- POST /api/pets/withimage - Create a pet with an image
This tests the process of creating a pet, but with an attached image. The image is read from a local path (../public/img/test-image.jpg) and sent as part of the request using the .attach() method. It verifies that the pet is created correctly with the image and that the image is present in the response.

For proper test execution, we are using mongodb-memory-server, a dependency that allows creating an in-memory MongoDB instance to perform isolated tests without affecting a real database.

## Project Restructuring and New Features
Instead of using models related to "adoption" and "pets," a product model has been incorporated to manage items in an online catalog.

The restructuring includes the creation of the necessary abstraction levels to handle products, such as DAO, services, and controllers. Additionally, routes have been implemented to interact with products through an API.

### Available Routes // Example POST Route to Create a Product
https://backendiiideploy.onrender.com/api/products 

{
    "name": "Laptop Gaming",
    "description": "Potente laptop con GPU dedicada",
    "price": 1500,
    "stock": 10,
    "category": "Electronics",
    "imageUrl": "https://example.com/laptop.jpg"
}

----------------------
Additionally, a cart field was added to the creation of a new user, allowing the user to add and remove products from their cart.

POST https://backendiiideploy.onrender.com/api/users/:uid/cart/:pid
DELETE https://backendiiideploy.onrender.com/api/users/:uid/cart/:pid

### Document Upload
POST /:uid/documents allows users to upload documents and images. Files are processed with multer, stored in the products or documents folders depending on the file type, and associated with the corresponding user in a subfolder with the userId. Upon success, the uploaded documents are returned, or an error message if no files were uploaded or a database issue occurred.

### Tests and Documentation
The following scripts test all functionalities and routes for products, sessions, and users:

    "userTest": "mocha tests/Users.test.js",
    "testProduct":"mocha tests/productsTest.test.js",
    "sessionstest": "mocha tests/sessionsTest.test.js",
    "cartsTest": "mocha tests/Carts.test.js"

The relevant documentation for products, users, and carts can be found in the files
`products.yaml`
`users.yaml`
`carts.yaml`

You can verify the Swagger documentation URL at => https://backendiiideploy.onrender.com/docs/
To facilitate endpoint verification, I provide sample values from the database =>
- uid = 67b773fda16a5f85687c83f3
- pid = 67b74d829266981086180ab1

To perform login =>
{
  "email": "user8.test@example.com",
  "password": "123"
}

### Handlebars
For better presentation, rendering with Handlebars has been added where a user can register, log in, view a home page with their cart and products from the database; on this home page, the user can add products to their cart and view them.

## Docker Image

The Docker image for this project is available on Docker Hub:

[Docker Hub - robertfacundo/ecommerce-app](https://hub.docker.com/repository/docker/robertfacundo/ecommerce-app/general)

To run the image =>

docker pull robertfacundo/ecommerce-app
docker run -p 8080:8080 robertfacundo/ecommerce-app

-------------------------------------------------

### Acknowledgments

I would like to express my gratitude to my tutors and professors in the course.

This project is the result of the knowledge gained during the course and represents my commitment to continue growing in the wonderful world of web development.

I am currently actively seeking my first job as a web developer, an opportunity that would not only mark my entry into the IT world but would also represent a significant change in my life.

To my tutors and professors => Since you are already part of the IT sector, you might be aware of job openings or know people looking for emerging talent. Any recommendations or advice would be invaluable to me, and I would be deeply grateful for your support at this early stage of my career.

If you would like to know more about my work, I invite you to visit my personal portfolio, where you will find other projects I have worked on, my technical skills, and more information about me as a professional in development.

Portfolio: https://robertfacundo.netlify.app/

Feel free to contact me if you have any opportunity or recommendation!

Thank you for taking the time to get here.

Sincerely,

Facundo Robert



**Creado por:**  
Facundo Robert