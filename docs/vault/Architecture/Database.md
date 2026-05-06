---
tags: [architecture, database, schema, dbml, postgresql]
---

# Database

Database schema.

## Schema DBML

```dbml
Project PROJECT-TITLE {
  database_type: 'Postgres'
  note: 'Project Title placeholder'
}

Table platform [headercolor: #2ecc71] {
  platform_id BIGINT [pk, increment]
  code VARCHAR(20) [not null, unique]
  name VARCHAR(200) [not null, unique]
  description VARCHAR(500)
  active BOOLEAN [not null, default: true]
  timezone VARCHAR(100) [not null]
  currency VARCHAR(3) [not null]
  created_at TIMESTAMPTZ [not null, default: `CURRENT_TIMESTAMP`]
  updated_at TIMESTAMPTZ
  deleted_at TIMESTAMPTZ

  indexes {
    code [unique, name: 'ix_platform_code_unique']
    name [unique, name: 'ix_platform_name_unique']
  }
}
```

## Design notes

## Docs

- Syntax DBML: https://dbml.dbdiagram.io/docs