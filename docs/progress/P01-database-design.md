# P01 - Database Design: MySphere

**Nama Aplikasi:** MySphere  
**Deskripsi:** Aplikasi manajemen keuangan pribadi all-in-one yang mencakup pencatatan keuangan, investasi, utang, kebiasaan (habits), dan jurnal pribadi.

---

## 1. Entity Relationship Diagram

![ERD MySphere](./images/P01-erd.png)

```mermaid
erDiagram
    USERS ||--o{ ACCOUNTS : "owns"
    USERS ||--o{ CATEGORIES : "creates"
    USERS ||--o{ TRANSACTIONS : "makes"
    USERS ||--o{ BUDGETS : "sets"
    USERS ||--o{ FINANCIAL_GOALS : "plans"
    USERS ||--o{ ASSETS : "invests"
    USERS ||--o{ DEBTS : "owes"
    USERS ||--o{ HABITS : "tracks"
    USERS ||--o{ JOURNALS : "writes"
    USERS ||--o{ RECURRING_TRANSACTIONS : "schedules"

    ACCOUNTS ||--o{ TRANSACTIONS : "used_in"
    ACCOUNTS ||--o{ DEBT_PAYMENTS : "paid_from"
    ACCOUNTS ||--o{ RECURRING_TRANSACTIONS : "charged_to"

    CATEGORIES ||--o{ TRANSACTIONS : "categorizes"
    CATEGORIES ||--o{ BUDGETS : "budgeted_for"
    CATEGORIES ||--o{ RECURRING_TRANSACTIONS : "categorizes"

    ASSETS ||--o{ ASSET_TRANSACTIONS : "has_history"
    DEBTS ||--o{ DEBT_PAYMENTS : "has_payments"
    HABITS ||--o{ HABIT_LOGS : "has_logs"

    USERS {
        bigint id PK
        string name
        string email UK
        string password
    }

    ACCOUNTS {
        bigint id PK
        bigint user_id FK
        string name
        decimal balance
        string type
    }

    CATEGORIES {
        bigint id PK
        bigint user_id FK
        string name
        string type
    }

    TRANSACTIONS {
        bigint id PK
        bigint user_id FK
        bigint account_id FK
        bigint category_id FK
        decimal amount
        date transaction_date
        string type
        text description
    }

    BUDGETS {
        bigint id PK
        bigint user_id FK
        bigint category_id FK
        decimal amount
        string month
    }

    FINANCIAL_GOALS {
        bigint id PK
        bigint user_id FK
        string name
        decimal target_amount
        decimal current_amount
        date target_date
    }

    ASSETS {
        bigint id PK
        bigint user_id FK
        string name
        string type
        decimal quantity
        decimal buy_price
        decimal current_price
    }

    ASSET_TRANSACTIONS {
        bigint id PK
        bigint asset_id FK
        string type
        decimal quantity
        decimal price
        date transaction_date
    }

    DEBTS {
        bigint id PK
        bigint user_id FK
        string contact_name
        string type
        decimal total_amount
        decimal remaining_amount
        date due_date
        string status
    }

    DEBT_PAYMENTS {
        bigint id PK
        bigint debt_id FK
        bigint account_id FK
        decimal amount
        date payment_date
    }

    HABITS {
        bigint id PK
        bigint user_id FK
        string name
        string frequency
        int goal_streak
    }

    HABIT_LOGS {
        bigint id PK
        bigint habit_id FK
        date date
        boolean completed
    }

    JOURNALS {
        bigint id PK
        bigint user_id FK
        string title
        text content
        string mood
        date date
    }

    RECURRING_TRANSACTIONS {
        bigint id PK
        bigint user_id FK
        bigint account_id FK
        bigint category_id FK
        string name
        string type
        decimal amount
        string frequency
        date next_due_date
    }