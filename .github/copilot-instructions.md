# GitHub Copilot Code Assist Instructions – AI Generated Code Tagging 

## Purpose
These instructions define the mandatory approach for tagging **AI-generated code changes** to ensure **traceability and auditability**.

They are designed to work with GitHub Copilot's **current behavior**, where instructions are **contextual guidance** (not hard rules), and therefore must be **short, explicit, and reinforced**.

These instructions apply to:
- All IDEs (VS Code, IntelliJ, Eclipse, Visual Studio, etc.)
- All Copilot modes: Chat, Ask, Edit, Agent, Inline suggestions
- All programming languages and technologies

---

## MANDATORY AI TAGGING (PRIMARY RULE)

Whenever GitHub Copilot **adds, edits, or refactors code**, the affected code **MUST be explicitly tagged** with start and end markers.

### Required Tag Pair
Use the language-appropriate comment syntax with **both START and END tags**:

**Line comments:**

**Script comments:**

**Block comments:**

**SQL comments:**

⚠️ **Both tags are mandatory** for **all AI-generated changes**.

---

## Tag Placement Rules (Follow Exactly)

1. **New or modified function / method**  

2. **Partial modification inside existing code**  

3. **New or generated files**  

4. **Multiple AI-generated sections in one file**  
   Use **separate tag pairs** for each distinct AI-generated block.  
   Each section gets its own START and END tags.

5. **Single line changes**  
   Even single-line changes require both START and END tags.

---

## IMPORTANT USAGE NOTE (Copilot Behavior)

GitHub Copilot does **not strictly enforce repository instructions**.

To ensure correct tagging:
- These instructions **must be referenced in Edit / Agent prompts**
- File-level header comments provide the **strongest signal**
- Reviewers and CI checks are the final enforcement mechanism

### Example Prompt Reinforcement

When using Copilot Edit or Agent mode, include this reminder:

```
```

---

## Examples

### Java - New Method
```java
public Order createOrder(OrderRequest request) {
    Order order = new Order();
    order.setCustomerId(request.getCustomerId());
    order.setItems(request.getItems());
    return orderRepository.save(order);
}
```

### Kotlin - New Class
```kotlin
data class UserDto(
    val id: Long,
    val name: String,
    val email: String
)
```

### Python - Function
```python
def calculate_discount(items: List[Item]) -> Decimal:
    total = sum(item.price for item in items)
    if total > 100:
        return total * Decimal('0.1')
    return Decimal('0')
```

### SQL - Query
```sql
UPDATE orders 
SET status = 'COMPLETED', 
    updated_at = CURRENT_TIMESTAMP,
    completed_by = :userId
WHERE id = :orderId
  AND status = 'PENDING';
```

### YAML - Configuration
```yaml
apiVersion: v1
kind: Service
metadata:
  name: user-service
  namespace: production
spec:
  selector:
    app: user-api
  ports:
    - port: 8080
      targetPort: 8080
```

### TypeScript - Partial Modification
```typescript
function processPayment(payment: Payment): Result {
    validatePayment(payment);
    
    const fee = calculateProcessingFee(payment.amount);
    const total = payment.amount + fee;
    const transaction = createTransaction(payment, total);
    
    return saveTransaction(transaction);
}
```

### New File with Headers
```java
/**
 * Copyright 2026 Company Name
 * Licensed under Apache License 2.0
 */
package com.example.service;

import java.util.List;
import com.example.model.User;

public class UserService {
    private final UserRepository repository;
    
    public UserService(UserRepository repository) {
        this.repository = repository;
    }
    
    public List<User> findAllActive() {
        return repository.findByStatus("ACTIVE");
    }
}
```

### Multiple AI Sections in One File
```java
public class OrderController {
    
    @GetMapping("/orders/{id}")
    public ResponseEntity<Order> getOrder(@PathVariable Long id) {
        return orderService.findById(id)
            .map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }
    
    // Existing human-written code
    public void someExistingMethod() {
        // ...
    }
    
    @PostMapping("/orders")
    public ResponseEntity<Order> createOrder(@RequestBody OrderRequest request) {
        Order order = orderService.create(request);
        return ResponseEntity.status(HttpStatus.CREATED).body(order);
    }
}
```

---

## Summary

All AI-generated code must be wrapped with:

Use the appropriate comment syntax for your language. Both tags are mandatory.

## Prompt Reinforcement

