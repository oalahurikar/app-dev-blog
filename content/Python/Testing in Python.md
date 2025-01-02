---
#inprogress 
---

Directory Structure and Scope:


~~~
tests/
├── conftest.py          # Global fixtures
├── unit/
│   ├── conftest.py      # Unit test fixtures
│   └── test_models.py
├── integration/
│   ├── conftest.py      # Integration test fixtures
│   └── test_api.py
└── e2e/
    ├── conftest.py      # E2E test fixtures
    └── test_workflow.py
~~~

what is conftest what does it do?
> conftest.py is a special file used in pytest for sharing fixtures across multiple test files. Let me explain its key features and usage:

```python
import pytest

# Shared fixture available to all test files
@pytest.fixture
def api_client():
    """Create a test client for the API."""
    from app import create_app
    app = create_app('testing')
    with app.test_client() as client:
        yield client
```

Key Features:
- Automatically discovered by pytest
- Can be placed in different directories for different scopes
- No need to import fixtures in test files
- Can define fixture hierarchies

Key Benefits:
- Reusability across test files
- Centralized test configuration
- Clean test organization
- Reduced code duplication

5. Easy mocking and dependency injection
- Flexible scoping options
- Automatic fixture discovery
- 
Remember:
- Place common fixtures in the root conftest.py
- Use directory-specific conftest.py for specialized fixtures
- Consider fixture scope for performance
- Use clear naming conventions
- Document fixtures with docstrings