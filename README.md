# Personal Cloud Storage Application

This is a personal cloud storage application built using **Go** (Golang) and **PostgreSQL**, designed to handle file uploads, note-taking, and user authentication via Google OAuth2. The system allows users to upload files to cloud storage (e.g., AWS S3) and create text-based notes. 

## Features

- **Google OAuth2 Authentication**: Users can sign in using their Google account.
- **File Uploads**: Users can upload files, with metadata stored in a PostgreSQL database and actual files hosted on a cloud storage service (e.g., AWS S3).
- **Note-Taking**: Users can create, edit, and store personal notes.
- **User Management**: Users can view and manage their files and notes.

---

## Setup Instructions

Follow these steps to set up and run the application locally:

### Prerequisites

- **Go** (Golang) installed (preferably version 1.19 or later).
- **PostgreSQL** installed and running.
- **AWS S3** (or any cloud storage service) setup for storing files.
- **Google OAuth credentials** for authentication.

### 1. Clone the Repository
> Brief explanation of your database schema: 
The database schema for the personal cloud storage application is designed to manage three main entities: Users, Files, and Notes. Each of these entities plays a crucial role in supporting the core functionalities of the app, such as Google OAuth authentication, file uploads, and note-taking. Here's a breakdown of the schema:

1. Users Table
The Users table stores information about the users who sign up or log in using Google OAuth2. This table is the central point for user authentication and identification.

id: The unique identifier for the user in the database, automatically generated.
google_id: This is the unique ID provided by Google after a successful OAuth authentication, used to associate the user with their Google account.
email: The email address of the user, fetched from the Google account.
created_at & updated_at: Timestamps to track when the user account was created and when it was last updated.
The Users table is the foundation for associating users with their files and notes. The google_id ensures that each user is uniquely identifiable via Google login.

2. Files Table
The Files table stores metadata for each file uploaded by the user to the cloud storage (e.g., AWS S3). Actual files are stored externally (e.g., on AWS S3), and the table records the file's metadata (name, size, URL).

id: The unique identifier for the file in the database, automatically generated.
user_id: A foreign key linking each file to a specific user from the Users table, establishing a relationship between the file and the user who uploaded it.
file_name: The name of the file uploaded by the user.
s3_url: The URL of the file stored on cloud storage (e.g., AWS S3), allowing the user to access it.
file_size: The size of the file in bytes.
created_at & updated_at: Timestamps tracking when the file was uploaded and last updated.
This table allows the application to manage files, enabling users to upload, view, and delete files.

3. Notes Table
The Notes table stores personal notes created by the user. It allows users to add, update, and manage textual content.

id: The unique identifier for the note in the database, automatically generated.
user_id: A foreign key linking the note to a specific user from the Users table, ensuring that each note belongs to a particular user.
title: The title of the note.
content: The body or content of the note, which is text.
created_at & updated_at: Timestamps tracking when the note was created and last updated.
This table supports the note-taking functionality, allowing users to store and manage their personal notes.

Relationships Between Tables
Users → Files: One-to-many relationship. A user can upload multiple files, but each file is associated with only one user.
Users → Notes: One-to-many relationship. A user can create multiple notes, but each note belongs to only one user.
Both the Files and Notes tables use the user_id foreign key to associate files and notes with their respective users.

```bash
git clone https://github.com/yourusername/personal-cloud-storage.git
cd personal-cloud-storage

---

### Breakdown of the Sections:

1. **Setup Instructions**: These explain how to install the dependencies, set up PostgreSQL, configure the Google OAuth2, AWS credentials, and finally run the application.
2. **Assumptions Made**: This outlines assumptions such as users needing a Google account for OAuth, proper configuration of cloud storage (AWS S3), and the database running locally or on a server.
3. **Database Schema Explanation**: Provides a quick explanation of the schema, including the `Users`, `Files`, and `Notes` tables and their relationships.
4. **Additional Features Implemented**: Highlights the core features like file upload, Google OAuth authentication, and note-taking.
5. **Working Demo**: Describes the flow for a user to sign in, upload files, and manage notes once the server is running.
