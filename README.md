# Ticket-Booking-System
 Project Type: A console-based Java application for managing train ticket bookings, built with file-based persistence using JSON.

 🧩 1. Project Objective
To create a console-based train ticket booking system using Java that allows:

User registration & login

Train search by stations

Booking and canceling seats

Viewing past bookings

Saving data persistently in .json files

   2. Project structure
project-root/
│
├── app/
│   ├── src/
│   │   └── main/
│   │       └── java/
│   │           └── ticket/
│   │               └── booking/
│   │                   ├── App.java               # Main class (entry point)
│   │                   ├── entities/
│   │                   │   ├── User.java
│   │                   │   ├── Ticket.java
│   │                   │   └── Train.java
│   │                   ├── services/
│   │                   │   ├── UserBookingService.java
│   │                   │   └── TrainService.java
│   │                   └── util/
│   │                       └── UserServiceUtil.java
│   └── localDb/
│       ├── users.json                            # Stores user data
│       └── trains.json                           # Stores train data

🧱 3. Key Functional Modules
🔐 A. User Authentication
Signup:

User provides username and password.

Password is hashed using BCrypt.

Stored in users.json along with generated userId.

Login:

Password is validated using BCrypt.checkpw().

User context is loaded and retained in UserBookingService.

🚉 B. Train Search
Trains are searched using TrainService.

It checks:

If both source and destination exist in the train's station list.

And if the source comes before destination.

Results are shown to the user for booking selection.

🎟️ C. Ticket Booking
User selects a train.

Seats are shown in 2D (rows x columns) — 0 = available, 1 = booked.

On selection:

The train's seat is marked as 1.

A new Ticket is created and added to the user's ticketsBooked list.

Changes are saved back to trains.json and users.json.

🧾 D. Fetch Bookings
Shows all tickets booked by the logged-in user with details:

Ticket ID, Source → Destination, Date, Train ID/No.

❌ E. Cancel Booking
User enters a ticket ID.

If found, it's removed from ticketsBooked list.

A confirmation is printed.

🧠 4. Classes & Responsibilities
Class                                     	Responsibility
App.java                                  	Console menu, main logic driver
User.java                                 	User data class: name, password, ID, tickets
Ticket.java                               	Booking info: ID, user, date, source, dest, train
Train.java                                	Train info: ID, number, seat matrix, stations
UserBookingService	                        Handles user login/signup, bookings, cancellations
TrainService	                              Reads trains from file and provides search & seat updates
UserServiceUtil	                           Provides password hashing and validation

🛠️ 5. Tech Stack Used
Java (OOPs + File IO)

Jackson (ObjectMapper) for JSON read/write

BCrypt (UserServiceUtil) for password hashing

Java Collections for in-memory data handling

UUID for generating unique IDs

💡 Possible Improvements (if you want to take it further):
Add UI with JavaFX or web interface (Spring Boot or JSP).

Add Admin module to manage trains.

Persist data in DB instead of JSON (e.g., MySQL).

Add OTP/email for password reset (simulated).
