# StudySpot

**Stop searching. Start studying.**

StudySpot is a responsive web application concept that helps university students quickly find a suitable and available place to study. Students can discover nearby study spaces, check available seats, filter spaces by their needs, and reserve a suitable location.

## Problem

University students often waste time looking for a quiet and available place to study. Libraries may be crowded, and students may not know which locations provide Wi-Fi, power outlets, group-study areas, or open seats.

StudySpot brings this information together in one place so students can choose a study space based on their current needs.

## MVP features

- Find available study spaces nearby.
- View available-seat counts and the last availability update.
- Filter spaces by:
  - Quiet study
  - Group study
  - Wi-Fi
  - Power outlets
  - Minimum available seats
  - Distance
- View study-space details, facilities, capacity, and opening hours.
- Reserve an available study space.
- View and cancel eligible bookings.
- Manage study spaces and availability through authorized administration features.

## Target users

| User | Main activities |
|---|---|
| Students | Search, filter, compare, and reserve study spaces |
| Availability managers | Update available-seat information |
| Administrators | Manage study spaces, facilities, users, and bookings |

## Project scope

The first release is designed for one university. It focuses on the core discovery, availability, filtering, and booking experience.

The following are planned for later phases:

- Multiple university support
- Partnerships with cafés and private study spaces
- Premium listings and student features
- Advertising and university partnerships
- Automated occupancy detection
- Native mobile applications

## Documentation

Project documentation is available in the [`docs`](./docs) folder:

- [Project Charter](./docs/project-charter.md)
- [Requirements Specification](./docs/requirements-specification.md)
- [Acceptance Criteria](./docs/acceptance-criteria.md)
- [Database Design](./docs/database-design.md)

## Product vision

Make finding an appropriate study space on campus as simple as searching for a destination.

## Success measures

- A student can find a suitable space and complete a booking in under two minutes.
- At least 90% of pilot users can locate a space using filters without assistance.
- Availability information includes a visible last-updated time.
- The system prevents double bookings and booking conflicts.
- Search and filtered results return within two seconds for 95% of normal pilot requests.

## Suggested technology

The database design recommends a relational database such as PostgreSQL. The final frontend and backend technology can be selected according to the implementation team's requirements.

Core technical expectations include:

- Secure authentication and role-based authorization
- Server-side input validation
- Transactional booking operations
- Foreign keys and database constraints
- Responsive desktop and mobile layouts
- WCAG 2.1 AA accessibility practices

## Example user flow

1. A student opens StudySpot.
2. The student searches for a nearby study space.
3. The student applies filters such as quiet, Wi-Fi, and available seats.
4. The student opens a matching space to review details and availability.
5. The student signs in and reserves the space.
6. StudySpot shows the booking confirmation and stores the booking in the student's account.

## Project status

This repository currently contains the project planning and requirements documentation for the StudySpot MVP. Application implementation can be added as development progresses.

## Repository

The project is intended for the public repository:

<https://github.com/qasim-hasaan/Studyspot-App-Lab>

## License

No license has been selected yet. Add a license before distributing or reusing the project publicly.
