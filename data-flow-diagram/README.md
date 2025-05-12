# Data Flow Diagram (DFD) Analysis for Airbnb-like Platform

This document outlines the data flows for key processes within the Airbnb-like platform. It will serve as the basis for creating a Level 0 (Context Diagram) and a Level 1 DFD, focusing on core backend operations related to users, properties, bookings, and payments.

## Key Entities (Data Stores)

Based on our ERD and database schema, the primary data stores are:

1.  **Users_DS:** Stores user account information (profiles, credentials, status).
2.  **Properties_DS:** Stores details of listed properties (descriptions, location, amenities, availability, pricing, host info).
3.  **Bookings_DS:** Stores information about reservations made (guest, property, dates, price, status).
4.  **Reviews_DS:** Stores reviews and ratings submitted by users for properties and potentially guests.
5.  **Payments_DS:** Stores details of financial transactions related to bookings (amount, method, status, transaction IDs).
6.  **PropertyTypes_DS:** Lookup table for property types.
7.  **Amenities_DS:** Lookup table for amenities.
8.  **PropertyAmenities_DS:** Linking table for properties and their amenities.

## External Entities

1.  **User (Guest/Host):** Interacts with the system to perform various actions.
2.  **Payment Gateway:** External system for processing payments.
3.  **Admin (Optional for this DFD focus):** Manages the platform.

## Core Processes and Data Flows

We will focus on a few key high-level processes. A Level 0 DFD would show the entire system as a single process interacting with external entities. A Level 1 DFD would break this down.

### Level 0: Context Diagram

*   **External Entities:** User (Guest/Host), Payment Gateway.
*   **System:** "Airbnb-like Platform"
*   **Data Flows (Examples):
    *   User -> System: Registration Info, Login Credentials, Profile Updates, Property Listing Info, Search Queries, Booking Requests, Review Submissions, Payment Details (via System to Payment Gateway).
    *   System -> User: Account Confirmation, Profile Data, Property Search Results, Property Details, Booking Confirmations, Payment Confirmations, Review Displays.
    *   System -> Payment Gateway: Payment Authorization Request, Refund Request.
    *   Payment Gateway -> System: Payment Confirmation/Failure, Refund Confirmation.

### Level 1 DFD: Decomposing the "Airbnb-like Platform"

#### Process 1: Manage User Accounts
   - **Description:** Handles user registration, login, profile updates.
   - **Inputs from User:** Registration Data (name, email, password), Login Credentials, Profile Update Data.
   - **Outputs to User:** Registration Confirmation, Session Token/Cookie, Profile View.
   - **Data Store Interactions:** 
     - WRITE to Users_DS (new user, updated profile).
     - READ from Users_DS (authentication, profile view).

#### Process 2: Manage Property Listings
   - **Description:** Handles creation, update, and retrieval of property listings.
   - **Inputs from User (Host):** New Property Data (title, description, address, photos, price, amenities, availability), Property Update Data.
   - **Inputs from User (Guest):** Search Criteria, Property ID for details.
   - **Outputs to User (Host):** Listing Confirmation, View of Own Listings.
   - **Outputs to User (Guest):** Search Results, Property Details (including amenities, reviews).
   - **Data Store Interactions:**
     - WRITE to Properties_DS (new/updated property).
     - WRITE to PropertyAmenities_DS (linking amenities).
     - READ from Properties_DS, Amenities_DS, PropertyAmenities_DS, Reviews_DS (for displaying listings and details).

#### Process 3: Process Bookings
   - **Description:** Handles booking requests, confirmations, and viewing.
   - **Inputs from User (Guest):** Booking Request (property_id, user_id, dates, num_guests).
   - **Outputs to User (Guest/Host):** Booking Confirmation/Status, Booking Details.
   - **Data Store Interactions:**
     - READ from Properties_DS (check availability, price).
     - READ from Users_DS (guest details).
     - WRITE to Bookings_DS (new booking, updated status).
     - This process will trigger/interact with "Process Payment".

#### Process 4: Process Payments
   - **Description:** Handles payment transactions for bookings.
   - **Inputs from Process 3 (Process Bookings):** Booking ID, Total Amount.
   - **Inputs from User (Guest, often via a secure iframe/redirect from Payment Gateway):** Payment Details.
   - **Interaction with Payment Gateway (External Entity):**
     - System SENDS Payment Authorization Request (amount, booking reference) TO Payment Gateway.
     - Payment Gateway SENDS Payment Confirmation/Failure TO System.
   - **Outputs to Process 3 (Process Bookings):** Payment Status.
   - **Outputs to User (Guest):** Payment Receipt/Notification.
   - **Data Store Interactions:**
     - WRITE to Payments_DS (payment record, status, transaction_id).
     - UPDATE Bookings_DS (payment status for the booking).

#### Process 5: Manage Reviews
   - **Description:** Handles submission and display of reviews.
   - **Inputs from User (Guest/Host):** Review Data (booking_id, rating, comment).
   - **Outputs to User (Guest/Host):** Review Confirmation.
   - **Outputs (as part of Property Details in Process 2):** Display of Reviews.
   - **Data Store Interactions:**
     - READ from Bookings_DS (verify completed stay before review).
     - WRITE to Reviews_DS (new review).

This analysis provides the structure for generating the DFD image. The image will visually represent these processes, data stores, external entities, and the data flowing between them.
