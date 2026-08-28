**Library Management System**

A desktop-based Library Management System developed in Java using Java Swing. The application provides functionality for managing books, members, borrowing requests, returns, and borrowing status through a graphical user interface.

Overview

The system provides a simple graphical interface for interacting with a library. Users can browse available books, borrow books, return books, and view borrowing status.

An administrator can log in to access an administrative panel where books can be added and information about members and borrowing requests can be viewed.

Features
User Features
Browse available books
Borrow a book
Return a borrowed book
View borrowing status
Enter member information
Automatic borrowing approval when copies are available
Admin Features
Admin login
Add new books
View borrowing requests
View registered members
Approve or reject borrowing requests based on book availability
Main Components
Book

Stores information about a book:

Title
Author
ISBN
Available copies
Member

Stores:

Member name
Member ID
Request

Represents a borrowing request and stores:

Member
Book
Request status

Possible request statuses include:

Pending
Approved
Rejected
Returned
Admin

The administrator manages:

Books
Members
Borrowing requests
Book approvals
Book returns
User Interface

The application is built using Java Swing and provides a graphical interface with options for:

Admin Login
Browse Books
Borrow Book
Return Book
View Borrowing Status

The administrative panel provides:

Add Book
View Requests
View Members
Technologies
Java
Java Swing
javax.swing
java.awt
java.awt.event
Java Collections Framework
How to Run

Make sure Java is installed on your system.

Compile the program:

javac LibraryManagementSystem.java

Run the application:

java LibraryManagementSystem
Default Admin Credentials

The project code defines the following default administrator credentials:

Username: admin
Password: admin

Note: These credentials are hard-coded in the academic project and are intended for demonstration purposes.


Concepts Demonstrated
Object-Oriented Programming
Classes and objects
Encapsulation
Constructors
Getters and setters
Java Collections (ArrayList, List)
Event-driven programming
Graphical User Interfaces
Java Swing
Basic authentication
Book inventory management
Borrowing and return management
Academic Project

This project was developed as an academic Java project demonstrating object-oriented programming and GUI development.
