# InfinityTalk - Entity Relationship Diagram (ERD)

```mermaid
erDiagram
    USERS {
        string _id PK
        string email UK
        string username UK
        string passwordHash
        string avatar
        string role
        datetime createdAt
        datetime updatedAt
    }
    
    CHANNELS {
        string _id PK
        string name
        string type
        string description
        string createdBy FK
        datetime createdAt
    }
    
    CHANNEL_MEMBERS {
        string _id PK
        string channelId FK
        string userId FK
        datetime joinedAt
    }
    
    MESSAGES {
        string _id PK
        string channelId FK
        string userId FK
        string content
        string type
        string fileId FK
        datetime createdAt
        datetime updatedAt
    }
    
    REACTIONS {
        string _id PK
        string messageId FK
        string userId FK
        string emoji
        datetime createdAt
    }
    
    MENTIONS {
        string _id PK
        string messageId FK
        string mentionedUserId FK
        datetime createdAt
    }
    
    FILES {
        string _id PK
        string name
        string url
        string mimeType
        number size
        string uploadedBy FK
        datetime uploadedAt
    }
    
    PROJECTS {
        string _id PK
        string name
        string description
        string createdBy FK
        string status
        datetime createdAt
        datetime updatedAt
    }
    
    PROJECT_MEMBERS {
        string _id PK
        string projectId FK
        string userId FK
        string role
        datetime joinedAt
    }
    
    TASKS {
        string _id PK
        string projectId FK
        string title
        string description
        string assignedTo FK
        string status
        datetime dueDate
        datetime createdAt
        datetime updatedAt
    }
    
    CALLS {
        string _id PK
        string type
        string initiatorId FK
        string status
        datetime startedAt
        datetime endedAt
    }
    
    CALL_PARTICIPANTS {
        string _id PK
        string callId FK
        string userId FK
        datetime joinedAt
        datetime leftAt
    }
    
    NOTIFICATIONS {
        string _id PK
        string userId FK
        string type
        string message
        string relatedId
        boolean read
        datetime createdAt
    }
    
    USER_SESSIONS {
        string _id PK
        string userId FK
        string token
        datetime expiresAt
        datetime createdAt
    }
    
    USERS ||--o{ CHANNELS : creates
    USERS ||--o{ CHANNEL_MEMBERS : member_of
    CHANNELS ||--o{ CHANNEL_MEMBERS : has_members
    CHANNELS ||--o{ MESSAGES : contains
    USERS ||--o{ MESSAGES : sends
    MESSAGES ||--o{ REACTIONS : has
    MESSAGES ||--o{ MENTIONS : contains
    USERS ||--o{ MENTIONS : mentioned_in
    USERS ||--o{ FILES : uploads
    MESSAGES }o--|| FILES : references
    USERS ||--o{ PROJECTS : creates
    PROJECTS ||--o{ PROJECT_MEMBERS : has_members
    USERS ||--o{ PROJECT_MEMBERS : member_of
    PROJECTS ||--o{ TASKS : contains
    USERS ||--o{ TASKS : assigned_to
    USERS ||--o{ CALLS : initiates
    CALLS ||--o{ CALL_PARTICIPANTS : has
    USERS ||--o{ CALL_PARTICIPANTS : participates
    USERS ||--o{ NOTIFICATIONS : receives
    USERS ||--o{ USER_SESSIONS : has

```

## Collections Description

### USERS
- Stores user accounts and authentication data
- Role: ADMIN, MANAGER, MEMBER

### CHANNELS
- Communication channels (public/private)
- Type: PUBLIC, PRIVATE

### CHANNEL_MEMBERS
- Many-to-many relationship between users and channels

### MESSAGES
- Chat messages in channels
- Type: TEXT, FILE, IMAGE, AUDIO, VIDEO

### REACTIONS
- Emoji reactions on messages

### MENTIONS
- User mentions (@username) in messages

### FILES
- Uploaded files and documents

### PROJECTS
- Project management entities
- Status: ACTIVE, ARCHIVED, COMPLETED

### PROJECT_MEMBERS
- Many-to-many relationship between users and projects

### TASKS
- Tasks within projects
- Status: TODO, IN_PROGRESS, DONE

### CALLS
- Audio/video call sessions
- Type: AUDIO, VIDEO
- Status: ACTIVE, ENDED

### CALL_PARTICIPANTS
- Participants in calls

### NOTIFICATIONS
- User notifications
- Type: MESSAGE, MENTION, CALL, TASK_ASSIGNED

### USER_SESSIONS
- JWT tokens and session management
