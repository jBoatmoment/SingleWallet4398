# Repository Layer

This folder contains database access interfaces using Spring Data JPA.

## Purpose
Repositories are responsible for:
- Database CRUD operations
- Custom query methods
- Data access logic

## Naming Convention
- `{Entity}Repository.java` (e.g., `WalletRepository.java`, `TransactionRepository.java`)

## Example Structure
```java
@Repository
public interface WalletRepository extends JpaRepository<Wallet, Long> {
    
    // Spring Data JPA will implement these automatically
    List<Wallet> findByUserId(Long userId);
    
    Optional<Wallet> findByAccountNumber(String accountNumber);
    
    // Custom query
    @Query("SELECT w FROM Wallet w WHERE w.balance > :minBalance")
    List<Wallet> findWalletsAboveBalance(@Param("minBalance") BigDecimal minBalance);
}
```

## Best Practices
- Extend JpaRepository<Entity, ID>
- Use method naming conventions for automatic queries
- Use @Query for complex queries
- Add @Repository annotation
- Keep repositories focused on data access only
