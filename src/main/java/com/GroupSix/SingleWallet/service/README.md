# Service Layer

This folder contains business logic and service classes.

## Purpose
Services are responsible for:
- Implementing business logic
- Orchestrating repository calls
- Transaction management
- Data transformation between entities and DTOs

## Naming Convention
- `{Entity}Service.java` (interface)
- `{Entity}ServiceImpl.java` (implementation)

## Example Structure
```java
public interface WalletService {
    WalletDTO createWallet(WalletDTO walletDTO);
    WalletDTO getWalletById(Long id);
    List<WalletDTO> getAllWallets();
    WalletDTO updateWallet(Long id, WalletDTO walletDTO);
    void deleteWallet(Long id);
}

@Service
public class WalletServiceImpl implements WalletService {
    
    private final WalletRepository walletRepository;
    
    @Autowired
    public WalletServiceImpl(WalletRepository walletRepository) {
        this.walletRepository = walletRepository;
    }
    
    @Override
    @Transactional
    public WalletDTO createWallet(WalletDTO walletDTO) {
        // Business logic here
    }
}
```

## Best Practices
- Use interfaces for services
- Add @Transactional where needed
- Handle business validation here
- Convert between entities and DTOs
- Throw custom exceptions for error cases
