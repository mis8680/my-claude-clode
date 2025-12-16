---
description: Generate comprehensive test suite
argument-hint: [test-type]
---

Generate tests for the code above.

Test type: $1 (or comprehensive if not specified)

Include:

## Unit Tests
- Test individual functions/methods
- Test edge cases and boundary conditions
- Test error handling

## Integration Tests (if applicable)
- Test component interactions
- Test API endpoints
- Test database operations

## Test Structure
```
describe('what we are testing', () => {
  it('should handle expected behavior', () => {
    // Arrange: Set up test data
    // Act: Execute the code
    // Assert: Verify results
  });

  it('should handle error cases', () => {
    // Test failure scenarios
  });

  it('should handle edge cases', () => {
    // Test boundaries
  });
});
```

Follow project testing conventions and use existing test utilities.
