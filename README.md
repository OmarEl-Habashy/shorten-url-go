# URL Shortener Service in Go

A modern URL shortening service built with Go, Fiber, and Redis.

## Overview

This project provides a simple yet powerful URL shortening service that allows users to:
- Create shortened URLs for long web addresses
- Optionally set custom short URLs
- Configure expiration times for shortened links
- Track usage statistics

## Tech Stack

- **Backend**: Go with Fiber framework
- **Database**: Redis
- **Containerization**: Docker and Docker Compose

## Features

- **URL Shortening**: Convert long URLs to short, manageable links
- **Custom Short URLs**: Ability to define custom short paths
- **Link Expiration**: Set configurable expiration times for links
- **Rate Limiting**: API rate limiting to prevent abuse
- **Visit Tracking**: Count redirects for each shortened URL

## Project Structure

```
shorten-url-go/
├── api/
│   ├── database/      # Redis database connection
│   ├── helpers/       # Utility functions
│   ├── routes/        # API endpoints
│   ├── Dockerfile     # API service container
│   ├── go.mod         # Go module dependencies
│   └── main.go        # Application entry point
├── db/
│   └── Dockerfile     # Redis container
├── docker-compose.yml # Services orchestration
└── README.md          # Project documentation
```

## API Endpoints

### Shorten URL
- **POST** `/api/v1`
- Request body:
  ```json
  {
    "url": "https://example.com/very/long/path",
    "short": "custom",     // Optional
    "expiry": 24           // Hours (default: 24)
  }
  ```
- Response:
  ```json
  {
    "url": "https://example.com/very/long/path",
    "short": "custom",
    "expiry": 24,
    "rate_limit": 9,
    "rate_limit_reset": 30
  }
  ```

### Resolve URL
- **GET** `/:shortURL`
- Redirects to the original URL

## Setup and Installation

### Prerequisites
- Docker and Docker Compose

### Running the Application

1. Clone the repository
   ```bash
   git clone https://github.com/OmarEl-Habashy/shorten-url-go.git
   cd shorten-url-go
   ```

2. Create a `.env` file in the `api` directory with the following variables:
   ```
   APP_PORT=:3000
   DB_ADDR=db:6379
   DB_PASSWORD=
   DOMAIN=localhost:3000
   API_QUOTA=10
   ```

3. Build and run using Docker Compose
   ```bash
   docker-compose up -d
   ```

4. The service will be available at `http://localhost:3000`

## Development

### Local Setup

1. Install Go (version 1.25+)
2. Install Redis
3. Configure environment variables
4. Run the application:
   ```bash
   cd api
   go run main.go
   ```
