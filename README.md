# Архитектуралық аудит және техқарыз

## Деректер қорының архитектурасы (ER-диаграмма)

```mermaid
erDiagram

USER {
int user_id PK
string name
string email
string password
string role
}

TEST_RESULT {
int result_id PK
int user_id FK
string recommended_profession
date created_at
}

PROFESSION {
int profession_id PK
string name
string description
string skills
}

COURSE {
int course_id PK
string title
string link
}

USER ||--o{ TEST_RESULT : creates
PROFESSION ||--o{ TEST_RESULT : recommends
PROFESSION ||--o{ COURSE : contains
```

---

## Қателерді өңдеу сценарийі (Sequence диаграмма)

```mermaid
sequenceDiagram

participant User
participant Interface
participant Validator
participant Database

User->>Interface: Тест нәтижесін жібереді

Interface->>Validator: Деректерді тексеру

alt Бос немесе қате мәлімет

Validator-->>Interface: Error message

Interface-->>User: Мәліметтерді толтырыңыз

else Рұқсат жоқ

Validator->>Database: Access тексеру

Database-->>Validator: Access denied

Validator-->>Interface: Reject

else Дұрыс мәлімет

Validator->>Database: Save result

Database-->>Interface: Saved

Interface-->>User: Мамандық ұсынысы

end
```

---

# Архитектуралық аудит

## Масштабталғыштық

Егер қолданушылар саны 100 есе өссе, негізгі қиындық деректер қорындағы тест нәтижелерін іздеу жылдамдығы болады.

Шешімі:
- деректер базасын индекстеу;
- сұраныстарды оңтайландыру;
- кэш қолдану.


## Қауіпсіздік (OWASP)

1. Парольдерді ашық сақтау қаупі.

Шешімі:
- парольдерді hash арқылы сақтау.


2. API рұқсаттарының қорғалмауы.

Шешімі:
- Role Based Access Control (RBAC);
- JWT авторизация.


## Рефакторинг

Келесі Sprint:

- код құрылымын модульдерге бөлу;
- API жақсарту;
- автоматты тест жазу;
- қауіпсіздік тексерулерін қосу.


  ## User Flow (Stitch)<img width="962" height="684" alt="Снимок экрана 2026-06-04 103225" src="https://github.com/user-attachments/assets/3af6fe9c-8206-44b9-abba-a4fb27143466" />
