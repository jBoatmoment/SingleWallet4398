# Model / Entity Layer

This folder contains JPA entity classes that represent database tables.

## Purpose
Entities are responsible for:
- Defining database table structure
- Defining relationships between tables
- Mapping Java objects to database rows

## Naming Convention
- `{Entity}.java` (e.g., `Wallet.java`, `Transaction.java`, `User.java`)

## Example Structure
```java
@Entity
@Table(name = "wallets")
public class Wallet {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false)
    private String accountNumber;
    
    @Column(nullable = false)
    private BigDecimal balance;
    
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    private User user;
    
    @OneToMany(mappedBy = "wallet", cascade = CascadeType.ALL)
    private List<Transaction> transactions = new ArrayList<>();
    
    @CreatedDate
    private LocalDateTime createdAt;
    
    @LastModifiedDate
    private LocalDateTime updatedAt;
    
    // Constructors, getters, setters
}
```

## Best Practices
- Use @Entity and @Table annotations
- Define proper relationships (@OneToMany, @ManyToOne, etc.)
- Use appropriate fetch types (LAZY vs EAGER)
- Add validation annotations (@NotNull, @Size, etc.)
- Include audit fields (createdAt, updatedAt)
- Consider using Lombok for boilerplate code
