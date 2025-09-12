---
layout: project
type: project
image: img/university/university.jpg
title: "University Course Registration System"
date: 2025
published: true
labels:
  - C++
  - Programming
summary: "A C++ program I made for my ICS 212 class that maintains a University Course Registration System."
---

In my ICS 212 class, one of my assignments was to design and implement a University Course Registration System C++ program using object-oriented programming concepts. This program allows students to be added to the university system, courses to be created, and registration for courses. Some of the requirements included preventing duplicate course registrations and students, enforcing an enrollment limit for the courses, and validating input such as date format and numeric entries.

The purpose of this assignment was to practice using C++. Previously, we had been learning how to use C. Unlike C, C++ is an object-oriented programming language. Throughout this program, I implemented oop concepts such as classes, encapsulation, and polymorphism.

Here is some of the code I wrote for this program. This is the Course class:

```cpp
class Course {
private:
  string code, title, instructor, ids[MAX_ENROLLMENT];
  int enrollment;

public:
  Course() {}
  Course(string code, string title, string instructor)
    : code(code), title(title), instructor(instructor), enrollment(0) {}

  string getCode() { return code; }
  string getTitle() { return title; }
  string getInstructor() { return instructor; }
  int getEnrollment() { return enrollment; }

  // Register student - checks and update enrollment
  bool registerStudent(string id) {
    if (enrollment == MAX_ENROLLMENT) // check if course is full
      return false;

    for (int i = 0; i < MAX_ENROLLMENT; i++) {
      if (ids[i].compare(id) == 0) // check if student already registered
        break;

      if (ids[i].empty()) { // look for empty space to add student
        ids[i] = id;
        enrollment++; // update enrollment
        return true; // successful
      }
    }
    return false; // unsucessful
  }

  // Remove student - updates enrollment
  bool removeStudent(string id) {
    for (int i = 0; i < MAX_ENROLLMENT; i++) {
      if (ids[i].compare(id) == 0) {
        for (int j = i; j < MAX_ENROLLMENT - 1; j++) { // remove student
          ids[j] = ids[j + 1];
        }
        ids[MAX_ENROLLMENT - 1] = ""; // edge case - clear last index
        enrollment--; // update enrollment
        return true; // successful
      }
    }
    return false; // unsuccessful
  }
};
```