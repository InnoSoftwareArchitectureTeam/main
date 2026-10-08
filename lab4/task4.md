@startuml
title InPlan — Use Case Diagram

left to right direction
skinparam packageStyle rectangle
skinparam shadowing false
skinparam actorStyle awesome

actor "Authenticated User" as User
actor Student
actor Lecturer
actor "Academic Office Employee" as AcademicOffice

Student --|> User
Lecturer --|> User
AcademicOffice --|> User

rectangle "InPlan System" {
  package "Identity and Access" {
    usecase "Authenticate" as UC_Authenticate
  }

  package "Study Plan Management" {
    usecase "Browse Course Catalogue" as UC_BrowseCourses
    usecase "View Course Details" as UC_ViewCourse
    usecase "Filter Courses" as UC_FilterCourses
    usecase "Add Course to Study Plan" as UC_AddCourse
    usecase "Remove Course from Study Plan" as UC_RemoveCourse
    usecase "Select Specialization" as UC_SelectSpecialization
    usecase "Validate Study Plan" as UC_ValidatePlan
    usecase "Check Course Prerequisites" as UC_CheckPrerequisites
    usecase "Verify Specialization\nRequirements" as UC_VerifySpecialization

usecase "Calculate Total Credits" as UC_CalculateCredits
    usecase "Calculate Total Cost" as UC_CalculateCost
    usecase "Allocate Credit Budget" as UC_AllocateBudget
    usecase "Compare with Model\nStudy Programme" as UC_ComparePlan
    usecase "Recommend Additional Courses" as UC_RecommendCourses
    usecase "Notify about Missing\nRequirements" as UC_NotifyMissing
  }

  package "Academic Administration and Reporting" {
    usecase "Manage Model Study Programme" as UC_ManageModel
    usecase "Define Courses in\nModel Programme" as UC_DefineModelCourses
    usecase "Assign Marks" as UC_AssignMarks
    usecase "View Marks" as UC_ViewMarks
    usecase "Track Academic Progress" as UC_TrackProgress
    usecase "Generate Academic\nPerformance Report" as UC_GenerateReport
    usecase "Report by Field of Study" as UC_ReportByField
    usecase "Report by Specialization" as UC_ReportBySpecialization
  }
}

User -- UC_Authenticate

Student -- UC_BrowseCourses
Student -- UC_AddCourse
Student -- UC_RemoveCourse
Student -- UC_SelectSpecialization
Student -- UC_AllocateBudget
Student -- UC_ComparePlan
Student -- UC_ViewMarks
Student -- UC_TrackProgress

Lecturer -- UC_AssignMarks

AcademicOffice -- UC_ManageModel
AcademicOffice -- UC_GenerateReport

UC_BrowseCourses ..> UC_ViewCourse : <<include>>
UC_BrowseCourses ..> UC_FilterCourses : <<include>>
UC_AddCourse ..> UC_ValidatePlan : <<include>>
UC_SelectSpecialization ..> UC_VerifySpecialization : <<include>>
UC_ValidatePlan ..> UC_CheckPrerequisites : <<include>>
UC_ValidatePlan ..> UC_VerifySpecialization : <<include>>
UC_ValidatePlan ..> UC_CalculateCredits : <<include>>
UC_AllocateBudget ..> UC_CalculateCost : <<include>>
UC_ManageModel ..> UC_DefineModelCourses : <<include>>
UC_TrackProgress ..> UC_CalculateCredits : <<include>>

UC_NotifyMissing ..> UC_VerifySpecialization : <<extend>>
UC_RecommendCourses ..> UC_TrackProgress : <<extend>>

UC_ReportByField --|> UC_GenerateReport
UC_ReportBySpecialization --|> UC_GenerateReport

legend right
  -- Association
  ..> <<include>> Mandatory reused behavior
  ..> <<extend>> Optional or conditional behavior
  --|> Generalization
endlegend

@enduml
