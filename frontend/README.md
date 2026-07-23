# Frontend - Library Management System (LMS)

The **Frontend** is the presentation layer of the Library Management System. It provides a modern, responsive, and interactive user interface for managing library operations. Users can perform tasks such as adding, updating, deleting, and searching books while interacting with the backend through RESTful APIs.

---

## Overview

The frontend is built using standard web technologies and is served through Nginx inside a Docker container. It communicates with the Flask backend to retrieve and display real-time data from the MySQL database. The application is designed with a responsive layout to ensure a consistent user experience across different screen sizes.

---

## Project Structure

```text
frontend/
│
├── Dockerfile          # Frontend container configuration
├── nginx.conf          # Nginx server configuration
├── index.html          # Main dashboard page
│
├── css/
│   └── style.css       # Application styling
│
├── js/
│   └── app.js          # Client-side functionality & API calls
│
└── images/             # Static images and assets
```

---

## Technologies Used

| Technology       | Description                                |
| ---------------- | ------------------------------------------ |
| HTML5            | Builds the application structure           |
| CSS3             | Provides responsive styling and layout     |
| JavaScript (ES6) | Handles client-side logic and API requests |
| Fetch API        | Communicates with the backend REST APIs    |
| Nginx            | Serves the frontend application            |
| Docker           | Containerizes the frontend service         |
