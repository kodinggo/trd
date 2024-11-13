# TRD: Online Publishing Platform (V1)

## Background

We would like to build the Online Publishing Platform like Medium, where there are several key features, such as: \
- Register &amp; Login
- Profile
- Story Management
- Story Portal
- Write Comment
- Notification

#### Register &amp; Login

Users can read stories without login, but when they want to write stories, share ideas or write comments, they must register or login.

#### Profile

After users have logged in, they can access profile page and edit their profiles.

#### Story Management 

The registered users (member) can share their ideas by creating story in Story Management. They can write new story, edit story, delete story etc.

#### Story Portal

All stories written by members will be shown in story portal. Visitors can search by keyword, filter by categories, read the story detail etc.

#### Write Comment

The registered users can write comment to all stories.

#### Notification

The registered users (member) can get notifications if there is a comment on their stories.

## System Design

#### Architecture Diagram

![medium-arch-diagram](https://github.com/user-attachments/assets/c31f69b1-0c87-4218-ace3-78e044278709)

#### ERD

![erd](https://github.com/user-attachments/assets/68ea97af-8ee0-4e51-b4d6-99f7cb3fc99b)


#### Flow Diagram

![flow](https://github.com/user-attachments/assets/d7116d19-c379-412b-93b4-244ae45f33ca)

## API Contract

#### Story Service

- [GET] /v1/stories
  ```
  Query Params:
  - category_ids=a,b,c
  - search=keyword
  - sort_by=<field>:<type> e.g. date:asc, az:desc
  - cursor=xxxxxx

  HTTP Status:
  200 (OK)
  
  Header Response:
  X-Cursor: xxxxxx
  
  Body Response:
  {
    "status": "success",
    "data": [
      {
        "id": 1,
        "title": "A Journey into Coding",
        "content": "This is a story about coding adventures.",
        "thumbnail_url": "https://example.com/thumbnail1.jpg",
        "category": {
          "id": 1,
          "name": "Technology"
        },
        "author": {
          "id": 1,
          "fullname": "John Doe",
          "sort_bio": "Developer",
          "gender": "male",
          "picture_url": "https://example.com/profile1.jpg",
          "username": "johndoe",
          "email": "johndoe@example.com"
        },
        "created_at": "2024-01-03T00:00:00Z",
        "updated_at": "2024-01-04T00:00:00Z"
      }
    ]
  }
  ```
- [GET] /v1/stories/{id}
  ```
  HTTP Status:
  200 (OK)
  
  Body Response:
  {
    "status": "success",
    "data": {
        "id": 1,
        "title": "A Journey into Coding",
        "content": "This is a story about coding adventures.",
        "thumbnail_url": "https://example.com/thumbnail1.jpg",
        "category": {
          "id": 1,
          "name": "Technology"
        },
        "author": {
          "id": 1,
          "fullname": "John Doe",
          "sort_bio": "Developer",
          "gender": "male",
          "picture_url": "https://example.com/profile1.jpg",
          "username": "johndoe",
          "email": "johndoe@example.com"
        },
        "comments": [
          {
            "id": 1,
            "comment": "Great story!",
            "author": {
              "id": 1,
              "fullname": "John Doe",
              "sort_bio": "Developer",
              "gender": "male",
              "picture_url": "https://example.com/profile1.jpg",
              "username": "johndoe",
              "email": "johndoe@example.com"
            },
            "created_at": "2024-01-06T00:00:00Z",
            "updated_at": "2024-01-07T00:00:00Z"
          }
        ],
        "created_at": "2024-01-03T00:00:00Z",
        "updated_at": "2024-01-04T00:00:00Z"
    }
  }
  ```
- [POST] /v1/stories
  ```
  HTTP Status:
  201 (Created)

  Body Request:
  {
        "title": "A Journey into Coding",
        "content": "This is a story about coding adventures.",
        "thumbnail_url": "https://example.com/thumbnail1.jpg",
        "category_id": 1,
        "author_id": 2
  }
  Body Response:
  {
    "status": "success",
    "data": {
        "id": 1,
        "title": "A Journey into Coding",
        "content": "This is a story about coding adventures.",
        "thumbnail_url": "https://example.com/thumbnail1.jpg",
        "category": {
          "id": 1,
          "name": "Technology"
        },
        "author": {
          "id": 1,
          "fullname": "John Doe",
          "sort_bio": "Developer",
          "gender": "male",
          "picture_url": "https://example.com/profile1.jpg",
          "username": "johndoe",
          "email": "johndoe@example.com"
        },
        "comments": [],
        "created_at": "2024-01-03T00:00:00Z",
        "updated_at": "2024-01-04T00:00:00Z"
    }
  }
  ```
- [PUT] /v1/stories/{id}
  ```
  HTTP Status:
  200 (OK)

  Body Request:
  {
        "title": "A Journey into Coding",
        "content": "This is a story about coding adventures.",
        "thumbnail_url": "https://example.com/thumbnail1.jpg",
        "category_id": 1,
        "author_id": 2
  }
  Body Response:
  {
    "status": "success",
    "data": {
        "id": 1,
        "title": "A Journey into Coding",
        "content": "This is a story about coding adventures.",
        "thumbnail_url": "https://example.com/thumbnail1.jpg",
        "category": {
          "id": 1,
          "name": "Technology"
        },
        "author": {
          "id": 1,
          "fullname": "John Doe",
          "sort_bio": "Developer",
          "gender": "male",
          "picture_url": "https://example.com/profile1.jpg",
          "username": "johndoe",
          "email": "johndoe@example.com"
        },
        "comments": [
          {
            "id": 1,
            "comment": "Great story!",
            "author": {
              "id": 1,
              "fullname": "John Doe",
              "sort_bio": "Developer",
              "gender": "male",
              "picture_url": "https://example.com/profile1.jpg",
              "username": "johndoe",
              "email": "johndoe@example.com"
            },
            "created_at": "2024-01-06T00:00:00Z",
            "updated_at": "2024-01-07T00:00:00Z"
          }
        ],
        "created_at": "2024-01-03T00:00:00Z",
        "updated_at": "2024-01-04T00:00:00Z"
    }
  }
  ```
- [DELETE] /v1/stories/{id}
  ```
  HTTP Status:
  204 (NoContent)
  ```

#### Comment Service

- [POST] /v1/comments
- [PUT] /v1/comments/{id}
- [DELETE] /v1/comments/{id}

#### Account Service

- [POST] /v1/auth/login

  ```
  Request Body
  {
    "email": "johndoe@gmail.com",
    "password": "secret123"
  }
  Response Body
  {
    access_token: jwttoken
  }
  ```

- [POST] /v1/auth/register

  ```
  Request Body:
  {
    "username": "johndoe",
    "email": "johndoe@gmail.com",
    "password": "secret123"
  }
  Response Body:
  {
    access_token: jwttoken
  }
  ```

- [PUT] /v1/accounts/{id}

#### Notification Service

- [GET] /v1/notifications
