# lab3

# InPlan — Functional Requirements

## Overview

InPlan is a system for automating individual study plan creation.

The system allows students to choose courses, build an individual study plan, track progress toward a specialization, and distribute their credit budget across paid courses.

The academic office can create model study programs and receive reports on academic performance. Lecturers can assign marks to students.

## Functional Requirements

| ID | Requirement | Priority |
|---|---|---|
| FR-01 | The system shall allow students to view the list of available courses. | Must Have |
| FR-02 | The system shall display course information, including course requirements, number of credits, field of study, and cost. | Must Have |
| FR-03 | The system shall allow students to select courses for their individual study plan. | Must Have |
| FR-04 | The system shall allow students to remove previously selected courses from their study plan. | Must Have |
| FR-05 | The system shall allow students to select a specialization. | Must Have |
| FR-06 | The system shall display the list of core courses required for the selected specialization. | Must Have |
| FR-07 | The system shall calculate the total number of credits in the student's study plan. | Must Have |
| FR-08 | The system shall verify whether the selected courses satisfy the specialization requirements. | Must Have |
| FR-09 | The system shall notify the student if mandatory core courses for the selected specialization are missing. | Must Have |
| FR-10 | The system shall notify the student if the total credit requirement for the specialization is not satisfied. | Must Have |
| FR-11 | The system shall allow students to allocate their available credit budget across selected courses. | Must Have |
| FR-12 | The system shall calculate the total cost of selected courses. | Must Have |
| FR-13 | The system shall prevent the student from exceeding the available credit budget. | Must Have |
| FR-14 | The system shall allow the academic office to create model study programmes. | Must Have |
| FR-15 | The system shall allow the academic office to define courses included in a model study programme. | Must Have |
| FR-16 | The system shall allow lecturers to assign marks to students for courses they teach. | Must Have |
| FR-17 | The system shall allow students to view their marks. | Must Have |
| FR-18 | The system shall allow students to track their academic progress. | Must Have |
| FR-19 | The system shall calculate progress toward completion of the selected specialization. | Must Have |
| FR-20 | The system shall allow the academic office to generate reports on academic performance by field of study. | Must Have |
| FR-21 | The system shall allow the academic office to generate reports on academic performance by specialization. | Must Have |
| FR-22 | The system should show students how many credits remain to complete their specialization. | Should Have |
| FR-23 | The system should warn students when a selected course does not satisfy its prerequisites. | Should Have |
| FR-24 | The system should allow students to compare their individual study plan with a model study programme. | Should Have |
| FR-25 | The system should provide filtering of courses by field of study, credits, and specialization. | Should Have |
| FR-26 | The system could recommend additional courses that help the student satisfy specialization requirements. | Could Have |
| FR-27 | The system could provide a dashboard showing academic progress, budget usage, and remaining credits. | Could Have |
| FR-28 | The system will not automatically enroll students in courses without their confirmation. | Won't Have |

# InPlan — Non-Functional Requirements

## Overview

The following non-functional requirements define the expected quality attributes of the InPlan system.

The requirements are written so that they can be objectively verified where possible.

## Non-Functional Requirements

| ID | Requirement | Priority |
|---|---|---|
| NFR-01 | The system shall require authentication before providing access to personal academic information. | Must Have |
| NFR-02 | The system shall provide role-based access control for students, lecturers, and academic office employees. | Must Have |
| NFR-03 | Students shall only be able to modify their own study plans. | Must Have |
| NFR-04 | Lecturers shall only be able to assign or modify marks for courses for which they are authorized. | Must Have |
| NFR-05 | Academic office users shall have access to study programme management and academic reporting functions. | Must Have |
| NFR-06 | The system shall protect student academic and personal data from unauthorized access. | Must Have |
| NFR-07 | The system shall validate all course, credit, budget, and specialization data before saving changes. | Must Have |
| NFR-08 | The system shall preserve consistency between selected courses, calculated credits, course costs, and specialization requirements. | Must Have |
| NFR-09 | The system shall prevent loss of confirmed study-plan and mark data during normal system operation. | Must Have |
| NFR-10 | The system shall record changes to critical academic data, including marks and study plans. | Should Have |
| NFR-11 | The system should return normal user operations within 2 seconds under expected workload. | Should Have |
| NFR-12 | Academic reports should be generated within 10 seconds under expected workload. | Should Have |
| NFR-13 | The system should support concurrent access by students, lecturers, and academic office employees. | Should Have |
| NFR-14 | The user interface should clearly display validation errors when a study plan violates course, credit, specialization, or budget constraints. | Should Have |
| NFR-15 | The system should be usable through modern desktop web browsers. | Should Have |
| NFR-16 | The system should maintain a clear separation between academic data, user data, and reporting functionality to support maintainability. | Should Have |
| NFR-17 | The system should support modification of course and specialization rules without requiring changes to unrelated system functionality. | Should Have |
| NFR-18 | The system could provide responsive support for tablets and mobile devices. | Could Have |
| NFR-19 | The system could provide notifications about incomplete study plans or missing specialization requirements. | Could Have |
| NFR-20 | Offline operation will not be supported in the initial version. | Won't Have |