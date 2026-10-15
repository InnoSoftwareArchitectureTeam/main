# Lab 5 — Software Life Cycle and Development Methodology

## Project and selected approach

**InPlan** automates individual study planning. Students select courses and a specialization, allocate their credit budget, and track academic progress. Lecturers assign marks, while academic office employees manage model study programmes and generate reports. The project baseline consists of the [requirements questions](../lab2/task2.md), the [functional and non-functional requirements](../lab3/task3.md), and the [use case diagram](../lab4/task4.md).

For InPlan, we propose:

- **Software life cycle model: iterative and incremental development.** Build the system through usable additions and improve existing functionality using feedback.
- **Software development methodology: Agile development organized with Scrum**, supported by code review, automated testing, and continuous integration. Scrum is technically a framework; here it provides the concrete team process requested by the assignment.

The model determines how the product evolves. The methodology determines how the team prioritizes, coordinates, checks, and improves its work. Scrum explicitly supports an iterative and incremental approach, so these choices are compatible. See the [Scrum Guide](https://scrumguides.org/scrum-guide.html#scrum-theory).

## Project characteristics and their implications

The repository describes the intended system, but does not specify actual staffing, team experience, delivery dates, deployment scale, or a technology stack. For this proposal, we assume a university pilot developed by **one student team of approximately 4–6 people**, with basic development skills and mixed experience in testing and deployment. We also assume a fixed course deadline and access to stakeholder feedback or an instructor acting as a stakeholder proxy. These are planning assumptions, not established project facts.

| Aspect | Evidence or assumption for InPlan | Implication for the choice |
| --- | --- | --- |
| **1. Product/project type** | A multi-user academic information system with three user groups. Its central problems are course selection, academic rules, budget calculations, and access to records (FR-01–FR-21; NFR-01–NFR-09). | Demonstrating realistic workflows helps users validate the rules and interface. Short iterations expose misunderstandings before they spread to reporting and progress calculations. |
| **2. Project scale** | Lab 3 lists 28 functional and 20 non-functional requirements, including optional features and exclusions. Lab 4 groups the behaviour into three functional areas. We assume an initial pilot at one university; user counts remain unknown. | A single backlog and integrated product are appropriate for this bounded scope. Incremental delivery makes it manageable without introducing coordination across multiple teams. Requirement counts do not establish workload capacity. |
| **3. Team size** | The assumed team has 4–6 members who collectively cover interface, application logic, storage, and testing. | One Scrum Team can coordinate directly and deliver complete user workflows. Separate analysis, implementation, and testing departments would introduce unnecessary handoffs at this scale. |
| **4. Team competence** | We assume basic programming competence but uneven experience with academic rules, authorization, and reliable data updates. | Small changes, peer review, paired work on unfamiliar areas, and regular retrospectives support learning. A shared completion checklist makes quality expectations explicit instead of relying on individual experience. |
| **5. Business factors and bureaucracy** | The academic office is a stakeholder, while students and lecturers have different needs. Lab 2 asks about eligibility, changes after courses start, and course constraints. Actual approval procedures are unspecified. | A designated Product Owner should resolve competing priorities and obtain academic-office decisions on rules. Regular reviews provide feedback, while documented rule decisions preserve accountability. The assumed course deadline makes scope prioritization essential. |
| **6. Artifacts necessity** | Requirements and a use case diagram already exist. Access restrictions, credit calculations, and specialization checks need verifiable interpretations. | Keep these artifacts current and link backlog items to requirement IDs, acceptance examples, and test evidence. Iterative development should maintain useful documentation as behaviour changes. |
| **7. Technological factors** | Browser access is requested in NFR-15; consistency, persistence, and modifiable academic rules appear in NFR-07–NFR-09 and NFR-17. No framework, database, or external integration is selected. | Integrate interface, logic, and storage early, then rerun checks after each change. Validate uncertain implementation choices through small technical experiments. The proposed process does not depend on an invented stack or integration. |

## 1. Software life cycle model: iterative and incremental

### Why this model fits InPlan

**The requirements provide a direction but still need clarification.** For example, FR-13 requires preventing budget overruns, while Lab 2 asks which restrictions apply to course selection. The team needs agreed examples of valid and invalid plans before implementing those rules. A working planning workflow lets the academic office inspect the consequences of its decisions and correct misunderstandings early.

**The product has natural increments with observable value.** Course browsing can be demonstrated before academic reporting is complete. Plan creation then adds value to the catalogue, and marks later enable meaningful progress tracking. Each increment extends an integrated system; it is not just a separate database or an unfinished interface.

**The same rules affect several features.** Credits influence plan validation and progress; marks feed progress and reports. Short integration cycles reveal inconsistencies while the affected change is still small. NFR-08 makes this especially relevant: correct individual screens are insufficient if their calculations disagree.

**A fixed deadline requires visibility into usable results.** An early integrated version shows what actually works. If progress is slower than expected, the team can defer Should Have and Could Have items before they displace mandatory functionality. Frequent delivery and adaptation also align with the [Agile Manifesto principles](https://agilemanifesto.org/principles.html).

### How the life cycle would work

Start with a short shared understanding of the system boundary, roles, academic terminology, data relationships, and major risks. Then repeat the following cycle for each selected workflow:

1. Clarify its requirements with concrete examples and acceptance criteria.
2. Design the necessary interface, data, and component interactions.
3. Implement and integrate the workflow, including its applicable access and validation rules.
4. Test the new behaviour and rerun checks for previously delivered functionality.
5. Make the usable increment available in a test environment and review it with relevant stakeholders.
6. Update requirements, priorities, and the next iteration using the feedback.

Deployment to real users is a separate release decision based on readiness and the university's constraints. After release, defects and academic-rule changes return to the same backlog. Database changes require migration and recovery checks so that improvements preserve existing study plans and marks.

### Example sequence of product increments

This is a proposed dependency order, not a delivery estimate. An increment below may require several Sprints, each delivering a smaller usable result.

| Increment | Usable outcome and requirement coverage | Feedback or risk addressed |
| --- | --- | --- |
| **1. Secure course discovery** | A student can sign in and inspect available courses and their details (FR-01–FR-02), with the relevant authentication and access protections from NFR-01–NFR-06. Start with agreed test catalogue data. | Students check whether credits, costs, and course information are understandable. The team proves that interface, application logic, and storage work together. |
| **2. Validated individual study planning** | Students select a specialization, add/remove courses, see credit and requirement checks, and allocate their budget (FR-03–FR-13). Include data validation, consistency, and persistence (NFR-07–NFR-09). | The academic office checks missing-course and insufficient-credit cases. Budget boundary checks verify that an over-budget change is rejected without corrupting the saved plan. |
| **3. Academic administration and progress** | Academic office employees create model programmes; authorized lecturers assign marks; students view marks and specialization progress (FR-14–FR-19). Enforce the relevant role and ownership restrictions. | Stakeholders verify programme definitions, grade visibility, and how completed courses contribute to progress. |
| **4. Reporting and release completion** | Academic office employees generate reports by field and specialization (FR-20–FR-21). Verify results against known academic records and complete release-wide acceptance checks. | Confirm that reports and student progress use consistent data. Check the complete mandatory scope before release. |

Agree on the catalogue and specialization rules before implementing dependent planning checks; the later programme-management interface must preserve those definitions. Optional improvements, such as filtering and recommendations (FR-25–FR-26), can follow according to priority and capacity. Mandatory protections apply from the first increment that exposes the relevant data or operation.

All Must Have requirements remain in the intended release scope. Intermediate demonstrations do not justify dropping them. The exclusions concerning unconfirmed automatic enrolment and offline operation (FR-28 and NFR-20) also remain unchanged.

### Comparison with other life cycle models

| Alternative | Why it is less suitable for this project |
| --- | --- |
| **Sequential Waterfall** | A largely fixed requirements baseline would be difficult to justify while academic rules and user workflows still need clarification. Discovering a misunderstanding after implementing dependent features would cause broader rework. It would be more attractive if requirements and acceptance procedures were stable and contractually fixed. |
| **V-model** | Its emphasis on matching requirements to verification is useful, and we adopt that traceability. However, a predominantly sequential application would offer less flexibility for the feedback expected here. No formal certification requirement is stated that would justify choosing it as the overall model. |
| **Spiral** | Risk-driven cycles could help if InPlan involved major technical uncertainty or high-risk integrations. Neither is established in the repository. For the assumed small pilot, targeted experiments and a risk list are more proportionate than a formal risk-analysis cycle for every expansion. |
| **Prototyping alone** | Interface prototypes can clarify course selection, but cannot establish reliable persistence, authorization, and consistent calculations. Use prototypes within iterations, then implement and verify production-quality functionality. |

## 2. Development methodology: Agile with Scrum

### Why Scrum fits InPlan

InPlan needs a shared priority order across three stakeholder groups. Otherwise, developers could independently finish catalogue screens, lecturer tools, and reports without producing a complete student workflow. A common Product Goal and a focused Sprint Goal help the team deliver something that can be inspected together.

We propose **two-week Sprints** as an initial cadence: long enough to integrate and verify a small workflow, but short enough to receive feedback during the assumed course project. The team should select scope using its actual availability and observed progress; the duration does not imply that every increment in the table takes two weeks.

The following is a proposed InPlan working arrangement, using the accountabilities and events defined in the [Scrum Guide](https://scrumguides.org/scrum-guide.html).

- **Product Owner:** designate one person to order the backlog, maintain the release scope, and clarify rules with academic office representatives while considering students and lecturers. In the course setting, a team member can act as a proxy, recording which decisions still need validation.
- **Scrum Master:** designate a team member to help the group use Scrum, resolve coordination problems, and follow through on process improvements. This need not be a separate full-time position.
- **Developers:** the team jointly owns implementation, testing, integration, and documentation. Work allocation follows the Sprint Goal rather than permanent component silos.

### Working rhythm

At **Sprint Planning**, choose one demonstrable goal, such as allowing a student to edit a budget-valid study plan. Select related backlog items and agree on examples of acceptable behaviour. Hold a **15-minute Daily Scrum** on each working day to coordinate progress and blockers. Continue refining upcoming work as questions are answered.

At the **Sprint Review**, inspect the working result with the relevant users or stakeholder proxy and revise priorities. At the **Sprint Retrospective**, select a concrete improvement, such as adding authorization checks earlier after an access-control defect. The review provides feedback; it does not replace testing or act as a mandatory release gate.

For the assumed small team and two-week cadence, start with about one hour of planning, 45 minutes of review, and 30 minutes of retrospective, adjusting within Scrum's event limits when necessary. These are proposed meeting lengths, not measured team practice.

### Artifacts and engineering discipline

Maintain a Product Backlog with a Product Goal, a Sprint Backlog with a Sprint Goal, and a usable Increment satisfying a shared Definition of Done. For InPlan, the proposed Product Goal is to let students manage valid individual plans while authorized staff maintain academic records and obtain consistent reports.

Each backlog item should link to the relevant FR/NFR IDs and include acceptance examples. Preserve the requirements, use case diagram, important academic-rule decisions, test results, and release instructions in version control. GitHub issues or a simple board can track work; a separate management platform is unnecessary for the assumed team.

An item is **Done** when:

1. Its agreed behaviour and relevant requirements are implemented and verified.
2. Another team member has reviewed the change, and automated checks pass.
3. Applicable access, validation, and persistence checks pass, including failure cases.
4. It integrates with earlier functionality without known blocking regressions.
5. Affected documentation and test-environment deployment instructions are current.

For example, a budget item needs checks at and above the available limit; a marks item needs checks that unauthorized lecturers cannot modify a mark. Continuous integration should run these checks after changes. Peer review and paired work on difficult rules complement Scrum, which does not prescribe the implementation techniques.

For performance requirements NFR-11–NFR-13, first agree on representative data volume and concurrent-user workload. Then measure the stated two-second operation and ten-second report targets under that workload. Without it, the team cannot claim those targets are verified. Retain the priorities recorded in Lab 3 when planning these checks.

### Comparison with other development approaches

| Alternative | Assessment for InPlan |
| --- | --- |
| **Kanban** | A credible option, especially for later maintenance with unpredictable incoming requests. For the assumed initial course project, Scrum's explicit goals and scheduled reviews provide useful coordination and feedback. Kanban could also provide a review cadence, but the team would need to define that arrangement itself. |
| **Extreme Programming (XP)** | Its testing, integration, and collaboration practices are useful for reliable academic calculations. Scrum provides our primary structure for stakeholder priorities and delivery; selected XP practices strengthen implementation. The repository does not establish that the team can sustain all XP practices, such as an on-site customer. |
| **A heavily tailored Unified Process** | Architecture and traceability are valuable, but a large set of roles and formal documents would consume a substantial share of the assumed small team's capacity. Keep the artifacts needed to explain decisions and verify behaviour, without introducing a process structure unsupported by the project's scale. |

### Conditions and limitations

The recommendation depends on regular feedback, a manageable team size, and authority to adjust backlog priorities. If academic staff are unavailable, record unresolved rules and seek proxy feedback without presenting it as university approval. If the team cannot maintain the core Scrum events and accountabilities, a simpler Kanban process would be a more honest and practical choice. If deployment introduces strict approval gates or major integration risks, add the necessary release controls and reassess the life cycle assumptions.

With the stated assumptions, iterative and incremental development addresses InPlan's evolving academic rules and connected workflows, while Scrum gives the team a concrete way to prioritize and inspect progress. Testing, traceable decisions, and incremental integration make the approach suitable for a system where incorrect plans, budgets, or marks would directly affect users.
