# HAPinUS Book Library

## Description
diagram: EDR
```mermaid
erDiagram
    publishers {
        integer id PK
        string name
        ...
    }
    authors {
        integer id PK
        string name
        ...
    }
    series {
        integer id PK
        string name
        ...
    }
    books {
        integer book_id PK
        string ISBN
        string title
        integer publisher_id FK
        integer series_id FK
        date published_date
        ...
    }
    book_authors {
        integer book_id FK
        integer author_id FK
        string role PK(book_id, author_id)
    }
    inventory {
        integer inventory_id PK
        integer book_id FK
        date acquisition_date
        string condition
        string location
        string status
        ...
    }

    publishers ||--o{ books : ""
    authors ||--o{ book_authors : ""
    series ||--o{ books : ""
    books ||--o{ inventory : ""
```