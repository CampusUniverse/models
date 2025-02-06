``` mermaid
classDiagram
   class Role {
        STUDENT
        LECTURER
        STAFF
        ADMIN
    }

    class Part {
        ONE
        TWO
        THREE
        FOUR
        FIVE
    }

    class EventVisibility {
        PUBLIC
        DEPARTMENT[]
        FACULTY[]
        PART[]
        PRIVATE
    }

    class EventCategory {
        LECTURE
        WORKSHOP
        MEETING
        SPORTS
        CULTURAL
        EXAM
        HOLIDAY
    }

    class EventStatus {
        SCHEDULED
        ONGOING
        COMPLETED
        CANCELLED
        POSTPONED
    }

    class CheckInMethod {
        QR_CODE
        MANUAL_OVERRIDE
    }

<<enumeration>> Role
<<enumeration>> EventStatus
<<enumeration>> EventCategory
<<enumeration>> EventVisibility
<<enumeration>> Part
<<enumeration>> CheckInMethod
```

``` mermaid
erDiagram
    User {
        string id
        string matricNumber
        string email
        string name
        Role role
        Part part
        string departmentId
        DateTime createdAt
    }

    Department {
        string id
        string name
        string code
        string facultyId
    }

    Faculty {
        string id
        string name
        string acronym
        float latitude
        float longitude
    }

    Event {
        string id
        string title
        string description
        DateTime start
        DateTime end
        boolean isAllDay
        EventVisibility visibility
        string creatorId
        string organizer
        string locationId
        EventCategory category
        EventStatus status
        string qrCodeUrl
    }

    Location {
        string id
        string building
        string room
        float latitude
        float longitude
    }

    EventSubscription {
        string id
        string userId
        string eventId
        DateTime subscribedAt
    }

    EventParticipant {
        string id
        string userId
        string eventId
        DateTime joinedAt
        boolean verified
        CheckInMethod checkInMethod
    }

    QRCheckIn {
        string id
        string eventId
        string qrCode
        DateTime expiresAt
    }

    User ||--o{ Event : "creates"
    User ||--o{ EventSubscription : "subscribes to"
    EventSubscription }o--|| Event : "notifies about"
    Faculty ||--o{ Department : "contains"
    Department }o--o{ User : "has members"
    Event }o--o{ Department : "allowed departments"
    Event }o--o{ Faculty : "allowed faculties"
    Event }|--|| Location : "occurs at"
    Location ||--o{ Event : "hosts"
    Event }o--o{ EventParticipant : "has participants"
    EventParticipant }o--o{ User : "participates"
    Event }|--o{ QRCheckIn : "has QR codes"
```
