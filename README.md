# DeskFlow – SLA Ticket Triage & Escalation Engine

![Java](https://shields.io)
![Spring Boot](https://shields.io)
![MySQL](https://shields.io)
![DSA](https://shields.io)
![Postman](https://shields.io)

Support ticket backend built with **Core Java** and **Spring Boot** to log, prioritize, and track technical issues across `OPEN`, `IN_PROGRESS`, and `RESOLVED` states.

## Architecture & Applied DSA
- **Severity Triage (`PriorityQueue`):** Implements a Min-Heap `PriorityQueue` with a custom Java `Comparator` so `CRITICAL` SLA tickets always assign ahead of `LOW` severity issues in O(log n) time.
- **Server-Side Pagination:** Uses Spring Data pagination to load ticket histories cleanly without heavy database queries.
- **Global Error Handling (`@ControllerAdvice`):** Returns structured JSON error messages and accurate HTTP status codes for invalid ticket updates.

## Core API Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `POST` | `/api/tickets` | Create new issue and insert into `PriorityQueue` |
| `GET` | `/api/tickets/next` | Poll highest-priority open ticket for engineer assignment |
| `PUT` | `/api/tickets/{id}/status` | Update ticket state (`OPEN` -> `IN_PROGRESS` -> `RESOLVED`) |
