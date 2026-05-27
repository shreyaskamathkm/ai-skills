# EXAMPLES.md — Rule Application Guide (Python)

This document provides real-world code examples demonstrating the core principles of the 12-Rule framework. Each example shows what AI agents commonly do wrong and how to fix it to ensure surgical, simple, and goal-driven results.

---

## 1. Think Before Coding (Rules 1 & 8)

### Example 1: Hidden Assumptions
**User Request:** "Add a feature to export user data"

**❌ What AI Agents Do (Wrong Assumptions)**
```python
def export_users(format='json'):
    """Export all users to a file."""
    users = User.query.all()
    
    if format == 'json':
        with open('users.json', 'w') as f:
            json.dump([u.to_dict() for u in users], f)
    elif format == 'csv':
        with open('users.csv', 'w') as f:
            writer = csv.DictWriter(f, fieldnames=['id', 'email', 'name'])
            writer.writeheader()
            writer.writerows([u.to_dict() for u in users])
    
    return f"Exported {len(users)} users"
```
**Problems:**
- Assumed it should export ALL users (privacy/pagination issues).
- Assumed file location without asking.
- Assumed fieldnames without checking the actual data structure.

**✅ What Should Happen (Surface Assumptions)**
> Before implementing, I need to clarify:
> 1. **Scope**: Export all users or a filtered subset?
> 2. **Format**: Should this be a file download, a background job with email, or an API response?
> 3. **Fields**: Which user fields are required? (Are any sensitive?)
> 4. **Volume**: How many users typically? (Determines if we need streaming).
>
> **Simplest approach**: Add a paginated API endpoint returning JSON. Would you like me to proceed with that or do you need a file-based export?

---

## 2. Simplicity First (Rules 2 & 5)

### Example 1: Over-abstraction
**User Request:** "Add a function to calculate discount"

**❌ What AI Agents Do (Over-engineered)**
```python
from abc import ABC, abstractmethod

class DiscountStrategy(ABC):
    @abstractmethod
    def calculate(self, amount: float) -> float:
        pass

class PercentageDiscount(DiscountStrategy):
    def __init__(self, percentage: float):
        self.percentage = percentage
    def calculate(self, amount: float) -> float:
        return amount * (self.percentage / 100)

# Requires 30+ lines of setup for a simple calculation...
```

**✅ What Should Happen (Simple)**
```python
def calculate_discount(amount: float, percent: float) -> float:
    """Calculate discount amount. percent should be 0-100."""
    return amount * (percent / 100)
```
**Insight**: Only add strategy patterns when you *actually* have multiple conflicting discount types. Refactor later if the requirement emerges.

---

## 3. Surgical Changes (Rule 3 & 11)

### Example 1: Drive-by Refactoring
**User Request:** "Fix the bug where empty emails crash the validator"

**❌ What AI Agents Do (Too Much)**
```diff
  def validate_user(user_data):
-     # Check email format
-     if not user_data.get('email'):
+     """Validate user data."""
+     email = user_data.get('email', '').strip()
+     
+     # Validate email
+     if not email:
          raise ValueError("Email required")
-     
-     # Basic email validation
-     if '@' not in user_data['email']:
+     if '@' not in email or '.' not in email.split('@')[1]:
          raise ValueError("Invalid email")
      
-     # Check username
-     if not user_data.get('username'):
+     # Validate username
+     username = user_data.get('username', '').strip()
+     if not username:
          raise ValueError("Username required")
```
**Problems**: "Improved" validation and added username checks that weren't requested.

**✅ What Should Happen (Surgical)**
```diff
  def validate_user(user_data):
      # Check email format
-     if not user_data.get('email'):
+     email = user_data.get('email', '')
+     if not email or not email.strip():
          raise ValueError("Email required")
      
      # Basic email validation
-     if '@' not in user_data['email']:
+     if '@' not in email:
          raise ValueError("Invalid email")
```

---

## 4. Goal-Driven Execution (Rules 4, 9 & 12)

### Example 1: Test-First Verification
**User Request:** "The sorting breaks when there are duplicate scores"

