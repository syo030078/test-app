erDiagram

  USERS {
    bigint id
    string name
    string email
    int role
  }

  MUSICIAN_PROFILES {
    bigint id
    bigint user_id
  }

  TRACKS {
    bigint id
    bigint musician_profile_id
  }

  JOBS {
    bigint id
    bigint client_id
  }

  PROPOSALS {
    bigint id
    bigint job_id
    bigint musician_id
  }

  CONTRACTS {
    bigint id
    bigint job_id
    bigint client_id
    bigint musician_id
    bigint proposal_id
  }

  MILESTONES {
    bigint id
    bigint contract_id
  }

  TRANSACTIONS {
    bigint id
    bigint contract_id
    bigint milestone_id
    bigint payer_id
    bigint payee_id
  }

  REVIEWS {
    bigint id
    bigint contract_id
    bigint reviewer_id
    bigint reviewee_id
  }

  MESSAGES {
    bigint id
    bigint contract_id
    bigint sender_id
  }

  %% リレーション定義

  USERS ||--o| MUSICIAN_PROFILES : "1 - 0..1 (musician)"
  MUSICIAN_PROFILES ||--o{ TRACKS : "1 - N"

  USERS ||--o{ JOBS : "client 1 - N jobs"

  JOBS ||--o{ PROPOSALS : "1 - N"
  USERS ||--o{ PROPOSALS : "musician 1 - N proposals"

  JOBS ||--o{ CONTRACTS : "1 - N(実質1)"
  USERS ||--o{ CONTRACTS : "client"
  USERS ||--o{ CONTRACTS : "musician"
  PROPOSALS ||--|| CONTRACTS : "1 - 0..1 from proposal"

  CONTRACTS ||--o{ MILESTONES : "1 - N"
  CONTRACTS ||--o{ TRANSACTIONS : "1 - N"
  MILESTONES ||--o{ TRANSACTIONS : "1 - N"

  USERS ||--o{ TRANSACTIONS : "payer"
  USERS ||--o{ TRANSACTIONS : "payee"

  CONTRACTS ||--o{ REVIEWS : "1 - N"
  USERS ||--o{ REVIEWS : "reviewer"
  USERS ||--o{ REVIEWS : "reviewee"

  CONTRACTS ||--o{ MESSAGES : "1 - N"
  USERS ||--o{ MESSAGES : "sender"
