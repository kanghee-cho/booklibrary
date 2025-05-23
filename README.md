# HAPinUS Book Library

## Description
diagram: EDR
```mermaid
erDiagram
    authors {
        SERIAL author_id PK "작가 고유 ID"
        VARCHAR(255) name "작가 이름"
        TEXT bio "작가 약력"
        INT birth_year "출생 연도"
        INT death_year "사망 연도"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    publishers {
        SERIAL publisher_id PK "출판사 고유 ID"
        VARCHAR(255) name UK "출판사 이름"
        TEXT description "출판사 설명"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    categories {
        SERIAL category_id PK "카테고리 고유 ID"
        VARCHAR(50) name UK "카테고리 이름"
        INT parent_id FK "부모 카테고리 ID"
        TEXT description "카테고리 설명"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    tags {
        SERIAL tag_id PK "태그 고유 ID"
        VARCHAR(50) name UK "태그 이름"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    series {
        SERIAL series_id PK "시리즈 고유 ID"
        VARCHAR(255) name UK "시리즈 이름"
        TEXT description "시리즈 설명"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    books {
        SERIAL book_id PK "책 고유 ID"
        VARCHAR(255) title "책 제목"
        VARCHAR(255) subtitle "부제"
        TEXT description "책 설명"
        VARCHAR(20) isbn UK "국제 표준 도서 번호 (ISBN)"
        INT publisher_id FK "출판사 ID"
        DATE published_date "출판일"
        INT page_count "페이지 수"
        VARCHAR(10) language "언어 (ISO 639-1)"
        VARCHAR(255) cover_image_url "표지 이미지 URL"
        INT series_id FK "시리즈 ID"
        INT series_order "시리즈 내 순서"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    books_authors {
        INT book_id PK,FK "책 ID"
        INT author_id PK,FK "작가 ID"
        VARCHAR(50) role "작가 역할"
    }

    books_categories {
        INT book_id PK,FK "책 ID"
        INT category_id PK,FK "카테고리 ID"
    }

    books_tags {
        INT book_id PK,FK "책 ID"
        INT tag_id PK,FK "태그 ID"
    }

    book_inventory {
        SERIAL inventory_id PK "실제 책 인스턴스 고유 ID"
        INT book_id FK "참조하는 책 ID"
        DATE acquisition_date "책 획득일"
        VARCHAR(50) condition "책 상태"
        VARCHAR(100) location "책 보관 위치"
        VARCHAR(20) status "현재 상태"
        TEXT notes "특이사항"
        TIMESTAMP created_at "생성 일시"
        TIMESTAMP updated_at "최종 수정 일시"
    }

    publishers ||--o{ books : "출판"
    series ||--o{ books : "포함"
    books ||--|{ books_authors : "참여"
    authors ||--o{ books_authors : "저술/번역"
    books ||--o{ book_inventory : "재고"
    books ||--o{ books_categories : "분류"
    categories ||--o{ books_categories : "분류"
    categories }o--o{ categories : "부모-자식"
    books ||--o{ books_tags : "태그 부여"
    tags ||--o{ books_tags : "사용"
```