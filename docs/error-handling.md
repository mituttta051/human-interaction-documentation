# Error Handling

## Common Failure Scenarios

### 400 Bad Request
Input is unclear, vague, or lacks structure.

### 429 Too Many Requests
Excessive or repetitive demands, especially under suboptimal conditions.

### 503 Service Unavailable
System is temporarily unable to respond (e.g., OFFLINE or extreme TIRED state).

## Critical Anti-Patterns

- unnecessary pressure
- requests early in the morning before activation
- task requests during weekends

## Recovery Recommendations

- reformulate request clearly
- delay request to a more appropriate time
- reduce pressure and urgency