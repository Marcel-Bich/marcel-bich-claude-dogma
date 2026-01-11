# Error Handling Guide

<log_levels>
## Log Levels

| Level | When to use | Example |
|-------|-------------|---------|
| **ERROR** | Unexpected failure, needs fixing | Database connection failed |
| **WARN** | Potential problem, should check | Deprecated API used |
| **INFO** | Important events | Server started, user logged in |
| **DEBUG** | Development details | Request payload, internal state |

**Production:** ERROR + WARN + INFO
**Development:** All levels
</log_levels>

<logging_patterns>
## Good vs Bad Logging

```typescript
// BAD: No context
try {
  await saveUser(user);
} catch (error) {
  console.log('Error');  // Useless
}

// BAD: Empty catch (swallowing error)
try {
  await saveUser(user);
} catch (error) {
  // Do nothing - ERROR IS LOST!
}

// GOOD: Log with context
try {
  await saveUser(user);
} catch (error) {
  console.error('Failed to save user', {
    userId: user.id,
    email: user.email,
    error: error.message,
    stack: error.stack,
  });
  throw error; // Re-throw or handle appropriately
}
```
</logging_patterns>

<user_messages>
## User-Facing Error Messages

```typescript
// BAD: Technical message shown to user
showError('ECONNREFUSED 127.0.0.1:5432');

// GOOD: Human-readable message
showError('Unable to connect. Please try again later.');

// Pattern: Map technical errors to user messages
const userMessages = {
  'ECONNREFUSED': 'Service temporarily unavailable',
  'ETIMEDOUT': 'Request timed out. Please try again.',
  'ENOTFOUND': 'Unable to connect to server',
  'default': 'Something went wrong. Please try again.',
};

function getUserMessage(error: Error): string {
  return userMessages[error.code] ?? userMessages.default;
}
```
</user_messages>

<external_calls>
## Wrapping External Calls

**Always wrap:**
- API calls (fetch, axios)
- Database queries
- File system operations
- Third-party services

```typescript
// API call with proper error handling
async function fetchUser(id: string): Promise<User> {
  try {
    const response = await fetch(`/api/users/${id}`);

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }

    return await response.json();
  } catch (error) {
    console.error('Failed to fetch user', { id, error });
    throw new UserFetchError(`Could not load user ${id}`, { cause: error });
  }
}
```
</external_calls>

<fail_fast>
## Fail Fast Principle

```typescript
// Validate at boundaries, fail early
function processOrder(order: unknown): ProcessedOrder {
  // Validate immediately
  if (!order || typeof order !== 'object') {
    throw new ValidationError('Order must be an object');
  }

  if (!order.items?.length) {
    throw new ValidationError('Order must have items');
  }

  // Now we know order is valid - proceed with confidence
  return {
    items: order.items.map(processItem),
    total: calculateTotal(order.items),
  };
}
```

**Validate at:**
- Function entry (parameters)
- External data (API responses, user input)
- Configuration (environment variables)
</fail_fast>

<custom_errors>
## Custom Error Classes

```typescript
// Base application error
class AppError extends Error {
  constructor(
    message: string,
    public code: string,
    public statusCode: number = 500
  ) {
    super(message);
    this.name = this.constructor.name;
  }
}

// Specific errors
class ValidationError extends AppError {
  constructor(message: string) {
    super(message, 'VALIDATION_ERROR', 400);
  }
}

class NotFoundError extends AppError {
  constructor(resource: string, id: string) {
    super(`${resource} with id ${id} not found`, 'NOT_FOUND', 404);
  }
}

class UnauthorizedError extends AppError {
  constructor(message = 'Authentication required') {
    super(message, 'UNAUTHORIZED', 401);
  }
}
```
</custom_errors>

<checklist>
## Error Handling Checklist

- [ ] No empty catch blocks
- [ ] Errors logged with context
- [ ] User sees friendly message
- [ ] Technical details logged (not shown)
- [ ] External calls wrapped in try/catch
- [ ] Validation at function boundaries
- [ ] Custom errors for common cases
</checklist>
