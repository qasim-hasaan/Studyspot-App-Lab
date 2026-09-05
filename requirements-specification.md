# StudySpot Requirements Specification

## 1. Purpose

This document defines the functional and non-functional requirements for the StudySpot MVP. The MVP helps university students find available study spaces and reserve a suitable space.

## 2. Product context

StudySpot is a responsive web application for a single university. It presents approved study spaces, their facilities, current availability, and booking options.

## 3. User roles

### Student

Can browse spaces, apply filters, view availability, create an account, make bookings, and cancel their own future bookings.

### Administrator

Can create and update study spaces, manage facilities, update availability, review bookings, and deactivate spaces.

### Availability manager

Can update seat availability for assigned spaces but cannot manage users or system configuration.

## 4. Functional requirements

### FR-01 Account access

The system shall allow a student to register, sign in, sign out, and reset a forgotten password.

### FR-02 Browse study spaces

The system shall display approved study spaces with their name, location, study type, capacity, available seats, facilities, and last-updated time.

### FR-03 Search

The system shall allow users to search study spaces by name or location.

### FR-04 Filter study spaces

The system shall allow users to filter by:

- Quiet study
- Group study
- Wi-Fi
- Power outlets
- Minimum available seats
- Maximum distance

### FR-05 Sort results

The system shall allow users to sort results by distance, available seats, and most recently updated availability.

### FR-06 Study-space details

The system shall provide a detail page with description, address or campus location, opening hours, facilities, capacity, current availability, and booking rules.

### FR-07 Availability updates

The system shall store the available-seat count and the time it was last updated.

### FR-08 Booking

The system shall allow an authenticated student to reserve an available study space for a permitted time period.

### FR-09 Booking validation

The system shall reject a booking when the space is inactive, the requested period is invalid, the student already has a conflicting booking, or no capacity remains.

### FR-10 Booking management

The system shall allow a student to view upcoming and past bookings and cancel an eligible upcoming booking.

### FR-11 Administration

The system shall allow authorized administrators to create, edit, activate, and deactivate study spaces.

### FR-12 Availability administration

The system shall allow authorized staff to update seat availability and retain the update timestamp and updater identity.

### FR-13 Auditability

The system shall record booking creation, cancellation, availability changes, and study-space status changes.

### FR-14 Error handling

The system shall show a clear user-facing error when an operation fails and shall not report a booking as successful unless it has been committed.

## 5. Non-functional requirements

### NFR-01 Performance

For normal pilot load, search and filtered results should be returned within two seconds at the 95th percentile.

### NFR-02 Availability

The service should be available during the university's published operating hours, excluding planned maintenance.

### NFR-03 Security

- Passwords shall be stored using a strong one-way password hash.
- Authorization shall be enforced on every administrative operation.
- Users shall only access and cancel their own bookings.
- Input shall be validated on the server.
- Database queries shall use parameterized statements or an equivalent safe data-access layer.

### NFR-04 Privacy

The system shall collect only data needed for accounts, bookings, and administration. A student's booking history shall not be publicly visible.

### NFR-05 Usability

The primary search and booking flow shall be usable on desktop and mobile viewport sizes.

### NFR-06 Accessibility

The interface should target WCAG 2.1 AA practices, including keyboard navigation, visible focus, meaningful labels, and sufficient color contrast.

### NFR-07 Data integrity

The database shall enforce unique identifiers, valid relationships, non-negative seat counts, and booking conflict rules.

### NFR-08 Observability

Application errors and important administrative changes shall be logged without exposing passwords, tokens, or unnecessary personal data.

## 6. Business rules

1. Only active study spaces may be displayed as bookable.
2. Available seats cannot be negative or greater than capacity.
3. A student cannot hold overlapping bookings.
4. A booking cannot exceed the space's configured booking window.
5. Availability must display its last-updated timestamp.
6. Deactivating a space must prevent new bookings but preserve historical bookings.

## 7. MVP release boundary

The MVP is complete when FR-01 through FR-14 and the critical NFRs for security, data integrity, usability, and performance are implemented and meet the acceptance criteria in `acceptance-criteria.md`.
