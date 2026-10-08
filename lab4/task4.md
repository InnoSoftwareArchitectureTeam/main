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
