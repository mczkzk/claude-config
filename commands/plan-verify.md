---
description: Verify plan document completeness and quality
allowed-tools:
  - Read
  - Edit
  - Grep
  - Glob
  - LS
---

# Plan Verification Command

Verifies plan document completeness and quality.

## Usage

```
/plan-verify [feature-name]
# Verifies plan document completeness and quality

/plan-verify
# Verifies plan document when feature-name is contextually obvious
```

## Command Execution Steps

1. 🔍 **Find Plan Document**: 
   - If feature-name provided: Look for `plans/[feature-name].md` file
   - If no feature-name: Search `plans/` directory for `*.md` files (excluding `*-search.md` and `archive/` subdirectory) and identify from context
2. 🔎 **CRITICAL Initial State Verification**: 
   - Run `grep '\- \[ \]' "plans/[feature-name].md"` to check unchecked items
   - **EXPECTED STATE**: Should find EXACTLY the "Plan Document Verification" checklist (10 items) + any Implementation Plan tasks
   - **RESET REQUIRED**: If Plan Document Verification items are already checked → Reset ALL to `[ ]` (unchecked state)
   - **MISSING STATE**: If Plan Document Verification section missing → STOP, return error message
3. 📋 **STRICT Checkbox State Validation**:
   - Plan Document Verification section: ALL items MUST be unchecked `[ ]` (reset if needed)
   - Requirements Summary: Items should remain unchecked (for implementation phase)
   - Implementation Plan: Items should remain unchecked (for implementation phase)
   - Other sections: No checkboxes expected (templates only)
   - **Action Required**: If any Plan Document Verification items are checked `[x]`, reset them to `[ ]` before proceeding
4. 📋 **Interactive Verification**: Go through each section with user:
   - Review section completeness and quality
   - Identify missing or insufficient content
   - Guide user through improvements
5. ✅ **Section-by-Section Checklist**: Mark ONLY verification checklist items as complete
6. 🚀 **Final Status Update**: Change status to "✅ Ready for implementation"
7. 🔎 **Final Verification Command**: Run `grep '\- \[ \]' "plans/[feature-name].md"` - should return ONLY unchecked Implementation Plan tasks

## Interactive Verification Process

### 📄 Requirements Summary
- **Check**: Are requirements clear and actionable?
- **Verify**: Do checkboxes represent testable outcomes?
- **Guide**: Help refine vague requirements

### 🏗️ Architecture Impact  
- **Check**: Are affected components identified?
- **Verify**: Are integration points documented?
- **Guide**: Help identify missing dependencies

### 📁 File Changes
- **Check**: Both Modified and New files sections populated?
- **Verify**: Are file purposes clearly described?
- **Guide**: Help identify missing files based on requirements

### 🧪 Testing Strategy
- **Check**: Are TDD test cases specific with inputs/outputs?
- **Verify**: Do tests cover main functionality and edge cases?
- **Guide**: Help create missing test scenarios

### 📋 Implementation Plan
- **Check**: Is work broken into logical phases?
- **Verify**: Are tasks actionable and specific?
- **Guide**: Help break down overly large tasks

### ⚠️ Risk Assessment
- **Check**: Are technical risks identified?
- **Verify**: Are mitigation strategies practical?
- **Guide**: Help identify overlooked risks

### 📚 Reference Documentation
- **Check**: Are methodology references included?
- **Verify**: Are links to relevant docs present?
- **Guide**: Add missing documentation references

### ⌨️ Commands Reference
- **Check**: Are complex commands documented?
- **Verify**: Are command descriptions clear?
- **Guide**: Help document project-specific commands

### 📝 Implementation Notes
- **Check**: Are date-based sections set up?
- **Verify**: Is template ready for discoveries?
- **Guide**: Explain how to use during implementation

### 📖 Plan Document Operation Guide
- **Check**: Is complete operational guide included?
- **Verify**: Are all sections from template present?
- **Guide**: Add any missing guide sections

## Verification Completion

When all sections are verified:

1. **Mark Verification Complete**: Check all items in Plan Document Verification section ONLY
2. **PRESERVE Implementation Tasks**: Do NOT check Requirements Summary or Implementation Plan items (these are for implementation phase)
3. **Update Status**: Change from "⚠️ Plan verification required" to "📋 Ready for implementation"
4. **Final Checkpoint**: Run `grep '\- \[ \]' "plans/[feature-name].md"` should return:
   - Requirements Summary checkboxes (unchecked - for implementation)
   - Implementation Plan task checkboxes (unchecked - for implementation)
   - NO Plan Document Verification checkboxes (all should be checked)

## Key Principles

- **Interactive Quality Control**: Work with user to improve plan quality
- **Section-by-Section**: Systematic verification of each plan component
- **Actionable Improvements**: Don't just identify problems, help solve them
- **Quality Assurance**: Ensure plan document meets completeness standards
- **Status Management**: Clear progression from verification to ready state