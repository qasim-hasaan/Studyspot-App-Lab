# StudySpot Project Charter

## 1. Project overview

**StudySpot** is a web application that helps university students find a suitable study space quickly. It addresses the common problem of searching across crowded libraries and unavailable rooms by showing study spaces, seat availability, facilities, and distance in one place.

**Tagline:** Stop searching. Start studying.

## 2. Background and problem statement

Interviews with university students identified four recurring problems:

- Empty study spaces are difficult to find.
- Libraries and popular study areas are often crowded.
- Students waste time walking between locations to find a suitable place.
- Information about Wi-Fi, power outlets, quietness, group-study suitability, and available seats is not easy to discover.

Students need a fast and reliable way to choose a study location based on their current needs.

## 3. Product vision

Make finding an appropriate study space on campus as simple as searching for a destination.

## 4. Objectives

1. Help students discover nearby study spaces.
2. Show current or most recently reported seat availability.
3. Enable filtering by study environment and facilities.
4. Allow students to reserve an available study space.
5. Validate a startup-ready MVP that can launch at one university and expand to other universities.

## 5. Scope

### In scope for the MVP

- Student browsing of study spaces.
- Study-space details: name, location, distance, type, facilities, and capacity.
- Availability display with available-seat counts.
- Filters for quiet study, group study, Wi-Fi, power outlets, and distance.
- Authenticated booking and booking cancellation.
- Basic administration of study spaces and availability.

### Out of scope for the MVP

- Payments and premium subscriptions.
- Advertising and sponsored listings.
- Multi-university tenancy and cross-campus analytics.
- Automated occupancy detection through sensors or computer vision.
- Native mobile applications.

## 6. Stakeholders and users

| Stakeholder | Interest and responsibility |
|---|---|
| Students | Find, compare, and reserve study spaces |
| University administrators | Maintain approved spaces and monitor usage |
| Study-space staff | Provide or validate availability information |
| Product team | Research, design, build, and measure the MVP |
| Future partners | Supply cafés and private study spaces during expansion |

## 7. Deliverables

- Responsive StudySpot website.
- Study-space catalogue and availability workflow.
- Search and filtering experience.
- Booking workflow.
- Administration workflow for spaces and availability.
- Requirements, acceptance criteria, and database design documentation.

## 8. Success measures

- A student can find a suitable space and complete a booking in under two minutes.
- At least 90% of tested users can locate a space using filters without assistance.
- Availability shown by the system is updated within the agreed operational window.
- Booking conflicts are prevented by the system.
- Pilot users report reduced time spent searching for a study location.

## 9. Assumptions and constraints

- The initial deployment serves one university.
- Availability may initially be maintained by staff or authorized users rather than sensors.
- Users have access to a modern web browser and an internet connection.
- The MVP uses a relational database.
- Location and availability data must be treated as potentially changeable and time-sensitive.

## 10. Risks and mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| Availability data becomes stale | Students lose trust | Show last-updated time and provide authorized update workflows |
| Double bookings | Poor user experience | Use database constraints and transactional booking logic |
| Low initial catalogue coverage | Limited usefulness | Start with high-demand university locations and expand gradually |
| Privacy concerns | Compliance and trust issues | Minimize personal data and restrict access to booking information |
| Demand exceeds capacity | Users cannot find spaces | Add waitlist or partner spaces in a later release |

## 11. Milestones

| Milestone | Outcome |
|---|---|
| Discovery | Validate student needs and priority filters |
| Design | Produce user flows, wireframes, and data model |
| MVP build | Implement discovery, availability, filtering, and booking |
| Pilot | Launch at one university with selected study spaces |
| Evaluation | Measure usage, accuracy, and user satisfaction |
| Expansion planning | Assess additional universities and external partners |

## 12. Approval

This charter establishes the MVP direction. Changes to scope, privacy expectations, booking rules, or the initial target university should be reviewed by the product owner before implementation.
