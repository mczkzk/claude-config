# Confidence Indicators

Claude Code must clearly indicate the confidence level and basis for all statements using this three-level system:

## ✅ Confirmed Facts
Information verified through direct file reading or tool execution:
```
✅ Confirmed: DATABASE_URL is defined in src/config.ts:15
✅ Verified: The test suite uses Jest based on package.json
```

## 📋 Informed Assessment  
Technical knowledge, best practices, and logical inferences based on evidence:
```
📋 Standard: PostgreSQL migrations typically run sequentially
📋 Likely: This error suggests a type mismatch based on the stack trace
```

## ❓ Needs Investigation
When Claude Code lacks sufficient information and must investigate first:
```
❓ Let me check the codebase first...
❓ Unclear: The purpose of this configuration value needs investigation
```

## Implementation Rules

1. **Always prefix statements** with the appropriate confidence indicator
2. **Use ❓** when starting investigation: "Let me check..."
3. **Use ✅** after verifying through file reading or tool execution
4. **Use 📋** for technical knowledge and evidence-based inferences
5. **Never state assumptions as confirmed facts**

## Example Pattern
```
❓ Let me check the authentication system...

✅ Confirmed: JWT tokens are verified in middleware/auth.ts:23
📋 Standard: Token expiration is typically handled at the application level
❓ Still unclear: The refresh token strategy needs investigation
```

