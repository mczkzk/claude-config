# Date Management in Documentation

When creating or updating documentation, **ALWAYS** use the correct current date to prevent confusion and maintain accurate records.

## **Date Format Standard**
- **Format**: `YYYY-MM-DD` (ISO 8601)
- **Examples**: `2025-06-27`, `2025-12-31`

## **How to Get Current Date**
```bash
# Current date in correct format
date +%Y-%m-%d

# Verify current date matches your documentation
echo "Today's date: $(date +%Y-%m-%d)"

# File naming examples
echo "$(date +%Y-%m-%d)-feature-name.md"
echo "$(date +%Y-%m-%d)-meeting-notes.md"
echo "$(date +%Y-%m-%d)-bug-report.md"
```

## **Date Verification Checklist**
Before committing documentation:
- [ ] Check that all dates match the actual work date
- [ ] Verify file naming uses correct date format
- [ ] Ensure timeline consistency across related documents
- [ ] Cross-reference with git commit dates if needed

## **Common Date Mistakes to Avoid**
- ❌ Using yesterday's date in today's work
- ❌ Copying old template dates without updating
- ❌ Inconsistent date formats (MM/DD/YYYY vs YYYY-MM-DD)
- ❌ Missing dates in critical issue documentation

**Quick File Creation**:
```bash
# Create file with current date
touch "$(date +%Y-%m-%d)-your-task-name.md"
```