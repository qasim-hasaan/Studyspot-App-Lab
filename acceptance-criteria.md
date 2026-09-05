# StudySpot Acceptance Criteria

## 1. Acceptance approach

Acceptance tests use the format **Given / When / Then**. Unless stated otherwise, the tester is using a supported modern browser and test data belongs to the pilot university.

## 2. Account and access

### AC-01 Student registration

**Given** a visitor provides a valid email and password  
**When** they submit registration  
**Then** an account is created and the user can sign in.

### AC-02 Invalid registration

**Given** an email is already registered or required data is invalid  
**When** registration is submitted  
**Then** the account is not created and a clear validation message is shown.

### AC-03 Role authorization

**Given** a student is signed in  
**When** they request an administrator-only operation  
**Then** access is denied and no data is changed.

## 3. Discovery and filtering

### AC-04 Browse spaces

**Given** active study spaces exist  
**When** a user opens the study-space catalogue  
**Then** each result shows name, location, study type, available seats, facilities, and last-updated time.

### AC-05 Apply filters

**Given** spaces have different facilities and study types  
**When** the user selects quiet study, Wi-Fi, power outlets, a minimum seat count, or a distance limit  
**Then** every displayed result satisfies all selected filters.

### AC-06 No matching spaces

**Given** no space satisfies the selected filters  
**When** the filters are applied  
**Then** the system shows an empty-state message and provides a way to clear filters.

### AC-07 Space details

**Given** a study-space result is displayed  
**When** the user opens it  
**Then** the detail view includes location, opening hours, capacity, facilities, availability, and booking rules.

## 4. Availability and booking

### AC-08 Availability freshness

**Given** availability has been updated  
**When** a user views the space  
**Then** the available-seat count and last-updated timestamp are shown.

### AC-09 Successful booking

**Given** an authenticated student selects an active space and valid available period  
**When** they confirm the booking  
**Then** exactly one booking is created and a confirmation is displayed with the space, period, and booking identifier.

### AC-10 Prevent overbooking

**Given** no seats remain or another transaction consumes the final available capacity  
**When** the student confirms a booking  
**Then** the booking is rejected and the system displays the current availability.

### AC-11 Prevent conflicting bookings

**Given** a student already has a booking overlapping the requested period  
**When** they attempt another booking  
**Then** the second booking is rejected with a clear conflict message.

### AC-12 Cancel booking

**Given** a student has an eligible future booking  
**When** they cancel it  
**Then** the booking is marked cancelled, it is no longer counted as active, and the student sees confirmation.

### AC-13 Booking history

**Given** a student has bookings  
**When** they open their bookings page  
**Then** they can distinguish upcoming, cancelled, and completed bookings.

## 5. Administration

### AC-14 Manage study spaces

**Given** an authorized administrator  
**When** they create or edit a study space with valid data  
**Then** the space is saved and appears according to its active status.

### AC-15 Deactivate a space

**Given** an active space has future bookings  
**When** an administrator deactivates it  
**Then** new bookings are blocked, historical records remain available, and the administrator receives a warning about affected future bookings.

### AC-16 Update availability

**Given** an authorized availability manager enters a count between zero and capacity  
**When** the update is saved  
**Then** the count and update timestamp change and the updater is recorded.

## 6. Security, quality, and usability

### AC-17 Data isolation

**Given** a signed-in student  
**When** they request another student's booking data  
**Then** the request is denied.

### AC-18 Validation and integrity

**Given** invalid, negative, or out-of-range values are submitted  
**When** the server processes them  
**Then** the request is rejected and the database remains unchanged.

### AC-19 Responsive experience

**Given** a supported mobile or desktop viewport  
**When** the user searches, filters, views details, and books  
**Then** the primary actions remain usable without horizontal scrolling.

### AC-20 Performance target

**Given** representative pilot data and normal pilot load  
**When** a user searches or applies filters  
**Then** 95% of responses complete within two seconds.

## 7. Release decision

The MVP is accepted when all critical criteria (AC-03, AC-09 through AC-12, AC-16 through AC-18) pass, no severity-one defects remain open, and the product owner approves the pilot release.