**❌ What AI Agents Do (Fix Without Reproducing)**
```python
# Immediately changes sort logic without confirming the bug
def sort_scores(scores):
    return sorted(scores, key=lambda x: (-x['score'], x['name']))
```

**✅ What Should Happen (Reproduce First)**
```python
# 1. Write a test that reproduces the issue
def test_sort_with_duplicate_scores():
    scores = [{'name': 'Alice', 'score': 100}, {'name': 'Bob', 'score': 100}]
    result = sort_scores(scores)
    # The bug: order is non-deterministic for duplicates
    assert result[0]['name'] == 'Alice'

# 2. Fix with stable sort
def sort_scores(scores):
    return sorted(scores, key=lambda x: (-x['score'], x['name']))

# 3. Verify: Test passes consistently
```

### Example 2: Fail Loud (Rule 12)
**User Request:** "Add a database migration for the new users table"

**❌ What AI Agents Do (Silencing Failures)**
```python
try:
    db.execute("CREATE TABLE users (id INT, email TEXT)")
except Exception:
    # Silently passing or just logging a warning
    print("Table might already exist, skipping...")
```

**✅ What Should Happen (Fail Loudly)**
```python
# If the migration fails, the deployment MUST stop.
# No silent catches. The error should be explicit.
def migrate():
    try:
        db.execute("CREATE TABLE users (id INT, email TEXT)")
    except Exception as e:
        logger.critical(f"Migration Failed: {str(e)}")
        raise SystemExit(1) # Stop execution immediately
```

---

## 5. Use the Model Only for Judgment Calls (Rule 5)

### Example 1: Deterministic Logic
**User Request:** "Write a function to retry an API call 3 times"

**❌ What AI Agents Do (AI-generated complex retry logic)**
AI writes a complex decorator with jitter, exponential backoff, and multiple exception handlers that might be buggy or non-idiomatic.

**✅ What Should Happen (Use Libraries/Deterministic Code)**
"Instead of writing a custom retry loop, we should use the `tenacity` library which is already in your `requirements.txt`. It is deterministic and handles edge cases safely."
```python
from tenacity import retry, stop_after_attempt

@retry(stop=stop_after_attempt(3))
def call_api():
    # ... logic ...
```

---

## 6. Token Budgets & Context (Rule 6)

### Example 1: Context Bloat
**User Request:** "Read all 50 files in the `src/` directory to find where we use `User`"

**❌ What AI Agents Do (Reading Everything)**
AI attempts to `read_file` on every single file in parallel, hitting the token limit and causing the model to lose track of previous instructions.

**✅ What Should Happen (Surgical Search)**
AI uses `grep_search` to find the specific files and lines where `User` is used, reading only the relevant snippets.
```bash
grep -rn "class User" src/
```

---

## 7. Surface Conflicts (Rule 7)

### Example 1: Architectural Drift
**User Request:** "Add a new endpoint for user profile updates"

**❌ What AI Agents Do (Averaging Styles)**
AI sees some endpoints using `Flask-Restful` and others using plain `Flask` decorators. It writes a hybrid that doesn't strictly follow either.

**✅ What Should Happen (Identify and Choose)**
"I notice the codebase is transitioning from `Flask-Restful` to plain `Flask` decorators (as seen in recent `auth_routes.py`). I will implement this new endpoint using the new decorator-based pattern and document this choice in `MEMORY.md` to ensure future consistency."

---

## Anti-Patterns Summary

| Principle | Anti-Pattern | Fix |
| :--- | :--- | :--- |
| **Think Before Coding** | Silently assumes file format or scope | List assumptions explicitly; ask before acting |
| **Simplicity First** | Speculative "just-in-case" features | Solve today's problem; refactor for tomorrow's |
| **Surgical Changes** | Reformats quotes or adds type hints while fixing bugs | Match existing style; touch only necessary lines |
| **Goal-Driven** | "I'll review and improve the code" | "Write failing test → fix → verify suite is green" |

## Key Insight
**Good code solves today's problem simply, not tomorrow's problem prematurely.** Over-abstraction and drive-by refactoring increase complexity and testing surface area without providing immediate value.
