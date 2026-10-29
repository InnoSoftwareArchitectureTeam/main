# Lab 7 — UML Sequence Diagram

A student views progress toward a specialization. This simple example assumes the student is authenticated and has one passed course accepted by the specialization.

![InPlan sequence diagram](sequence-diagram.svg)

The system checks that the course is eligible, obtains its earned credits, finds missing core courses, and returns an AcademicProgress object. The UI then reads the remaining credits, completion percentage, and completion status.

The result uses the enrollment's credit snapshot, the specialization's required credits, and the missing core courses. Completion requires both enough credits and all core courses. Other histories and error paths are outside this example.

## Assignment checklist

| Requirement | Result |
| --- | --- |
| At least 4 components | 6 existing classes, plus the user actor. |
| At least 8 method calls | 9 numbered calls; returns and object creation are excluded. |
| Logical sequence | Request progress, check the course and mark, calculate the result, display progress. |
| Existing classes and methods | All names and method signatures come from the [Lab 6 class diagram](../lab6/class-diagram.puml). |

The create message initializes AcademicProgress; it does not add a method to the class diagram. The sequence describes the proposed design, not an implemented application trace.

Files: [PlantUML source](sequence-diagram.puml), [SVG](sequence-diagram.svg), [PNG](sequence-diagram.png).
