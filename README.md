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
## Data Model Overview\
This project includes the following core entities as part of the backend system:\
### Users\

**Key Fields**\
- `id`: Unique identifier\
- `name`: Full name of the user\
- `email`: Contact email address\
- `password_hash`: Encrypted password\
- `role`: User role (e.g., guest, host, admin)\
\
**Relationships**\
- A user can own multiple **properties**\
- A user can make multiple **bookings**\
- A user can write multiple **reviews**\
- A user can make multiple **payments**\
\

### Properties
**Key Fields**\
- `id`: Unique identifier\
- `title`: Title of the property\
- `location`: Address or location info\
- `price_per_night`: Cost per night\
- `owner_id`: Foreign key to the user (host)\
\
**Relationships**\
- A property is owned by **one user**\
- A property can have multiple **bookings**\
- A property can have multiple **reviews**\
\
### Bookings\

**Key Fields**\
- `id`: Unique identifier\
- `user_id`: ID of the guest who made the booking\
- `property_id`: ID of the booked property\
- `start_date`: Check-in date\
- `end_date`: Check-out date\
- `status`: Booking status (e.g., pending, confirmed, cancelled)\
\
**Relationships**\
- A booking is made by **one user**\
- A booking is for **one property**\
- A booking is linked to **one payment**\
\
### Reviews\
**Key Fields**\
- `id`: Unique identifier\
- `user_id`: ID of the user who wrote the review\
- `property_id`: ID of the property being reviewed\
- `rating`: Numerical rating (e.g., 1–5)\
- `comment`: Review content\
\
**Relationships**\
- A review is written by **one user**\
- A review is for **one property**\
- Typically, a user can leave **one review per booking**\
\
### Payments\
**Key Fields**\
- `id`: Unique identifier\
- `booking_id`: Related booking ID\
- `user_id`: User who made the payment\
- `amount`: Total paid\
- `status`: Payment status (e.g., paid, pending, failed)\
- `payment_method`: Method used (e.g., Credit Card, PayPal)\
\
**Relationships**\
- A payment is linked to **one booking**\
- A payment is made by **one user**\
\

###  Entity Relationship Summary\
- **User ↔ Properties**: One-to-many (host can own many properties)\  
- **User ↔ Bookings**: One-to-many (guest can make many bookings)\  
- **User ↔ Reviews**: One-to-many (user can leave reviews)  \
- **User ↔ Payments**: One-to-many (user can make payments)  \
- **Property ↔ Bookings**: One-to-many (property can have many bookings)  \
- **Property ↔ Reviews**: One-to-many (property can be reviewed multiple times)\  
- **Booking ↔ Payment**: One-to-one (each booking has a corresponding payment)\
- **Booking ↔ Property & User**: Many-to-one (each booking is linked to one property and one user)\
