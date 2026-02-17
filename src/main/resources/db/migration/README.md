# Database Migrations

This folder contains database migration scripts for version control of your database schema.

## Purpose
Migration scripts are used to:
- Create and modify database tables
- Maintain database schema version control
- Ensure consistent database state across environments
- Support rollback capabilities

## Tool Options
Choose between **Flyway** (simpler) or **Liquibase** (more features).

## For Flyway

### Naming Convention
`V{version}__{description}.sql`

Examples:
- `V1__create_users_table.sql`
- `V2__create_wallets_table.sql`
- `V3__add_balance_column_to_wallets.sql`

### Example Migration
```sql
-- V1__create_wallets_table.sql
CREATE TABLE wallets (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    account_number VARCHAR(50) NOT NULL UNIQUE,
    balance DECIMAL(19, 2) NOT NULL DEFAULT 0.00,
    user_id BIGINT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE INDEX idx_wallet_user_id ON wallets(user_id);
```

### Add to pom.xml
```xml
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
</dependency>
```

### Configure in application.properties
```properties
spring.flyway.enabled=true
spring.flyway.locations=classpath:db/migration
```

## For Liquibase

### Naming Convention
- `db.changelog-master.xml` (main file)
- Individual changesets in separate files

### Example Changeset
```xml
<changeSet id="1" author="team">
    <createTable tableName="wallets">
        <column name="id" type="BIGINT" autoIncrement="true">
            <constraints primaryKey="true"/>
        </column>
        <column name="account_number" type="VARCHAR(50)">
            <constraints nullable="false" unique="true"/>
        </column>
        <column name="balance" type="DECIMAL(19,2)" defaultValue="0.00">
            <constraints nullable="false"/>
        </column>
    </createTable>
</changeSet>
```

## Best Practices
- Never modify existing migrations
- Test migrations locally before committing
- Keep migrations small and focused
- Add rollback scripts when possible
- Document complex changes with comments
- Use consistent naming and ordering
