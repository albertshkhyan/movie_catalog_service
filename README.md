Here's the updated `README.md` with the folder structure tree included:

```markdown
# Movie Catalog Service

## Overview

The **Movie Catalog Service** is a core component of the CineNova movie streaming platform. This service is responsible for managing the movie catalog, handling movie data CRUD operations, movie search functionality, and movie-related metadata. It is built using **Node.js** and **Express.js**, and interacts with **DynamoDB** for storing unstructured movie data. It also integrates with **Elasticsearch** for fast and scalable movie search.

The service follows a **microservices architecture**, with its own isolated database and event-driven interactions with other services like user authentication and subscription/payment services.

---

## Features

- **Movie Management**: Allows CRUD operations for adding, updating, and deleting movie data.
- **Movie Search**: Provides a search functionality for users to find movies based on titles, genres, actors, etc.
- **Elasticsearch Integration**: Powers full-text search for movie metadata like titles, genres, and descriptions.
- **Movie Metadata**: Stores movie-related data such as titles, descriptions, release dates, genres, and posters in **DynamoDB**.
- **Rate Limiting**: Protects the API by limiting the number of requests for movie-related actions.

---

## Tech Stack

- **Node.js**: JavaScript runtime for building scalable, server-side applications.
- **Express.js**: Web framework for building RESTful APIs.
- **DynamoDB**: NoSQL database for storing unstructured movie data.
- **Elasticsearch**: Distributed search and analytics engine for fast, scalable search functionality.
- **Kafka**: For event-driven communication between microservices.
- **Docker**: For containerization and ensuring consistency across different environments.
- **Nginx**: For reverse proxying and load balancing.

---

## Setup Instructions

### 1. Clone the repository:

```bash
git clone https://github.com/yourusername/movie_catalog_service.git
cd movie_catalog_service
```

### 2. Install dependencies:

```bash
npm install
```

### 3. Set up environment variables:

Create a `.env` file in the root directory and add the following environment variables:

```env
DB_URI=your_dynamodb_connection_string
ELASTICSEARCH_URI=your_elasticsearch_connection_string
KAFKA_BROKER=your_kafka_broker_address
```

### 4. Run the application locally:

```bash
npm run dev
```

The service will be available on `http://localhost:3000`.

### 5. Docker Setup (Optional):

To run the service in a Docker container, use the following command:

```bash
docker-compose up --build
```

---

## API Endpoints

### 1. **GET** `/movies`

Fetch a list of movies.

- **Response**:
  ```json
  [
    {
      "id": "movie1",
      "title": "Movie Title",
      "description": "Movie Description",
      "release_date": "2023-12-01",
      "genres": ["Action", "Drama"],
      "poster": "/images/movie1.jpg"
    },
    ...
  ]
  ```

### 2. **POST** `/movies`

Add a new movie to the catalog.

- **Request Body**:
  ```json
  {
    "title": "New Movie",
    "description": "Movie Description",
    "release_date": "2024-01-01",
    "genres": ["Action", "Sci-Fi"],
    "poster": "/images/new_movie.jpg"
  }
  ```

- **Response**:
  ```json
  {
    "message": "Movie added successfully."
  }
  ```

### 3. **GET** `/movies/search`

Search for movies based on a query string (title, genre, or other metadata).

- **Query Parameters**:
    - `query`: The search query string (e.g., movie title, genre).

- **Response**:
  ```json
  [
    {
      "id": "movie1",
      "title": "Movie Title",
      "description": "Movie Description",
      "release_date": "2023-12-01",
      "genres": ["Action", "Drama"],
      "poster": "/images/movie1.jpg"
    },
    ...
  ]
  ```

### 4. **PUT** `/movies/:id`

Update the details of a specific movie.

- **Request Body**:
  ```json
  {
    "title": "Updated Movie Title",
    "description": "Updated Movie Description",
    "release_date": "2024-02-01",
    "genres": ["Action", "Thriller"],
    "poster": "/images/updated_movie.jpg"
  }
  ```

- **Response**:
  ```json
  {
    "message": "Movie updated successfully."
  }
  ```

### 5. **DELETE** `/movies/:id`

Delete a specific movie from the catalog.

- **Response**:
  ```json
  {
    "message": "Movie deleted successfully."
  }
  ```

---

## Event-Driven Architecture

The **Movie Catalog Service** communicates with other services using **Kafka** for event-driven actions. This allows the system to scale efficiently and enables asynchronous communication across services.

### Kafka Events:

- **Movie Added Event**: Triggered when a new movie is added to the catalog.
- **Movie Updated Event**: Triggered when an existing movie is updated.
- **Movie Deleted Event**: Triggered when a movie is removed from the catalog.

---

## Testing

To run the tests, use the following command:

```bash
npm test
```

You can find tests for movie-related functionality, search, and CRUD operations inside the `tests/` folder.

---

## Contributing

We welcome contributions! To contribute to this project:

1. Fork the repository.
2. Create a new branch for your feature or bugfix.
3. Commit your changes.
4. Push to your fork.
5. Open a pull request.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Notes

- Ensure that **DynamoDB** and **Elasticsearch** are set up and configured properly before starting the application.
- Make sure to keep your environment variables secure and never expose sensitive data like database credentials in public repositories.
- Always follow best practices, including implementing proper error handling and validation in the API.

---

## Folder Structure

```
movie_catalog_service/
├── README.md                         # Documentation for the service
├── package.json                      # Project dependencies and scripts
├── .env                              # Environment variables (e.g., DB_URI, KAFKA_BROKER)
├── .gitignore                        # Git ignore rules (node_modules, .env, etc.)
├── config/                            # Configuration files for environment, database, and services
│   ├── db.config.js                  # DynamoDB connection configuration
│   ├── kafka.config.js               # Kafka producer and consumer configuration for events
│   ├── elasticsearch.config.js       # Elasticsearch configuration for search functionality
├── src/                               # Source files for the service
│   ├── controllers/                  # API controllers handling incoming requests
│   │   ├── movieController.js        # Handles CRUD operations and movie search logic
│   │   ├── searchController.js       # Handles search requests for movies
│   ├── models/                       # Models for movie data (DynamoDB)
│   │   └── movieModel.js             # Defines the Movie model for DynamoDB
│   ├── routes/                       # Express route definitions
│   │   ├── movieRoutes.js            # Routes for fetching movie data and search
│   ├── services/                     # Business logic and interactions with databases and services
│   │   ├── movieService.js           # Logic for CRUD operations on movie data
│   │   ├── searchService.js          # Logic for handling search functionality using Elasticsearch
│   ├── utils/                        # Utility functions (e.g., helper functions, validation)
│   │   └── validationUtils.js        # Input validation for movie search requests
│   ├── app.js                        # Main Express app setup
│   ├── server.js                     # Server entry point (starting the Express app)
├── public/                           # Static assets (e.g., images, movie posters)
│   ├── movies/                       # Movie-related media storage
│   ├── images/                       # Movie poster storage
├── config/                           # Docker, NGINX, and CI/CD files for the service
│   ├── Dockerfile                    # Docker configuration for containerizing the app
│   ├── docker-compose.yml            # Local development environment setup using Docker Compose
│   └── nginx.conf                    # NGINX configuration if acting as reverse proxy/load balancer
├── tests/                            # Unit and integration tests
│   ├── movie.test.js                 # Tests for movie-related functionality
│   ├── search.test.js                # Tests for search-related functionality
│   └── service.test.js
```

---

This `README.md` contains all the necessary details about the **Movie Catalog Service**, the setup instructions, API documentation, and a clear explanation of the service architecture. The folder structure is displayed for better organization of the project files.
