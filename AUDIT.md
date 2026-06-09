## Verification Table

| Bug                 | Before                                     | After                                       | Verification Method                             |
| ------------------- | ------------------------------------------ | ------------------------------------------- | ----------------------------------------------- |
| SQL Injection       | Search payload returned unintended records | Search treated as literal string            | GET /api/products?search=shirt' OR '1'='1       |
| Plaintext Passwords | Password stored directly in database       | Password stored as bcrypt hash ($2b$12$...) | SELECT password FROM users                      |
| Double Discount     | Same coupon could be reused                | Second request returns 400 error            | POST /api/cart/checkout twice with same coupon  |
| Stock Decrement     | Stock remained unchanged after purchase    | Stock reduced by purchased quantity         | Compare product stock before and after checkout |
| N+1 Order History   | Multiple database queries per order        | Single JOIN query retrieves all data        | Profiling middleware output                     |
