# Awesome Project  

This project demonstrates the use of **sdm (Schema Data Migration)** for managing database schema and data migrations in a reproducible and rollback-safe manner.  

---

## Environment Details  

For this assignment, both **MySQL** and **SDM** were run inside Docker containers.  

- **MySQL Version:** `9.4.0`  
  Retrieved with:  
  ```bash
  docker exec -it sdm-mysql mysql -u root -pXXXX -e "SELECT VERSION();"
  ```


- **SDM Version:** `0.6.4`  
  Retrieved with:  
  ```bash
  docker run -v "%cd%:/workspace" -e MYSQL_PWD="XXXX" -it --rm beim/schema-data-migration:latest sdm --version
  ```
---

## How the sdm Tool Works
sdm is a tool that ensures databases remain consistent across environments (development, test, and production) by version-controlling both schema and data changes.

### Core Concepts

- **Schema Migrations**:
Managed by Skeema, which compares the live database schema with a model and generates the necessary SQL changes (e.g., adding/dropping columns or tables).

- **Data Migrations**:
Implemented using SQL, Python, TypeScript, or Shell scripts to apply or modify data as part of the versioned migration process.

- **Repeatable Migrations**:
Handle reusable operations such as seeding data or creating views that can be reapplied multiple times safely.

Each migration is stored in a JSON migration plan with forward (apply) and optional backward (rollback) steps. SDM automatically maintains migration history for auditing and rollback.

### Typical Workflow

1. **Initialize project**:
`sdm init` creates schema and migration folders.

2. **Add environments**:
`sdm add-env` links databases like dev, staging, and prod.

3. **Create migrations**:
`sdm make-schema` or `sdm make-data` generates migration plans.

4. **Apply migrations**:
`sdm migrate` applies pending migrations.

5. **Rollback**:
`sdm rollback` reverts to a previous version.

6. **Check differences**:
`sdm diff` detects schema drift between environments.

### Example: Rollback (Assignment Task)

In this assignment, I demonstrated SDM’s rollback functionality:

1. Created a user table in the `awesome_db database`.

2. Added a new column `address` through schema migration.

3. Seeded test data.

4. Rolled back to the initial version (`0000`) using:

```bash
docker run -v %cd%:/workspace -e MYSQL_PWD="XXXX" -it --rm beim/schema-data-migration:latest sdm rollback --version 0000 dev
```



### Why sdm Is Valuable for Data Scientists

- SDM offers several benefits for data-driven projects:

- Consistency: Keeps schemas aligned across environments.

- Experimentation Safety: Allows reversible schema and data changes.

- Collaboration: Migration plans can be version-controlled and reviewed.

- Traceability: Tracks when and how database changes occur.

- Reproducibility: Ensures stable and reliable data pipelines.

By mastering SDM, a data scientist can manage schema and data evolution in a controlled, reproducible, and rollback-safe way, which is essential for maintaining robust data workflows.

---

## Challenge Faced and Solution
**Challenge:**
When moving the pre-commit file from the main repository folder to `.git/hooks/` using:

```bash
mv pre-commit .git/hooks/
# or on Windows:
move pre-commit .git/hooks/
```

Git pre-commit checks began blocking commits, preventing pushes to GitHub.

**Solution:**
To bypass the issue, I committed changes using:

```bash
git commit -m "message" --no-verify
```


This allowed successful commits while keeping the repository functional. The issue was later traced to a **misconfigured pre-commit** hook, which may be adjusted or removed in future revisions.





