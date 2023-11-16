# Online Learning Platform
An example full-stack web app for creating and participating in online courses
## Functional Requirements
  - Unregistered user:
    - [x] View public courses and their contents
    - [x] Create a new account
  - Registered user:
    - [x] Login
    - [x] Logout
    - [x] Manage personal info:
      - [x] Username
      - [x] Email
      - [x] Password
    - [x] Queue account for deletion
  - Registered educator:
    - [x] Create and manage courses, specify:
      -  [x] Description
      -  [x] Preview image
      -  [x] Pricing info
      -  [x] Course length
      -  [x] Scheduling info
      -  [x] Gained and prerequisite skills
      -  [x] Supported languages and subtitles
      -  [x] Course visibility
    -  [x] Course sections
    -  [x] Text content
    -  [ ] Video content
    -  [ ] Downloadable files
    -  [ ] File submissions
    -  [ ] Quizes
      -  [ ] Multiple-choice
      -  [ ] Open questions
      -  [ ] Drag & drop
      -  [ ] Coding questions 
  - Registered learner:
    - [ ] Join courses
    - [ ] Access course content
    - [ ] Submit course feedback
    - [ ] Report inappropriate content
  - Administrator:
    - [x] Manage list of languages
    - [x] Manage list of skills
    - [ ] View hidden content
    - [ ] Review inappropriate content reports
    - [ ] Block inappropriate content
    - [ ] Block users       
## Tech stack
- Nginx proxy
- .NET7
- React
- MySql
- RabbitMQ
- Docker
## Current platform status
| Functionality                  | API           | [Frontend]     |
| ------------------------------ |:-------------:| :-------------:|
| [Authentication]               | ✅            | ✅             |
| [Course Management]            | ✅            | ✅             |
| [Course Content Management]    | ⏳            | ⏳             |
| Course Participation           | ❌            | ❌             |
| Test Taking                    | ❌            | ❌             |

[Authentication]: https://github.com/Nadegamra/microservices-authentication
[Course Management]: https://github.com/Nadegamra/microservices-course_management
[Frontend]: https://github.com/Nadegamra/olp-frontend-spa
[Course Content Management]: https://github.com/Nadegamra/microservices-course_content_management
## Launch instructions
### General requirements
- Having docker installed on the device
### Backend
#### Requirements
- Having an email (for sending Authentication service emails)
- Having a Google Drive API Service Account (for storing course images)
#### Instructions (Dev)
- Create auth_dev.env file inside `./Backend` directory. It should contain these environment variables:
  - Smtp__EmailAddress (Email address from which to send account confirmation emails, etc.)
  - Smtp__EmailPass (If you are using gmail, you should generate an App Password, but this could differ according to email provider)
  - Smtp__TestEmail (Used for testing. Email to which all mail is redirected, leave empty to turn off this functionality)
- Get a Google Drive API Service Account json key, rename it to `key.json` and place inside the `./Backend/Services/CourseManagement/` directory
- Uncomment localhost ConnectionStrings and comment out sqlstore ones in `./Backend/Services/Authentication`, `./Backend/Services/CourseManagement`, `./Backend/Services/CourseContentManagement` (might fix this later)
- Execute `dotnet ef database update` in `./Backend/Services/Authentication`, `./Backend/Services/CourseManagement`, `./Backend/Services/CourseContentManagement`
- Execute `docker-compose -f docker-compose.yml -f docker-compose.dev.yml up` from `./Backend` directory
#### Instructions (Prod)
- Dev steps except for the last 3
- Replace Database__ConnectionString within each microservice appsettings.Production.json file
- Execute `docker-compose -f docker-compose.yml -f docker-compose.prod.yml up` from `./Backend` directory
### Frontend
#### Instructions (Dev)
- Execute `docker-compose -f docker.compose.yml up` from `./Frontend` directory
#### Instructions (Prod)
- Replace .env.prod file VITE_BACKEND_URI with either http://localhost if run locally or with deployed backend url
- Execute `docker-compose -f docker.compose.yml up` from `./Frontend` directory
## System architecture
![image](https://github.com/Nadegamra/STPP/assets/63640402/1efc7c64-92c9-4bfb-94b9-5722ae6edee0)

## API reference
- [Authentication microservice](https://github.com/Nadegamra/microservices-authentication/blob/master/APIReference.md)
- [Course Management microservice](https://github.com/Nadegamra/microservices-course_management/blob/master/docs/APIReference.md)
- [Course Content Management microservice](https://github.com/Nadegamra/microservices-course_content_management/blob/master/docs/APIReference.md)
