Создание очереди для генерации id например:
```SQL
CREATE SEQUENCE IF NOT EXISTS token_sequence START WITH 1 INCREMENT BY 1;
```

Создание таблицы со связью:
```SQL
CREATE TABLE IF NOT EXISTS token  
(  
    token_id    BIGINT PRIMARY KEY,  
    token       VARCHAR(255),  
    expired     BOOLEAN NOT NULL,  
    revoked     BOOLEAN NOT NULL,  
    CONSTRAINT fk_token_employee FOREIGN KEY (employee_id) REFERENCES employee (employee_id) ON DELETE CASCADE,  
)
```

