# Behavioral Control Guidelines

## Investigation Keywords
When receiving instructions containing words like "調べて" (investigate), "探して" (search), "見つけて" (find), or similar investigative terms:
- **Only perform investigation/research** - do not implement code changes
- You may write temporary code for investigation purposes, but **clean it up afterwards**
- Do not start implementing features or writing production code
- Focus strictly on gathering information and providing findings

## Wait for Implementation Signal
- **Do not start implementing code changes during conversation** unless explicitly asked
- Investigation, analysis, and discussion are encouraged
- Only begin implementation when user provides clear signals like:
  - "実装して" (implement it)
  - "やって" (do it)  
  - "始めて" (start)
  - "作って" (create)
  - Direct implementation requests

## Question Mode
- When query starts with "q.", provide answer only
- Do not perform additional actions without permission
- Ask for permission if response requires file operations or implementation