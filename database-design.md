# StudySpot Database Design

## 1. Design goals

The database supports a single-university MVP while keeping the model extensible for future universities and partner venues. It must preserve booking history, prevent invalid availability values, and support fast filtering of study spaces.

## 2. Recommended technology

Use a relational database such as PostgreSQL. The design relies on transactions, foreign keys, check constraints, indexes, and reliable timestamp handling.

## 3. Entity relationship overview

```text
users 1 ────< bookings >──── 1 study_spaces
  │                              │
  └────< availability_updates >──┘

study_spaces >────< facilities
```

One user can create many bookings and availability updates. One study space can have many bookings and availability updates. A study space can have many facilities, and a facility can belong to many study spaces.

## 4. Tables

### 4.1 `users`

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | User identifier |
| `email` | VARCHAR(255) | UNIQUE, NOT NULL | Login email |
| `password_hash` | TEXT | NOT NULL | Strong one-way password hash |
| `role` | VARCHAR(30) | NOT NULL, default `student` | `student`, `availability_manager`, or `admin` |
| `display_name` | VARCHAR(120) | NOT NULL | Name shown to the user |
| `is_active` | BOOLEAN | NOT NULL, default `true` | Account status |
| `created_at` | TIMESTAMPTZ | NOT NULL | Creation time |
| `updated_at` | TIMESTAMPTZ | NOT NULL | Last modification time |

### 4.2 `study_spaces`

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | Study-space identifier |
| `name` | VARCHAR(160) | NOT NULL | Public name |
| `description` | TEXT | NULL | Space description |
| `location_name` | VARCHAR(200) | NOT NULL | Building or campus location |
| `latitude` | NUMERIC(9,6) | NULL | Map latitude |
| `longitude` | NUMERIC(9,6) | NULL | Map longitude |
| `study_type` | VARCHAR(20) | NOT NULL | `quiet`, `group`, or `mixed` |
| `capacity` | INTEGER | NOT NULL, CHECK > 0 | Maximum seats |
| `available_seats` | INTEGER | NOT NULL, CHECK 0..capacity | Current available seats |
| `opening_hours` | JSONB | NOT NULL | Published opening schedule |
| `is_active` | BOOLEAN | NOT NULL, default `true` | Whether new bookings are allowed |
| `created_at` | TIMESTAMPTZ | NOT NULL | Creation time |
| `updated_at` | TIMESTAMPTZ | NOT NULL | Last modification time |

### 4.3 `facilities`

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | Facility identifier |
| `code` | VARCHAR(40) | UNIQUE, NOT NULL | Stable filter code |
| `name` | VARCHAR(80) | NOT NULL | Display name |

Initial facility codes may include `wifi`, `power_outlets`, `quiet`, and `group_study`.

### 4.4 `study_space_facilities`

| Column | Type | Constraints | Description |
|---|---|---|---|
| `study_space_id` | UUID | PK/FK | References `study_spaces.id` |
| `facility_id` | UUID | PK/FK | References `facilities.id` |

The composite primary key prevents duplicate facility assignments.

### 4.5 `availability_updates`

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | Update identifier |
| `study_space_id` | UUID | FK, NOT NULL | Updated study space |
| `updated_by` | UUID | FK, NOT NULL | User who entered the update |
| `available_seats` | INTEGER | NOT NULL, CHECK >= 0 | Reported seats |
| `recorded_at` | TIMESTAMPTZ | NOT NULL | Time the report was recorded |

The application must also validate that `available_seats` does not exceed the space capacity.

### 4.6 `bookings`

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK | Booking identifier |
| `user_id` | UUID | FK, NOT NULL | Student who booked |
| `study_space_id` | UUID | FK, NOT NULL | Reserved space |
| `starts_at` | TIMESTAMPTZ | NOT NULL | Booking start |
| `ends_at` | TIMESTAMPTZ | NOT NULL, CHECK > starts_at | Booking end |
| `status` | VARCHAR(20) | NOT NULL | `confirmed`, `cancelled`, or `completed` |
| `created_at` | TIMESTAMPTZ | NOT NULL | Creation time |
| `cancelled_at` | TIMESTAMPTZ | NULL | Cancellation time |

## 5. Integrity and concurrency rules

1. All foreign keys use restrictive behavior unless historical records must be retained; study spaces should be deactivated rather than deleted.
2. Booking creation must run in a transaction.
3. The service must lock or atomically update the relevant space capacity while creating a booking.
4. Active bookings for the same student may not overlap.
5. A booking for an inactive space must be rejected.
6. `starts_at` and `ends_at` must use UTC-aware timestamps.
7. Availability updates must record who made the change and when.
8. Password hashes, access tokens, and secrets must never be stored in logs.

For PostgreSQL, overlapping bookings can be protected with an exclusion constraint using a time range for confirmed bookings, or with an equivalent transactional service rule if booking capacity is modeled per time slot.

## 6. Indexes

Recommended indexes:

```sql
CREATE INDEX idx_study_spaces_active
    ON study_spaces (is_active);

CREATE INDEX idx_study_spaces_location
    ON study_spaces (location_name);

CREATE INDEX idx_bookings_user_time
    ON bookings (user_id, starts_at, ends_at);

CREATE INDEX idx_bookings_space_time
    ON bookings (study_space_id, starts_at, ends_at);

CREATE INDEX idx_availability_updates_space_time
    ON availability_updates (study_space_id, recorded_at DESC);
```

Facility filtering should use indexed join-table lookups. If distance search becomes a primary workload, use a geospatial extension such as PostGIS or a database-supported spatial index.

## 7. Retention and privacy

- Keep cancelled and completed bookings for operational reporting for a defined retention period.
- Provide a process for account deactivation and personal-data deletion where legally required.
- Limit booking and audit data to authorized users.
- Use backups and migration scripts appropriate for the selected deployment environment.
