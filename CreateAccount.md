# What is account?

- An account is a collection of authorizations, stored on the blockchain, and used to identify a sender/recipient. It has a flexible authorization structure that enables it to be owned either by an individual or group of individuals depending on how permissions have been configured. An account is required to send or receive a valid transaction to the blockchain. This tutorial series uses two "user" accounts, bob and alice, as well as the default eosio account for configuration. Additionally accounts are made for various contracts throughout this tutorial series.

# Create

```
cleos create account eosio bob YOUR_PUBLIC_KEY 
cleos create account eosio alice YOUR_PUBLIC_KEY
```

# Check

```
cleos wallet list
```

