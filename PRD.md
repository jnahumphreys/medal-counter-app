# Product Requirements Document (PRD)

## Product Name
**Olympic Medal Counter**

![image](https://github.com/user-attachments/assets/368adf1d-0fd0-44d1-a581-01e3e1739165)


---

## Purpose

The Olympic Medal Counter is a lightweight, fast, and accessible web application that allows users to view the top-performing countries in an Olympic-style medal table.

Users can easily view the top 10 countries by medal count and re-sort the list by gold, silver, bronze, or total medals.

The product is optimized for clarity, accessibility, and performance, with a focus on clean design and minimal user friction.

---

## Target Audience

- Sports fans wanting a quick overview of top medal standings
- Reporters or analysts looking for a fast reference

---

## User Goals

- ✅ See the top 10 countries by Olympic medal count
- ✅ Easily change the sort order (gold, silver, bronze, total)
- ✅ Understand which country is leading based on the current sorting
- ✅ Share or revisit the app with a consistent sort order reflected in the URL
- ✅ Be informed if data is unavailable or if an error occurs

---

## Functional Requirements (MVP)

### Must-Have Features

- Display a table showing the top 10 countries by medal count.
- Show medal counts for gold, silver, bronze, and total.
- Include visual flags for each country.
- Allow the user to sort the table by:
  - Gold
  - Silver
  - Bronze
  - Total
- In the event of a tie (e.g. two countries with the same gold count), the secondary and tertiary medal counts will be used to determine ranking (e.g. silver, then bronze). If still tied, alphabetical order (by country code) will be used.
- Visually indicate which sort is currently active.
- Respect the `?sort=` URL parameter and update the UI accordingly.
- Update the URL when a new sort is selected (without reloading).
- Fallback to a default sort (`gold`) if the parameter is missing or invalid.
- Show an error message if data fails to load, with an option to retry.

---

## Will Not Include (Intentionally Out of Scope for MVP)

- Country detail pages or click-throughs
- Live medal data from external APIs
- Search or filtering by country
- Custom sorting beyond medal types
- User preferences or authentication
- Historical data views (past games)
- Pagination (only top 10 will be shown)
- Fully accessible to keyboard and screen readers.
- Responsive across common mobile and desktop breakpoints.

---

## Future Considerations

- Pagination to view more than 10 countries
- Data visualizations (e.g. bar charts or medal breakdowns)
- Live data from an official source or API
- Light/dark mode toggle
- Internationalization (i18n) and multi-language support
- Animated sorting transitions for improved UX
- Ability to "pin" a country or compare two countries side-by-side
- Full accesibility support

---

## Success Metrics

- ✅ User can load and sort the medal table in under 2 seconds.
- ✅ UI works on desktop without layout bugs.
- ✅ Sort preference is reflected in the URL and persists on refresh.
- ✅ App handles missing or malformed data gracefully.

---

## Delivery Format

The app will be delivered as a single-page web application that can be hosted statically or embedded into a broader site.  
It is designed to be portable, dependency-light, and easy to maintain or hand off.

---

## Review Notes

This PRD defines the what, not the how. It focuses on user experience and functionality rather than implementation details. Technical architecture, tooling, and testing strategy are documented separately.
