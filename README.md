# Horus Air - Airline Ticket Booking

An airline ticket booking website for domestic flights across Egypt.

Full-stack concept application: a **React 18** single-page client, a **PHP 8 REST API**
(framework-free, PDO with prepared statements) and a **MySQL** database.

## Features

- Flight search by route and date across a domestic network
- Interactive seat map generated per flight (6 seats x 28 rows)
- Transactional booking: every seat is claimed with a guarded UPDATE so a seat can never be sold twice
- Boarding-pass style ticket with passenger names, seats and a unique reference
- Cancellation releases the seats back to the map, refused after departure

## Interface

The client ships a hand-written motion layer - CSS keyframes plus a few small React
helpers, no animation library: staged entrances with per-card stagger, hover lift and
cover zoom, numbers that count up, charts that draw themselves, an animated seat map and
boarding pass, confetti only on real success states, and shimmering skeletons while a
request is in flight. All of it switches off under `prefers-reduced-motion: reduce`.

## Tech stack

| Layer | Tech |
| --- | --- |
| Front end | React 18, Vite, React Router |
| Back end | PHP 8.1+, PDO (native prepared statements), PHP sessions |
| Database | MySQL 8 (InnoDB, foreign keys, transactions) |

## Screenshots

| Screen | Preview |
| --- | --- |
| Flight search | ![search](screenshots/search.png) |
| Search results | ![results](screenshots/results.png) |
| Seat map and passenger form | ![seats](screenshots/seats.png) |
| Boarding pass | ![ticket](screenshots/ticket.png) |

## Engineering

- **API test suite:** 21 end-to-end tests (80 assertions) that start the real PHP front controller and drive it over HTTP: registration and sessions, validation, ownership checks, seat claiming and rollback, booking privacy, cancellation, seat changes and flight search validation. They run against SQLite so no database server is needed; real MySQL is covered by the smoke test below.
- **Docker Compose:** MySQL 8.4, the PHP API and nginx serving the React client start with one command.
- **CI (GitHub Actions):** PHP lint and tests on PHP 8.3, the client production build, and a Docker smoke test that boots the whole stack and checks health, registration and the session endpoint against real MySQL.
- **Endpoints added in this round:** `POST /api/bookings/{reference}/seat` (atomic seat change) and `GET /api/health`.

## Source code

The full source code for this project - the React client, the PHP REST API, and the
database schema with seed data - is kept in a **private repository**.

It is available on request: reach out through my
[GitHub profile](https://github.com/ahmed-ghalwash) and I will be happy to share it.
