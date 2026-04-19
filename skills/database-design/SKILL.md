---
name: database-design
---

# Database Design Workflow (Viktor Forge)

## Context
Schema design and optimization.

## Logic Steps
1. **Relation Mapping**: Define 1:1, 1:N, and N:N relationships.
2. **Schema Definition**: Write the Prisma/SQL schema with proper constraints (Unique, Not Null).
3. **Indexing Strategy**: Add indexes on fields frequently used in WHERE or JOIN clauses.
4. **Migration Path**: Draft the migration script (e.g., `npx prisma migrate dev`).
5. **Security Audit**: Ensure no sensitive data is stored in plain text (e.g., hash passwords).

## Output
Database schema or migration files.
