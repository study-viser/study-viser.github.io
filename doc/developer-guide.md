# StudyViser Developer Guide

## 1. Overview

StudyViser is a collaborative study-material platform designed for students, instructors, and teaching assistants (TAs). The system allows instructors to define course study needs, students to submit definitions or resources for extra credit, and TAs/instructors to review and approve high-quality submissions into official course materials.

This guide explains how developers can install, run, and contribute to the project.

## 2. Tech Stack

- Frontend: Next.js, React
- Styling: Bootstrap 5 / React Bootstrap
- Forms: React Hook Form
- Authentication: NextAuth.js
- Database ORM: Prisma
- Database: PostgreSQL
- Testing: Playwright
- Linting: ESLint
- CI/CD: GitHub Actions

## 3. Installation and Setup

### 3.1 Prerequisites

- Node.js v18+
- npm
- PostgreSQL

### 3.2 Clone the Repository

```bash
git clone https://github.com/your-org/studyviser.git
cd studyviser
```   

### 3.3 Install Dependencies

```bash
npm install
```

### 3.4 Configure Environment Variables

Create a .env file in the project root:

```bash
DATABASE_URL="postgresql://user:password@localhost:5432/studyviser"
NEXTAUTH_SECRET="your-secret-key"
NEXTAUTH_URL="http://localhost:3000"
```

### 3.5 Set Up Database

```bash
npx prisma migrate dev
npx prisma generate
npx prisma db seed
```

## 4. Running the Application

```bash 
npm run dev
```

Open the app at:

```bash
http://localhost:3000
```

## 5. Project Structure

```bash
.
├── doc/
│   └── developer-guide.md
├── prisma/
│   ├── schema.prisma
│   └── migrations/
├── public/
├── src/
│   ├── app/
│   ├── components/
│   └── lib/
│   └── styles/
├── tests/
├── .github/
│   └── workflows/
└── README.md
```

## 6. User Roles

### Student
* Join courses
* View assigned terms
* Submit definitions or resources
* Earn extra credit

### Instructor
* Create courses
* Define weekly topics and terms
* Review and approve submissions

### Teaching Assistant
* Review student submissions
* Approve or reject entries
* Help maintain content quality

## 7. Core Workflows

### Course Creation
An instructor creates a coursae and defines weekly study topics. 

### Student Enrollment
Students join a course to access course-specific study materials.

### Term Creation
Instructors define terms that need explanations or resources.

### Definition Submission
Students submit definitions or resources for assigned terms.

### Submission Review
Teaching assistants or instructors review student submissions.

### Approved Glossary 
Approved submissions become official materials for the course. 

## 8. Data Model 

### User

```bash
  id              
  name            
  email                  
  password        
  role        
  taughtCourses   
  enrolledCourses 
  submissions  
  createdAt
  updatedAt 
  ```

### Course

```bash
crn
code
secret
title
description
createdAt
updatedAt
instructor
instructorId
listing
listingId
externalURLs
location
students
terms
```

### Listing

```bash
id
code
subject
title
credits
description
prerequisites
corequisites
genEd
gradeOption
repeatable
majorRestrictions
classStanding
crossListed
createdAt
updatedAt
courses
externalURLs
```

### Term

```bash
id
word
referenceDefinition
maxSubmission
bestSubmission
bestSubmissionId
coveredOn
week
difficulty
imageRequired
course
courseCRN
```

### Submission

```bash
id
creator
creatorId
createdAt
updatedAt
definition
wasReviewed
points
term
termId
bestForTerm
```

## 9. Pages and Routes

```bash
/                             Landing Page
/about                        About Page
/auth/signin                  Login Page  
/auth/signup                  Register Page   
/student-dashboard            Student Dashboard
/instructor-dashboard         Instructor Dashboard
/courses/join                 Join a course
/courses/claim                Claim a course
/add-term                     Add new term page
/add-definition               Submit definition page
/instructor-dashboard/courses Instructor Course View
/instructor-dashboard/terms   Instructor Glossary Veiew
/student-course/[crn]         Student Course View
/student-course/[crn]/terms   Glossary Term View
```

## 10. Authentication and Authorization

Authentication is handled with NextAuth.js.

Role-based access control is used to restrict pages and actions:

```bash
Student: submit content
TA: Review content
Instructor: manage courses and approve content
```

## 11. Testing
Run all tests:

```bash
npx playwright test
```

Run a specific test file:

```bash
npx playwright test tests/example.spec.ts
```

Run tests in headed mode:

```bash
npx playwright test --headed
```

## 12. Code Quality

Run ESLint:

```bash
npm run lint
```

Automatically fix lint issues:

```bash
npm run lint -- --fix
```

## 13. Build and Production

Build the application:

```bash
npm run build
```

Start the production server:

```bash
npm start
```

## 14. Continuous Integration

GitHub Actions workflow files are stored in:

```bash
.github/workflows/
```

The CI workflow should:

```bash
install dependencies
set up the database
run Prisma migrations
run lint checks
build the app
run Playwright tests
```

## 15. Contributing

```bash
1. Create a new branch.
2. Make your changes.
3. Run tests and lint checks.
4. Commit your changes.
5. Open a pull request.
```

## 16. Future Improvements
* Real-time collaboration
* Better grading and feedback tools
* Search and filtering for study materials
* Improved dashboard design
* Notification system

