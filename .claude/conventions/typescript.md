# TypeScript Coding Conventions

## 1. Type Annotations
Always use explicit type annotations for function parameters, return values, and class properties. Avoid using `any` type unless absolutely necessary.

```typescript
// Good
function calculateTotal(price: number, quantity: number): number {
  return price * quantity;
}

// Bad
function calculateTotal(price, quantity) {
  return price * quantity;
}
```

## 2. Interface vs Type Alias
Use `interface` for object shapes and `type` for unions, intersections, and primitive aliases.

```typescript
// Good
interface User {
  id: string;
  name: string;
  email: string;
}

type Status = 'active' | 'inactive' | 'pending';

// Bad
type User = {
  id: string;
  name: string;
  email: string;
};
```

## 3. Naming Conventions
- Use PascalCase for types, interfaces, enums, and classes
- Use camelCase for variables, functions, and methods
- Use UPPER_SNAKE_CASE for constants

```typescript
// Good
interface UserProfile { }
class UserService { }
const MAX_RETRY_COUNT = 3;
function getUserById(id: string) { }

// Bad
interface user_profile { }
const maxRetryCount = 3;
function GetUserById(id: string) { }
```

## 4. Async/Await over Promises
Prefer async/await syntax over raw promises for better readability and error handling.

```typescript
// Good
async function fetchUserData(id: string): Promise<User> {
  try {
    const response = await api.get(`/users/${id}`);
    return response.data;
  } catch (error) {
    throw new Error(`Failed to fetch user: ${error.message}`);
  }
}

// Bad
function fetchUserData(id: string): Promise<User> {
  return api.get(`/users/${id}`)
    .then(response => response.data)
    .catch(error => {
      throw new Error(`Failed to fetch user: ${error.message}`);
    });
}
```

## 5. Strict Mode and ESLint
Always enable TypeScript strict mode in `tsconfig.json` and use ESLint with TypeScript plugin for consistent code quality.

```json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true
  }
}
```