# Project Coding Convention

## Rule: No Direct Dictionary Literals in Business Logic

### Overview
This project follows a strict convention where **all data structures representing domain entities must be created through dedicated factory functions or classes, not inline dictionary literals**.

### Rationale
- **Consistency**: Ensures all entity objects are created uniformly across the codebase
- **Maintainability**: Centralizes object creation logic, making changes easier
- **Validation**: Factory functions can include validation logic
- **Type Safety**: Provides a single point for documenting object structure
- **Refactoring**: Makes it easier to migrate to proper classes in the future

### Rule Details

#### ❌ INCORRECT - Direct Dictionary Literals
```python
def add_task():
    new_task = {
        'id': len(tasks) + 1,
        'text': task_text,
        'completed': False
    }
    tasks.append(new_task)
```

#### ✅ CORRECT - Factory Function
```python
def create_task(task_id, text, completed=False):
    """Factory function for creating task objects"""
    return {
        'id': task_id,
        'text': text,
        'completed': completed
    }

def add_task():
    new_task = create_task(len(tasks) + 1, task_text)
    tasks.append(new_task)
```

### Scope
This rule applies to:
- ✅ Business logic functions
- ✅ Route handlers
- ✅ Service layer functions
- ✅ Data manipulation operations

This rule does NOT apply to:
- ❌ Configuration dictionaries
- ❌ Simple key-value mappings for JSON responses
- ❌ Test fixture data (unless representing domain entities)

### Enforcement
All code reviews must verify compliance with this convention. Any direct dictionary literals representing domain entities should be flagged and refactored to use factory functions.

### Version
- **Created**: 2026-01-30
- **Status**: Active
- **Applies to**: All Python modules containing business logic