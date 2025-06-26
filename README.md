# airbnb-clone-project
**Project Goal:** Booking airticket online\
**Stack:** Backend Stack\
\
**Team Roles**\
Database Design: databases should communicate together, how integrations should work, and how to ensure that the product is secure and stable.\
Backend Role: ITRex offers back-end web development services, including building full applications or supporting front-end teams on a flexible basis. They specialize in creating customer portals, e-commerce sites, and enterprise web apps. Their solutions connect IT systems, integrate third-party tools, and provide secure APIs that automate tasks and improve business efficiency.\
DevOps engineer: Facilitates cooperation between development and operations teams. Builds continuous integration and continuous delivery (CI/CD) pipelines for faster delivery.\
QA engineers: design and implement quality assurance processes and procedures that help prevent defects at later stages of development.\
\
**Technology Stack**\
Python: programming the backend.\
Django: a framework used with python and RESTAPI.\
PostgreSQL: For databases.\
\
## Data Model Overview

This project includes the following core entities as part of the backend system:

---

### Users

**Key Fields**
- `id`: Unique identifier
- `name`: Full name of the user
- `email`: Contact email address
- `password_hash`: Encrypted password
- `role`: User role (e.g., guest, host, admin)

**Relationships**
- A user can own multiple **properties**
- A user can make multiple **bookings**
- A user can write multiple **reviews**
- A user can make multiple **payments**

---

### Properties

**Key Fields**
- `id`: Unique identifier
- `title`: Title of the property
- `location`: Address or location info
- `price_per_night`: Cost per night
- `owner_id`: Foreign key to the user (host)

**Relationships**
- A property is owned by **one user**
- A property can have multiple **bookings**
- A property can have multiple **reviews**

---

### Bookings

**Key Fields**
- `id`: Unique identifier
- `user_id`: ID of the guest who made the booking
- `property_id`: ID of the booked property
- `start_date`: Check-in date
- `end_date`: Check-out date
- `status`: Booking status (e.g., pending, confirmed, cancelled)

**Relationships**
- A booking is made by **one user**
- A booking is for **one property**
- A booking is linked to **one payment**

---

### Reviews

**Key Fields**
- `id`: Unique identifier
- `user_id`: ID of the user who wrote the review
- `property_id`: ID of the property being reviewed
- `rating`: Numerical rating (e.g., 1–5)
- `comment`: Review content

**Relationships**
- A review is written by **one user**
- A review is for **one property**
- Typically, a user can leave **one review per booking**

---

### Payments

**Key Fields**
- `id`: Unique identifier
- `booking_id`: Related booking ID
- `user_id`: User who made the payment
- `amount`: Total paid
- `status`: Payment status (e.g., paid, pending, failed)
- `payment_method`: Method used (e.g., Credit Card, PayPal)

**Relationships**
- A payment is linked to **one booking**
- A payment is made by **one user**

---

### Entity Relationship Summary

- **User ↔ Properties**: One-to-many (host can own many properties)  
- **User ↔ Bookings**: One-to-many (guest can make many bookings)  
- **User ↔ Reviews**: One-to-many (user can leave reviews)  
- **User ↔ Payments**: One-to-many (user can make payments)  
- **Property ↔ Bookings**: One-to-many (property can have many bookings)  
- **Property ↔ Reviews**: One-to-many (property can be reviewed multiple times)  
- **Booking ↔ Payment**: One-to-one (each booking has a corresponding payment)  
- **Booking ↔ Property & User**: Many-to-one (each booking is linked to one property and one user)

---

## Main Features

### User Management
Handles user registration, authentication, and role-based access (e.g., guest, host, admin). This feature ensures secure login, profile management, and proper permission control across the platform.

### Property Management
Allows hosts to list, update, and manage their properties, including details such as location, pricing, availability, and images. This enables property owners to maintain accurate and up-to-date listings for users to browse and book.

### Booking System
Enables users to check availability and make reservations for specific date ranges. It manages booking statuses (pending, confirmed, cancelled) and ensures accurate scheduling to avoid conflicts.

### Reviews and Ratings
Allows users to leave reviews and ratings for properties they have booked. This feature builds transparency and trust within the platform by providing feedback that helps future guests make informed decisions.

### Payments and Invoicing
Integrates secure payment gateways to process transactions related to bookings. It tracks payment statuses, generates invoices, and allows both users and administrators to monitor financial activity.

## Security Measures

Security is a critical aspect of this project to protect sensitive user data, prevent unauthorized access, and ensure safe transactions. Below are the key security measures implemented in the system:

### Authentication
The system uses secure authentication methods (such as hashed passwords and token-based sessions) to verify user identities. This ensures that only registered users can access their accounts and prevents unauthorized login attempts.

### Authorization
Role-based access control (RBAC) is implemented to restrict access to specific resources based on user roles (e.g., guest, host, admin). This protects sensitive actions like managing properties, viewing payment data, or accessing admin dashboards from being misused.

### Input Validation and Sanitization
All user inputs are validated and sanitized to prevent common vulnerabilities such as SQL injection and cross-site scripting (XSS). This protects the system from malicious data that could compromise functionality or data integrity.

### Rate Limiting and Throttling
Rate limiting is applied to APIs to prevent abuse (e.g., brute-force attacks, spamming). It ensures fair usage and protects the server from being overwhelmed by excessive requests.

### Secure Payments
Payment processing is handled through trusted third-party gateways (e.g., Stripe, PayPal), ensuring encryption, fraud protection, and PCI compliance. This safeguards financial data and builds trust between the platform and its users.

### Data Encryption
Sensitive data (such as passwords and payment tokens) is encrypted both at rest and in transit using industry-standard protocols (e.g., HTTPS, TLS). This prevents data leaks and unauthorized access during communication.

### Logging and Monitoring
System logs and monitoring tools are used to detect suspicious activity and respond to security inc

## CI/CD Pipelines

Continuous Integration and Continuous Deployment (CI/CD) pipelines automate the process of testing, building, and deploying code changes. They help ensure that every code update is automatically checked for errors and safely delivered to production without manual intervention.

CI/CD is important for this project because it reduces human error, speeds up development, and ensures consistent, reliable deployments. It also helps maintain high code quality by running automated tests on every commit or pull request.

### Tools Used:
- **GitHub Actions**: Automates testing, linting, and deployment workflows directly from the repository.
- **Docker**: Creates consistent development and deployment environments using containerization.
- **Docker Hub or GitHub Container Registry**: Stores and distributes Docker images used in deployment.
- **Optional: Heroku, Render, AWS, or DigitalOcean**: Can be used as hosting platforms to deploy the application in CI/CD workflows.
