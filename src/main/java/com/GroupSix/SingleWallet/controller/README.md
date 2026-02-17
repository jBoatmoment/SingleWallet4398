# Controller Layer

This folder contains REST API controllers that handle HTTP requests.

## Purpose
Controllers are responsible for:
- Receiving HTTP requests
- Validating request data (basic validation)
- Calling appropriate service methods
- Returning HTTP responses

## Naming Convention
- `{Entity}Controller.java` (e.g., `WalletController.java`, `TransactionController.java`)

## Example Structure
```java
@RestController
@RequestMapping("/api/wallets")
public class WalletController {
    
    private final WalletService walletService;
    
    @Autowired
    public WalletController(WalletService walletService) {
        this.walletService = walletService;
    }
    
    @GetMapping
    public ResponseEntity<List<WalletDTO>> getAllWallets() {
        // Call service and return response
    }
    
    @PostMapping
    public ResponseEntity<WalletDTO> createWallet(@RequestBody WalletDTO walletDTO) {
        // Call service and return response
    }
}
```

## Best Practices
- Keep controllers thin - delegate logic to services
- Use DTOs for request/response, not entities
- Use proper HTTP status codes
- Add @Valid for request body validation
- Document with Swagger annotations
