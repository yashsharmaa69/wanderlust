# Project Name

Wanderlust.

# Project Overview

This is a Node.js + Express travel listing application for creating, viewing, editing, and deleting property listings, along with user accounts and review posting. It is built for authenticated users who want to publish listings and for visitors who want to browse listings and read reviews.

# Features

Implemented features:

- User signup, login, and logout using Passport Local authentication.
- Session-based auth with flash messages and MongoDB-backed session storage.
- Listing creation with image upload to Cloudinary.
- Listing browsing, detailed listing pages, edit, and delete actions.
- Review creation and review deletion on individual listings.
- Ownership checks for editing/deleting listings and deleting reviews.
- Server-side validation for listing and review forms with Joi.
- Listing detail pages that show owner information and populated reviews.
- Listing cards with price formatting, tax toggle UI, and category-style filter chips in the homepage layout.
- Bootstrap-based form validation on the client side.
- Seed data initialization script for populating the database.

Inactive or not fully implemented in the current codebase:

- Map rendering and geocoding code is present only in comments, and the map section in the listing detail view is commented out.
- The navbar includes a search input, but no backend search route or controller is implemented.

# Tech Stack

Frontend:

- EJS templates
- Bootstrap 5.3.8 via CDN
- Font Awesome 7.0.1 via CDN
- Google Fonts: Plus Jakarta Sans
- Custom client-side validation script
- Custom CSS in `public/css/style.css` and `public/css/rating.css`

Backend:

- Node.js 24.14.0
- Express 5.2.1
- Method override for PUT and DELETE form support
- EJS Mate layout engine
- Multer for multipart form handling

Database:

- MongoDB
- Mongoose 9.7.4

Authentication:

- Passport 0.7.0
- Passport Local
- Passport Local Mongoose
- express-session
- connect-mongo for session persistence

State Management:

- Server-side sessions
- Flash messages with connect-flash

Styling:

- Bootstrap
- Custom CSS

APIs:

- Cloudinary for image uploads
- `@mapbox/mapbox-sdk` and `@maptiler/sdk` are installed, but the active geocoding/map flow is commented out in the current codebase

Libraries:

- `joi`
- `cloudinary`
- `multer-storage-cloudinary`
- `dotenv`
- `maplibre-gl`

Build tools:

- npm
- CommonJS modules

Deployment-related tools:

- `dotenv` for environment configuration
- `connect-mongo` for session storage in MongoDB
- Cloudinary for external image storage
- MongoDB Atlas is referenced through `ATLASDB_URL`

# Architecture

The project is organized as an Express MVC-style application:

```text
WANDERLUST/
├── app.js
├── cloudConfig.js
├── middleware.js
├── schema.js
├── controllers/
├── init/
├── models/
├── public/
├── routes/
├── utils/
└── views/
```

- `app.js` configures Express, MongoDB, sessions, Passport, flash messages, static assets, route mounting, and the error handler.
- `routes/` contains the HTTP entry points for listings, reviews, and users.
- `controllers/` contains the request handlers for listing CRUD, review CRUD, and auth flows.
- `models/` defines the Mongoose schemas for listings, reviews, and users.
- `middleware.js` contains auth checks, ownership checks, and Joi validation middleware.
- `schema.js` defines the Joi request schemas for listings and reviews.
- `cloudConfig.js` configures Cloudinary storage for uploaded listing images.
- `init/` contains the database seed script and sample listing data.
- `public/` contains client-side JS and CSS.
- `views/` contains EJS templates for layouts, listings, users, and shared partials.

Important modules and responsibilities:

- `models/listing.js` stores listing metadata, image data, ownership, reviews, and coordinates.
- `models/review.js` stores review text, rating, timestamps, and author reference.
- `models/user.js` stores user email data and Passport Local Mongoose credentials.
- `controllers/listings.js` handles listing browsing, creation, editing, and deletion.
- `controllers/reviews.js` handles adding and removing reviews from listings.
- `controllers/users.js` handles signup, login, and logout.
- `middleware.js` protects routes with login, ownership, and author checks.

# Installation

```bash
git clone https://github.com/yashsharmaa69/wanderlust.git
cd wanderlust
npm install
```

# Environment Variables

Create a `.env` file with the variables used by the application:

```bash
ATLASDB_URL=<your-mongodb-connection-string>
SECRET=<session-secret>
CLOUD_NAME=<cloudinary-cloud-name>
CLOUD_API_KEY=<cloudinary-api-key>
CLOUD_API_SECRET=<cloudinary-api-secret>
MAP_TOKEN=<map-token>
```

Note: `MAP_TOKEN` is referenced in the listing detail view and commented map/geocoding code, but the active map integration is not enabled.

# Running the App

```bash
node app.js
```

The server listens on port `8080`.

# Database Seeding

```bash
node init/index.js
```

This seed script connects to a local MongoDB instance at `mongodb://127.0.0.1:27017/wanderlust`, clears existing listings, and inserts sample listing data.

# Scripts

- `npm test` currently exits with `Error: no test specified`.

# Application Routes

- `GET /listings` - list all listings
- `GET /listings/new` - render the create listing form
- `POST /listings` - create a listing
- `GET /listings/:id` - show a listing
- `GET /listings/:id/edit` - render the edit form
- `PUT /listings/:id` - update a listing
- `DELETE /listings/:id` - delete a listing
- `POST /listings/:id/reviews` - add a review
- `DELETE /listings/:id/reviews/:reviewId` - delete a review
- `GET /signup` - render signup form
- `POST /signup` - create a user account
- `GET /login` - render login form
- `POST /login` - authenticate a user
- `GET /logout` - log out the current user

# Notes

- The footer links to `/privacy` and `/terms`, but no matching routes are defined in the current codebase.
- The listing detail template includes a commented map section, so location visualization is currently inactive.
