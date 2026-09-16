# Task 1: Backend — Identity Reconciliation

## Overview

This project implements an identity reconciliation service for an e-commerce platform. It identifies customers who use different email addresses and phone numbers across multiple purchases and consolidates their contact information.

## Technology Stack

* Node.js
* Express.js
* TypeScript
* PostgreSQL
* Prisma ORM

## Features

* `POST /identify` endpoint.
* Accepts email and phone number in JSON format.
* Creates a primary contact when no matching contact exists.
* Creates secondary contacts when new information is associated with an existing customer.
* Merges contact records when two previously separate primary contacts are found to be related.
* Returns consolidated email addresses, phone numbers, and secondary contact IDs.
* Handles invalid requests and database errors.
* Includes automated tests.

## API Endpoint

### POST /identify

Request:

```json
{
  "email": "doc@example.com",
  "phoneNumber": "9876543210"
}
```

Response:

```json
{
  "primaryContactId": 1,
  "emails": [
    "doc@example.com"
  ],
  "phoneNumbers": [
    "9876543210"
  ],
  "secondaryContactIds": []
}
```

## Database Schema

The Contact model contains:

* `id`
* `phoneNumber`
* `email`
* `linkedId`
* `linkPrecedence`
* `createdAt`
* `updatedAt`
* `deletedAt`

`linkPrecedence` can be `primary` or `secondary`.

## Project Setup

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Create a `.env` file:

```env
DATABASE_URL="postgresql://postgres:password@localhost:5432/identity_db"
PORT=3000
```

### 3. Generate Prisma Client

```bash
npx prisma generate
```

### 4. Run database migrations

```bash
npx prisma migrate dev
```

### 5. Start the application

```bash
npm run dev
```

The API will run at:

`http://localhost:3000`

## Testing

Run the automated tests:

```bash
npm test
```

## Example Test Scenarios

1. Create a new primary contact.
2. Add a secondary contact with a new email.
3. Add a secondary contact with a new phone number.
4. Merge two previously separate primary contacts.
5. Handle requests containing only an email or only a phone number.

## License

This project was developed as part of a backend and DevOps assignment.
