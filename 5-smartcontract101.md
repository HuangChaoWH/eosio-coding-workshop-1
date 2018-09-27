# general.cpp

- General Structure

```
#include <iostream>

using namespace std;

int main(){
	cout << "hello world" << endl;
}
```


# Generalconstructs.cpp
- General programming constructs

```
#include <iostream>

using namespace std;

struct ForLoopControl{
	int numberOfIterations;
	bool isGreaterThanTen;
};


bool parameterizedForLoop(int forLoopLength) {
	for(int i = 0; i < forLoopLength; i++ ){
		if(forLoopLength >= 10){
			return true;
		}
	}
	return false;
}


bool parameterizedForLoop(ForLoopControl fControl) {
	for(int i = 0; i < fControl.numberOfIterations; i++ ){
	}
	return fControl.isGreaterThanTen;
}


int main(){
	ForLoopControl fControl;
	fControl.numberOfIterations = 100;
	fControl.isGreaterThanTen = true; 
	//cout << parameterizedForLoop(11) << endl;
	cout << parameterizedForLoop(fControl) << endl;
}
```

# hello.cpp (EOSIO smart contract crashcourse)

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


