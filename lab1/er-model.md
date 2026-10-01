# ER-модель онлайн-магазину

## Mermaid ER-діаграма

```mermaid
erDiagram

    USER ||--o{ ORDER : places
    CATEGORY ||--o{ PRODUCT : contains
    ORDER ||--|{ ORDER_ITEM : contains
    PRODUCT ||--o{ ORDER_ITEM : included_in
    ORDER ||--|| PAYMENT : has

    USER {
        int id PK
        string name
        string email
    }

    CATEGORY {
        int id PK
        string name
    }

    PRODUCT {
        int id PK
        string name
        decimal price
        int category_id FK
    }

    ORDER {
        int id PK
        int user_id FK
        datetime created_at
    }

    ORDER_ITEM {
        int id PK
        int order_id FK
        int product_id FK
        int quantity
        decimal unit_price
    }

    PAYMENT {
        int id PK
        int order_id FK
        decimal amount
        string status
    }
```

## Опис зв'язків

- `User 1:N Order` — один користувач може створити багато замовлень.
- `Category 1:N Product` — одна категорія може містити багато товарів.
- `Order 1:N OrderItem` — одне замовлення містить одну або більше позицій.
- `Product 1:N OrderItem` — один товар може зустрічатися в багатьох позиціях замовлень.
- `Order 1:1 Payment` — кожне замовлення має один платіж.

`OrderItem` є асоціативною сутністю між `Order` та `Product`, оскільки зв'язок має власні атрибути `quantity` та `unit_price`.