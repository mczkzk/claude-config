# Database Design Guidelines

**Universal principles for database design and migration management across all projects and technologies.**

---

## 🎯 Core Philosophy

### The Golden Rule
**"Investigate First, Implement Second"** - Never make database changes without understanding the existing schema, data relationships, and domain requirements.

---

## 🔍 Investigation Techniques

### 1. **Schema Exploration**
```bash
# Technology-agnostic commands (adapt to your DB)
# PostgreSQL: \d table_name
# MySQL: DESCRIBE table_name  
# SQLite: .schema table_name
# MongoDB: db.collection.findOne()

# Sample existing data to understand patterns
# PostgreSQL: SELECT * FROM table_name LIMIT 5;
# MongoDB: db.collection.find().limit(5);
```

### 2. **Database Analysis**
```sql
-- Find existing patterns
SELECT column_name, data_type, is_nullable 
FROM information_schema.columns 
WHERE table_name = 'existing_similar_table';

-- Sample data for understanding
SELECT * FROM existing_table LIMIT 10;

-- Check relationships
SELECT * FROM information_schema.key_column_usage 
WHERE table_name = 'target_table';
```

### 3. **Runtime Data Validation**
```javascript
// Language-agnostic approach
console.log('INVESTIGATION: Actual data structure', actualObject);
// Log in development, remove before production
```

### 4. **Prototype Validation**
```javascript
// Create minimal test to verify assumptions
async function investigateDataStructure() {
  const data = await externalAPI.getData();
  console.log('PROTOTYPE: External API structure', data);
  // Verify assumptions before building schema
}
```

---

## 🚨 Common Anti-Patterns to Avoid

### 1. **Copy-Paste Pattern Blindness**
❌ **Wrong**: "Feature X uses this pattern, so Feature Y should too"
✅ **Right**: "Feature Y has similar needs to Feature X, but with these key differences..."

### 2. **Assumption-Driven Design** 
❌ **Wrong**: "The API probably returns data in format X"
✅ **Right**: "Let me log the actual API response to confirm the format"

### 3. **Single-Use Design**
❌ **Wrong**: Design for exactly the current use case
✅ **Right**: Design for current needs + reasonable future extension

### 4. **Documentation Trust Without Verification**
❌ **Wrong**: "The docs say it returns a string, so it must be a string"
✅ **Right**: "The docs say string, but let me verify with actual runtime data"

---

## 🛠️ Migration Management

### Development Phase
```bash
# Create experimental migrations freely
# Test with real data
# Iterate quickly
# Document what works and what doesn't
```

### Pre-Production Cleanup
```bash
# Remove experimental/temporary migrations
# Consolidate related changes into single migration
# Ensure migrations are idempotent
# Test migration + rollback sequence
```

### Production Deployment
```bash
# Backup before migration
# Apply migrations during low-traffic windows
# Monitor for performance impacts
# Have rollback plan ready
```

---

## 📐 Schema Design Principles

### 1. **Clarity Over Cleverness**
- Use descriptive names for tables and columns
- Prefer explicit relationships over implicit ones
- Document complex business rules in comments

### 2. **Consistency Within Domain**
- Follow existing naming conventions
- Use similar data types for similar concepts
- Maintain consistent relationship patterns

### 3. **Data Integrity**
- Use appropriate constraints (NOT NULL, UNIQUE, CHECK)
- Implement foreign key relationships where applicable
- Consider domain-specific validation rules

### 4. **Performance Considerations**
- Index frequently queried columns
- Consider query patterns when designing schema
- Balance normalization vs query performance
- Plan for data growth

---

## 💡 Investigation Framework

### Key Questions to Answer
- **Purpose**: What is the purpose of each existing column?
- **Types**: What data types and constraints are used?
- **Relationships**: Are there existing relationships/foreign keys?
- **Indexes**: What indexes exist and why?
- **Volume**: What is the current data volume and growth pattern?
- **Similar Features**: How do existing similar features handle data?
- **Unique Requirements**: What makes this feature different?
- **Business Rules**: What constraints does the domain impose?
- **Future Extensibility**: What changes might be needed later?
- **Performance Impact**: How will this affect query performance?

### Red Flags That Require Investigation
- "This should work like Feature X"
- "The API probably returns..."
- "We can change this later if needed"
- "It's just a simple table addition"
- "The migration is straightforward"

### Green Lights for Implementation
- ✅ Existing schema is well understood
- ✅ External data structures are verified
- ✅ Domain requirements are clearly defined
- ✅ Migration path is tested
- ✅ Rollback strategy is confirmed

---

## 🎯 Success Indicators

### Technical Success
- New schema follows existing project conventions
- All migrations are reversible
- Performance requirements are met
- Data integrity is maintained
- External integrations work as expected

### Process Success
- Investigation was thorough and documented
- Assumptions were validated with real data
- Changes were implemented incrementally
- User feedback was incorporated early
- Rollback plan was tested

### Future-Proofing Success
- Schema can accommodate reasonable future requirements
- External dependency changes won't break the design
- Code is maintainable and well-documented
- Performance will scale with expected data growth

---

**Remember**: Time spent in investigation saves multiples of that time in fixing design mistakes later.