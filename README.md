# Backstage IDP — My Practical Learning Journey

> **Learner:** CR Hapuarachchi ([@0019-KDU](https://github.com/0019-KDU))
> **Instance:** http://24.144.83.231:3000

This is my hands-on Backstage IDP instance. The 3 folders inside this repo are my **practical study repositories** — each one built during a specific learning module.

---

## Study Material Repositories

These repos are cloned here as my practical reference and learning material:

```
backstage/
├── backstage-idp-lab/            ← Practical: Catalog + Templates + Org Data
├── express-service-template/     ← Practical: Real Express.js Service Component
├── express-service-infra-template/ ← Practical: Infrastructure Template (Terraform)
└── ... (backstage core files)
```

### 1. [backstage-idp-lab](https://github.com/0019-KDU/backstage-idp-lab)
**Course modules:** Catalog → Registering Components, Relationships, Users/Groups, API Entity, Templates

What I built inside:
- `user-guest-domain-system/entity.yaml` — Full org structure with `Domain`, `System`, `Component`, `Resource`, `Group`, `User` entities and their relationships
- `template/api-template.yaml` — Scaffolder template to create new API services
- `template/infra-template.yaml` — Scaffolder template to create app + infra repos with Terraform CI/CD

---

### 2. [express-service-template](https://github.com/0019-KDU/express-service-template)
**Course modules:** Catalog → Registering a Component, API Entity, TechDocs

What I built:
- A production-ready Express.js backend service (TypeScript, PostgreSQL, Prisma, REST API)
- `catalog-info.yaml` — Registers the service as a `Component` + `API` entity in Backstage
- `mkdocs.yml` + `docs/` — TechDocs configuration for auto-generated documentation

---

### 3. [express-service-infra-template](https://github.com/0019-KDU/express-service-infra-template)
**Course modules:** Templates → Templates with Infrastructure

What I built:
- Terraform infrastructure code (`main.tf`, `variables.tf`, `outputs.tf`)
- Kubernetes manifest (`resource.yaml`)
- Used as the **skeleton** that the `infra-template.yaml` scaffolder template deploys from

---

## What I Configured in This Backstage Instance

### PostgreSQL Database
Moved from in-memory SQLite to persistent PostgreSQL (Docker):
```bash
docker run --name postgres \
  -e POSTGRES_USER=appuser \
  -e POSTGRES_PASSWORD=<password> \
  -e POSTGRES_DB=appdb \
  -p 5432:5432 -d postgres:16.3
```
Backstage auto-created 11 plugin databases on first run.

### GitHub Authentication
- Created a GitHub OAuth App
- Configured `plugin-auth-backend-module-github-provider`
- Users sign in with their GitHub account — no Guest access

### GitHub Integration
- Added a Personal Access Token (PAT) so Backstage can read repo content
- Catalog locations registered for the study repos above

---

## How to Start

```bash
NODE_OPTIONS=--no-node-snapshot yarn start
```

| Service | URL |
|---|---|
| Frontend | http://24.144.83.231:3000 |
| Backend API | http://24.144.83.231:7007 |

---

## Learning Reference

| Module | Topic | My Practical |
|---|---|---|
| Backstage Basics | Architecture, Creating Instance | This Backstage setup |
| Catalog | Entities, Relationships, API | `backstage-idp-lab/user-guest-domain-system/` |
| Catalog | Registering a Component | `express-service-template/catalog-info.yaml` |
| Templates | Scaffolder Basics | `backstage-idp-lab/template/api-template.yaml` |
| Templates | Infrastructure Templates | `express-service-infra-template/` + `infra-template.yaml` |
| TechDocs | Docs as Code | `express-service-template/docs/` + `mkdocs.yml` |
| Production | PostgreSQL + Auth | Configured in `app-config.yaml` |
