# Use Cases and Actors for Airbnb-like Platform

This document identifies the primary actors and key use cases for an Airbnb-like platform, focusing on functionalities such as user registration, property booking, and payments. This analysis will serve as the basis for creating a use case diagram.

## Actors

The primary actors interacting with the system are:

1.  **Guest (Unregistered User / Registered User):** An individual looking to find and book accommodations. This actor can be an unregistered user for browsing and a registered user for booking and other personalized actions.
2.  **Host (Registered User):** An individual who owns properties and lists them on the platform for guests to rent. A host is always a registered user.
3.  **System:** Represents the Airbnb-like platform itself, performing automated tasks, processing information, and interacting with external services.
4.  **Administrator (Registered User with Special Privileges):** A user responsible for managing the platform, users, listings, and resolving issues. (While not the primary focus of the user's request, it's a typical actor in such systems).
5.  **Payment Gateway (External System):** An external service responsible for processing financial transactions securely.

For the requested diagram focusing on registration, booking, and payments, the primary actors will be Guest, Host, System, and Payment Gateway.

## Key Use Cases

### 1. User Management & Authentication
   - **Register Account:** (Actor: Unregistered User)
     - Description: An unregistered user provides necessary details (name, email, password) to create a new account. The System validates information and creates the account.
     - Includes: Email Verification.
   - **Login to Account:** (Actor: Registered User - Guest/Host)
     - Description: A registered user provides credentials (email, password) to access their account. The System authenticates the user.
   - **Logout from Account:** (Actor: Registered User - Guest/Host)
     - Description: A logged-in user ends their session.
   - **Manage Profile:** (Actor: Registered User - Guest/Host)
     - Description: A registered user updates their personal information (name, contact, profile picture).
   - **Reset Password:** (Actor: Registered User - Guest/Host)
     - Description: A user requests to reset their forgotten password, typically via an email link.

### 2. Property Discovery & Viewing
   - **Search Properties:** (Actor: Guest)
     - Description: A guest searches for properties based on criteria like location, dates, number of guests, price, amenities.
   - **View Property Details:** (Actor: Guest)
     - Description: A guest views detailed information about a specific property, including photos, description, amenities, price, availability, and reviews.
   - **View Host Profile:** (Actor: Guest)
     - Description: A guest views the profile of a property's host.

### 3. Property Listing Management (Host)
   - **Create Property Listing:** (Actor: Host)
     - Description: A host creates a new listing for their property, providing all necessary details and images.
   - **Manage Property Listings:** (Actor: Host)
     - Description: A host views, edits, or deactivates their existing property listings.
   - **Manage Property Availability:** (Actor: Host)
     - Description: A host updates the availability calendar for their property.

### 4. Booking Management
   - **Book Property:** (Actor: Guest)
     - Description: A guest selects a property, specifies dates and number of guests, and proceeds to book it. This involves price calculation and initiating payment.
     - Extends: Process Payment.
   - **View My Bookings (Guest):** (Actor: Guest)
     - Description: A guest views their past and upcoming bookings.
   - **Manage Bookings (Host):** (Actor: Host)
     - Description: A host views and manages reservations for their properties (e.g., confirm/decline if not instant book, view guest details).
   - **Cancel Booking:** (Actor: Guest / Host)
     - Description: A guest or host cancels an existing booking, subject to cancellation policies. May involve refund processing.
     - Extends: Process Refund (via Payment Gateway).

### 5. Payment Processing
   - **Process Payment:** (Actor: Guest, System, Payment Gateway)
     - Description: The System, on behalf of the Guest, interacts with the Payment Gateway to process the payment for a booking.
     - Guest provides payment details (handled by Payment Gateway interface).
   - **Process Refund:** (Actor: System, Payment Gateway)
     - Description: The System interacts with the Payment Gateway to process a refund for a cancelled booking.

### 6. Reviews and Ratings
   - **Submit Review for Property:** (Actor: Guest)
     - Description: A guest submits a rating and textual review for a property after their stay.
   - **Submit Review for Guest:** (Actor: Host)
     - Description: A host submits a rating and textual review for a guest after their stay.

For the requested diagram, we will focus on:
-   **User Registration Cluster:** Register Account, Login to Account.
-   **Property Booking Cluster:** Search Properties, View Property Details, Book Property.
-   **Payment Cluster:** Process Payment (as part of Book Property).

Actors involved will primarily be Guest (or Unregistered User for registration), Host (implicitly, as they provide properties to be booked), System, and Payment Gateway.
