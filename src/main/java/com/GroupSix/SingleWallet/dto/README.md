# DTO (Data Transfer Object) Layer

This folder contains DTOs used for API requests and responses.

## Purpose
DTOs are responsible for:
- Defining API contract (request/response structure)
- Hiding internal entity structure
- Data validation
- Preventing over-fetching of data

## Naming Convention
- `{Entity}DTO.java` for general purpose
- `Create{Entity}Request.java` for creation requests
- `Update{Entity}Request.java` for update requests
- `{Entity}Response.java` for specific responses

## Example Structure
```java
public class WalletDTO {
    
    private Long id;
    
    @NotBlank(message = "Account number is required")
    private String accountNumber;
    
    @NotNull(message = "Balance is required")
    @DecimalMin(value = "0.0", message = "Balance must be positive")
    private BigDecimal balance;
    
    private Long userId;
    
    private LocalDateTime createdAt;
    
    // Constructors, getters, setters
}

public class CreateWalletRequest {
    @NotBlank
    private String accountNumber;
    
    @NotNull
    private BigDecimal initialBalance;
    
    @NotNull
    private Long userId;
    
    // Getters, setters
}
```

## Best Practices
- Use validation annotations (@NotNull, @Size, @Email, etc.)
- Keep DTOs simple and focused
- Don't include entities in DTOs
- Use different DTOs for different operations
- Document fields with clear names
