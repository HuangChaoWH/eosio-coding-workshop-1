# 1. Create Development Wallet

```
cleos wallet create --to-console
```

- Save the private key
```
Creating wallet: default
Save password to use in the future to unlock this wallet.
Without password imported keys will not be retrievable.
"PW5Kewn9L76X8Fpd....................t42S9XCw2"
```

# 2. Open the wallet
```
cleos wallet open
cleos wallet list
```
- Check the outcome
```
Wallets:
[
  "default"
]
```

# 3. Unlock wallet
```
cleos wallet unlock
cleos wallet list
```

# 4. Import keys

```
cleos wallet create_key
```

- Check the outcome
```
Created new private key with a public key of: "EOS8PEJ5FM42xLpHK...X6PymQu97KrGDJQY5Y"
```

# 5.Import the Development Key

```
cleos wallet import
```
