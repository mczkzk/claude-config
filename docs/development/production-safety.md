# Production Safety Protocol

**Critical safety measures to prevent production environment incidents**

---

## 🚨 Production Environment Detection

### Mandatory Environment Check
**ALWAYS verify environment before ANY potentially destructive operation**

```bash
# Required check before dangerous operations
echo "⚠️ ENVIRONMENT CHECK ⚠️"
echo "Checking environment indicators..."
```

### Claude Code Detection Rules
1. **Read environment configuration files immediately** when destructive operations are requested:
   - `.env`, `.env.production`, `.env.local`
   - `config/`, `settings/` directories
   - Cloud service configuration files

2. **Analyze environment indicators**:
   - **Database URLs**: Production domains (`.amazonaws.com`, `.neon.tech`, `.herokuapp.com`, `.vercel.app`, etc.)
   - **Environment variables**: `NODE_ENV=production`, `RAILS_ENV=production`, `ENV=prod`
   - **Branch/deployment context**: `main`, `master`, `production`, `prod` branches
   - **Domain patterns**: Live websites, production APIs

3. **Flag production environment** if ANY indicator suggests production use

---

## ⛔ Forbidden Operations in Production

### Dangerous Operation Patterns (Technology-Agnostic)
```bash
# Keywords that indicate destructive operations - NEVER execute in production
*reset*     # ❌ Any reset command (db:reset, schema:reset, etc.)
*drop*      # ❌ Drop operations (drop database, drop table, etc.)
*clear*     # ❌ Clear operations (clear data, truncate, etc.)
*delete*    # ❌ Bulk delete operations
*truncate*  # ❌ Table truncation
```

### High-Risk Operation Patterns Requiring Confirmation
```bash
# Patterns requiring explicit user confirmation in production
*seed*      # ⚠️ Data seeding operations
*migrate*   # ⚠️ Schema migration operations
*deploy*    # ⚠️ Deployment commands
*publish*   # ⚠️ Publishing operations
```

---

## 🛑 Claude Code Safety Protocol

### Pre-Operation Checklist
When database operations are requested:

1. **IMMEDIATE .env FILE CHECK**
   ```
   ✅ Read project .env file
   ✅ Parse DATABASE_URL
   ✅ Detect production environment
   ```

2. **PRODUCTION ENVIRONMENT RESPONSE**
   ```
   🚨 PRODUCTION ENVIRONMENT DETECTED 🚨
   
   DATABASE_URL indicates production database: [URL]
   
   Requested operation: [OPERATION]
   Risk level: [HIGH/CRITICAL]
   
   ⛔ STOPPING EXECUTION ⛔
   
   Please confirm:
   1. Is this operation intended for production?
   2. Have you taken necessary backups?
   3. Do you understand the risk of data loss?
   
   Type 'CONFIRM PRODUCTION OPERATION' to proceed.
   ```

3. **MANDATORY USER CONFIRMATION**
   - Never proceed with dangerous operations without explicit user confirmation
   - Require specific confirmation text for high-risk operations
   - Provide backup and rollback recommendations

### Destructive Operation Decision Tree
```
Potentially Destructive Operation Requested
│
├─ Read environment configuration files
│
├─ Analyze environment indicators
│
├─ Is Production Environment?
│  │
│  ├─ YES → 🚨 STOP & REQUEST CONFIRMATION
│  │      │
│  │      ├─ Contains Dangerous Keywords? → ⛔ REFUSE + ALTERNATIVES
│  │      └─ High Risk Operation? → ⚠️ DETAILED WARNING + CONFIRMATION
│  │
│  └─ NO → ✅ Proceed with standard caution
```

---

## 🔒 Risk Classification

### CRITICAL RISK (Refuse Execution)
- `db:reset`, `db:drop`, `db:clear`
- Any operation that deletes production data
- Schema destructive operations

### HIGH RISK (Detailed Warning + Double Confirmation)
- `db:seed` in production
- `db:migrate` without backup confirmation
- Bulk data operations

### MEDIUM RISK (Standard Warning + Confirmation)
- Schema additive migrations
- Index creation/deletion
- Performance optimization queries

### LOW RISK (Environment Notice Only)
- Read-only queries
- Database inspection commands
- Non-destructive operations

---

## 📋 Required Questions for Production Operations

### For ANY Production Database Operation:
1. **Environment Confirmation**
   - "Are you sure this is the correct database environment?"
   - "Have you verified this is not a development/testing mistake?"

2. **Backup Verification**
   - "When was the last backup taken?"
   - "Can you confirm backup integrity before proceeding?"

3. **Impact Assessment**
   - "What is the expected impact of this operation?"
   - "How many records/tables will be affected?"

4. **Rollback Planning**
   - "What is your rollback plan if something goes wrong?"
   - "Do you have the necessary restore procedures ready?"

5. **Business Justification**
   - "Why is this production operation necessary?"
   - "Has this been approved by relevant stakeholders?"

---

## 🎯 Success Criteria

### Before Operation
- ✅ Production environment correctly identified
- ✅ User has been warned about risks
- ✅ Explicit confirmation obtained
- ✅ Backup status verified
- ✅ Rollback plan confirmed

### During Operation
- ✅ Progress monitored
- ✅ Unexpected errors immediately reported
- ✅ Operation can be halted if needed

### After Operation
- ✅ Results verified
- ✅ Data integrity confirmed
- ✅ Performance impact assessed
- ✅ Incident documentation updated

---

## 📖 Emergency Response

### If Production Incident Occurs
1. **IMMEDIATE RESPONSE**
   ```bash
   # Stop all operations
   # Assess damage scope
   # Initiate backup restore if necessary
   ```

2. **INCIDENT DOCUMENTATION**
   ```markdown
   ## Incident Report - [DATE]
   
   **What happened**: [Description]
   **Root cause**: [Analysis]
   **Impact**: [Scope of damage]
   **Recovery actions**: [Steps taken]
   **Prevention measures**: [Future safeguards]
   ```

3. **LEARNING INTEGRATION**
   - Update this safety protocol
   - Enhance Claude Code detection rules
   - Implement additional safeguards

---

**Remember**: Production safety is NEVER optional. When in doubt, ALWAYS err on the side of caution.