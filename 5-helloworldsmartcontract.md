# hello.cpp

- General Structure

```
#include <iostream>

using namespace std;

int main(){
	cout << "hello world" << endl;
}
```


```
#include <eosiolib/eosio.hpp>
#include <eosiolib/print.hpp>

class hello : public eosio::contract {
  public:
      using contract::contract;

      [[eosio::action]]
      void hi( account_name user ) {
         print( "Hello, ", name{user} );
      }
}
```

# Generate hello.wast

```
eosio-cpp -o hello.wast hello.cpp --abigen
```

# Create account for this smartcontract

```
cleos create account eosio hello YOUR_PUBLIC_KEY -p hello@active
```

# Deploy this smartcontract to the production

```
cleos set contract CONTRACTS_DIR/hello --abi hello.abi -p hello@active
```

# Push an action

```
cleos push action hello hi '["bob"]' -p bob@active
```

# Updating a smart contract

- new hello.cpp

```
#include <eosiolib/eosio.hpp>
#include <eosiolib/print.hpp>

class hello : public eosio::contract {
  public:
      using contract::contract;
      void hi( account_name user ) {
      require_auth( user );
      print( "Hello, ", name{user} );
      }
}
```

- Recompile this contract

```
eosio-cpp -o hello.wast hello.cpp --abigen
```

- Update it

```
cleos set contract hello../hello -p hello@active
```

- Rerun with in-correct user?

```
cleos push action hello hi '["bob"]' -p alice@active
```
- Rerun with correct user?

```
cleos push action hello hi '["alice"]' -p alice@active
```
