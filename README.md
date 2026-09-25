# Dental Practice Management Database

A fully normalized relational database for a dental practice, built with **SQLite**. Course project covering the full lifecycle: ERD → relational algebra → BCNF schema → implementation → analytical queries.

## Schema

- **28 tables**, all in BCNF
- Models patients, medical staff, treatments, appointments, billing records, payments (cash / check / card / insurance), insurance plans, inventory, medical records (history, X-rays, medications, allergies, HIPAA forms), and patient reviews
- Enforced primary/foreign keys and `CHECK` constraints (e.g., payment type ∈ {Cash, Check, Card, Insurance})

## What's included

| File | Contents |
|---|---|
| `CreateQueries.sql` | Full DDL — table creation with keys, constraints, and indexes |
| `InsertQueries.sql` | Seed data inserts |
| `InsertDeleteQueries.sql` | Insert/delete statements with FK-ordering |
| `SimpleQueries.sql` | 9 analytical queries — per-patient revenue ranking, payment-type summaries, most frequent procedure, insurance plan counts |
| `ExtraQueries.sql` | 5 advanced queries — CTEs, `LEFT JOIN`s, most common allergies, most recent appointment per patient |

Plus:

- **2 views** — `PatientPaymentOverview` (payment count + totals per patient), `RecentAppointments` (appointments in the last 30 days)
- **2 transactions** — multi-table staff onboarding and card-payment-to-billing linkage, kept atomic to protect data integrity
- **Index design with written justification** — B-tree on `Payment(Type, ReceivedBy)` for cash-handling audit queries; hash-style lookup on `People(PhoneNumber)` for fast patient search

## Usage

```bash
sqlite3 practice.db < CreateQueries.sql
sqlite3 practice.db < InsertQueries.sql
sqlite3 practice.db < SimpleQueries.sql
```

(Originally developed and tested on sqliteonline.com — any SQLite client works.)

## Team

4-person team project. My contributions: schema design and implementation, ERD and relational algebra, analytical SQL queries, and index design.
