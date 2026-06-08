---
type: srs-erd
feature: sport-matching
updated: 2026-06-04
---

# Sport Matching — Entity Relationship Diagram

```mermaid
erDiagram
    Player {
        string player_id PK
        string name
        string email UK
        string password
        string avatar
        string role
        datetime created_at
        datetime updated_at
    }

    Sport {
        string sport_id PK
        string name
        string icon
    }

    PlayerSport {
        string player_id FK
        string sport_id FK
        string skill_level
        float rating_avg
        int matches_played
        int wins
        int losses
    }

    Partner {
        string partner_id PK
        string name
        string contact
        string address
        string kyc_status
        datetime created_at
    }

    Court {
        string court_id PK
        string partner_id FK
        string name
        string address
        float lat
        float lng
        datetime created_at
    }

    CourtSport {
        string court_id FK
        string sport_id FK
    }

    Slot {
        string slot_id PK
        string court_id FK
        date date
        time start_time
        time end_time
        decimal price
        string status
    }

    Match {
        string match_id PK
        string player1_id FK
        string player2_id FK
        string slot_id FK
        string sport_id FK
        string status
        datetime created_at
    }

    Invite {
        string invite_id PK
        string match_id FK
        string from_player_id FK
        string to_player_id FK
        string status
        datetime expires_at
        datetime created_at
    }

    Rating {
        string rating_id PK
        string match_id FK
        string rater_id FK
        string ratee_id FK
        int score
        string comment
        datetime created_at
    }

    Wallet {
        string wallet_id PK
        string player_id FK
        decimal balance
    }

    WalletTransaction {
        string tx_id PK
        string wallet_id FK
        decimal amount
        string type
        string reference
        datetime created_at
    }

    Player ||--o{ PlayerSport : "chơi nhiều môn"
    Sport ||--o{ PlayerSport : "có nhiều player"
    Player ||--o{ Match : "tham gia (player1)"
    Player ||--o{ Match : "tham gia (player2)"
    Match ||--|| Slot : "diễn ra tại"
    Match ||--|| Invite : "có 1 invite"
    Match ||--o{ Rating : "nhận đánh giá"
    Player ||--o{ Rating : "đánh giá"
    Partner ||--o{ Court : "sở hữu nhiều sân"
    Court ||--o{ CourtSport : "hỗ trợ nhiều môn"
    Sport ||--o{ CourtSport : "được chơi tại nhiều sân"
    Court ||--o{ Slot : "có nhiều slot"
    Player ||--o| Wallet : "có 1 ví"
    Wallet ||--o{ WalletTransaction : "có nhiều giao dịch"
    Match }o--|| Sport : "thuộc 1 môn"
```
