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
## What I learned so far
- That I didn't didn't know what HTTP codes should be returned
- There can be many variation of JWT authentication
- One of JWT benefits is that you can store extra information in the token
- If need a functionality in frontend, it's most certainly already done and published by someone else
- Commonly you can make page more responsive by remove the CSS
- Using non-standard ports can make the deployment more difficult or even impossible
- Proxy server can be useful, when you have multiple apps, but only 1 port
- Even if the app works perfectly locally, it may not work at all in production
## Tech stack
- Nginx proxy
- .NET7
- React
- MySql
- RabbitMQ
- Docker
## Current progress
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
## Build instructions
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
![image](https://github.com/Nadegamra/online-learning-platform/assets/63640402/ba476c33-6149-4b2d-80b0-ada0868d860a)

## API reference
- [Authentication microservice](https://github.com/Nadegamra/microservices-authentication/blob/master/APIReference.md)
- [Course Management microservice](https://github.com/Nadegamra/microservices-course_management/blob/master/docs/APIReference.md)
- [Course Content Management microservice](https://github.com/Nadegamra/microservices-course_content_management/blob/master/docs/APIReference.md)
## Frontend Design
- [Wireframes with implementations](https://github.com/Nadegamra/STPP/blob/master/FrontendDesign.md)
