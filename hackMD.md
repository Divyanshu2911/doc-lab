# Test Plan – SecureDocs (Collaborative Document Security Platform)

## 1. Introduction

**Objective:**  
The goal of this Test Plan is to ensure the correctness, reliability, and security of the SecureDocs platform — a web-based document storage and sharing system with end-to-end encryption and access control.

**Scope:**  
This plan covers API-level, backend, and user interface testing for critical modules such as authentication, document upload/download, encryption, and access-control logic.

**Out of Scope:**  
Performance testing at scale and post-deployment monitoring are excluded from this phase.

**References:**  
- Software Requirements Specification (SRS) – v1.0  
- Design Document – v1.2  
- Security Guidelines – OWASP ASVS Level 2  

---

## 2. Test Items

| Module | Description |
|---------|--------------|
| Auth Service | Login, signup, token refresh |
| File Service | Upload, download, encryption |
| Access Control | Role/attribute-based access enforcement |
| Blockchain Audit Log | Verify on-chain write transactions |

---

## 3. Test Approach

| Level | Type | Technique | Tool / Framework |
|-------|------|------------|------------------|
| Unit | Functional | Assertions | Jest / Mocha |
| Integration | API | Contract testing | Postman / Newman |
| System | End-to-End | UI + backend | Cypress |
| Security | Static & Dynamic | OWASP ZAP, dependency scan | GitHub Dependabot, ZAP CLI |

**Environments:**
- Local container setup (Docker Compose)
- CI/CD test runner (GitHub Actions)

---

## 4. Test Cases

| ID | Title | Steps | Expected Result |
|----|--------|--------|-----------------|
| TC-001 | Valid Login | 1. POST `/auth/login` with valid creds | Returns `200 OK` with JWT token |
| TC-002 | Invalid Login | 1. Wrong password → verify 401 | Returns error `Invalid credentials` |
| TC-003 | File Upload | 1. Choose file → click Upload | File encrypted and stored |
| TC-004 | Access Policy | 1. User A (no access) requests doc | API returns `403 Forbidden` |
| TC-005 | Blockchain Log | 1. Upload doc → query transaction | Hash stored on blockchain |

---

## 5. Entry / Exit Criteria

**Entry Criteria:**
- All feature modules integrated.  
- Dev branch builds successfully in CI pipeline.  
- Test environment stable.

**Exit Criteria:**
- ≥ 95% unit tests pass.  
- No open critical bugs.  
- Security checks show no high-severity issues.

---

## 6. Schedule & Responsibilities

| Activity | Tester | Date |
|-----------|---------|------|
| Unit testing | Divyanshu | 18 Oct 2025 |
| Integration tests | Sudip | 19 Oct 2025 |
| E2E + security tests | Anand | 20 Oct 2025 |
| Final validation | All | 21 Oct 2025 |

---

## 7. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|---------|-------------|
| API schema change | High | Versioned test suites |
| Token expiry mid-test | Medium | Mock JWT for automation |
| Merge conflicts during parallel edits | Low | Clear branching & review policy |

---

## 8. Collaboration Observations (HackMD Session)

1. **Conflict #1 – Editing “Scope” simultaneously:**  
   Both contributors changed the same line (“Scope of testing”). HackMD highlighted conflicting edits in yellow. We merged the two descriptions manually and discussed consistency.

2. **Conflict #2 – Table merge issue:**  
   While one added a new row in “Test Cases,” another modified the header alignment. HackMD merged most edits but dropped one cell. We restored it from the version history.

3. **Conflict #3 – Formatting confusion:**  
   One used numbered lists while the other used bullets. We agreed on consistent Markdown syntax and re-ran markdownlint to verify style uniformity.

---

## 9. Versioning / Merging Notes

- **Platform used:** HackMD (real-time collaboration).  
- **Merge observation:** HackMD merges automatically but preserves last writer in case of conflict.  
- **Finalization:** Reviewed collaboratively, exported to `Test_Plan.md`, and pushed to GitHub branch `lab3/test-plan`.  
- **Verification:** Vale + markdownlint CI jobs passed successfully.

---

## 10. Approval

| Role | Name | Signature / Date |
|------|------|------------------|
| Author | Divyanshu Semwal | — |
| Reviewer | Sudip Dey | — |
