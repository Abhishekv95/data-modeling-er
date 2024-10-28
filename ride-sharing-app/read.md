Ride-Sharing App. This system tracks essential components such as drivers, riders, rides, routes, payments, and ratings, supporting the core functions of a ride-sharing platform.

Main Entities and Relationships
User

Attributes: user_id (PK), name, email, phone_number, user_type (driver/rider), registration_date, status
Relationships:
Can either be a Driver or a Rider
Driver

Attributes: driver_id (PK), user_id (FK), license_number, vehicle_id (FK), rating, status
Relationships:
Is a specific type of User
Has one Vehicle
Participates in many Rides
Rider

Attributes: rider_id (PK), user_id (FK), preferred_payment_method, rating
Relationships:
Is a specific type of User
Participates in many Rides
Can make multiple Payments
Vehicle

Attributes: vehicle_id (PK), driver_id (FK), license_plate, model, color, year, capacity
Relationships:
Belongs to a Driver
Ride

Attributes: ride_id (PK), driver_id (FK), rider_id (FK), route_id (FK), start_time, end_time, status (e.g., completed, canceled), fare
Relationships:
Assigned to a Driver and a Rider
Has one Route
Is linked to a Payment
Route

Attributes: route_id (PK), start_location, end_location, distance, estimated_time, created_at
Relationships:
Associated with multiple Rides
Payment

Attributes: payment_id (PK), ride_id (FK), rider_id (FK), amount, payment_method (e.g., credit card, cash), status, timestamp
Relationships:
Associated with a Ride
Belongs to a Rider
Rating

Attributes: rating_id (PK), ride_id (FK), rider_id (FK), driver_id (FK), rating_value, feedback, timestamp
Relationships:
Linked to a specific Ride
Given by a Rider to a Driver
ER Diagram Design Notes
Users are divided into Drivers and Riders; both share common user attributes.
Vehicles are managed and associated with Drivers, while each Ride involves a Driver and a Rider.
Routes store details about the starting and ending points of each ride, with additional route-specific information.
Payments are linked to each Ride, capturing payment methods, amounts, and statuses.
Ratings allow riders to provide feedback and ratings for drivers after each ride, tied to a specific Ride.
