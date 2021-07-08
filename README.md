# dogecoin-node-setup


 ## Setup 
The primary sources for the setup from official repository are given below :
1) https://github.com/dogecoin/dogecoin/blob/master/doc/build-osx.md
2) https://github.com/dogecoin/dogecoin/blob/master/doc/Building-Dogecoin-1.14-for-Mac.md

# Errors during setup 
Error related to berkley db version was fixed by referring to https://github.com/dogecoin/dogecoin/issues/1948 . Installed the version 5 from  https://github.com/fastcoin-project/homebrew-formulas .

Error related to 'openssl/sha.h' file not found was fixed by linking it manually and referring to https://github.com/dogecoin/dogecoin/issues/1948 .

While building dogecoin no matching function for call to 'objc_msgSend' error occurred. The issue was related to QT gui version. The solution was to change configuration and rebuild. The solution is described here https://github.com/dogecoin/dogecoin/issues/1862 .

# Starting the node on testnet 
For starting the node on testnet and printing the syncing process to console
```sh
./src/dogecoind -testnet -printtoconsole -debug
```
The command is described here https://github.com/dogecoin/dogecoin/pull/169.

# Explore basic commands  
```sh
./src/dogecoin-cli -testnet help
```

# Syncing the data 
```sh
./src/dogecoin-cli -testnet getblockchaininfo
```
OR 

```sh
curl --user dogecoinrpc:dcb436fa3db12e0e8a05c219501c66c1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getblockchaininfo", "params": [] }' -H 'content-type: text/plain;' http://127.0.0.1:44555/
```

# Create account in wallet 
```sh
./src/dogecoin-cli -testnet getaccountaddress "minahil's account"
```
It returns the address of the account. The output address in this case given below:
```sh
nWLC4XbD684F8ztr8os45tb4QN5vM2yovX
```

OR

```sh
curl --user dogecoinrpc:dcb436fa3db12e0e8a05c219501c66c1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaccountaddress", "params": ["minahil"] }' -H 'content-type: text/plain;' http://127.0.0.1:44555/
```
It returns the address of the created account in the result key-value pair.
```sh
{
    "result": "nji5zEavjzKRrJdCJmSHTiYFAESujMY3yA",
    "error": null,
    "id": "curltest"
}
```


# Get balance 
```sh
./src/dogecoin-cli -testnet getbalance "Minahil's Wallet"
``` 
For newly created the balance  will be ```0.00000000```. In this case  the  wallet was charged using testnet faucet so the output was ``` 100.00000000```

OR

```sh
curl --user dogecoinrpc:dcb436fa3db12e0e8a05c219501c66c1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getbalance", "params": ["minahil"] }' -H 'content-type: text/plain;' http://127.0.0.1:44555/
```
It returns the balance of the required account in the result key-value pair.
```sh
{
    "result": 288.01000000,
    "error": null,
    "id": "curltest"
}
```

# Get  address 
```sh
./src/dogecoin-cli -testnet getaccountaddress "Minahil's Wallet" 
```
The address returned  for receiving  funds is ```nWLC4XbD684F8ztr8os45tb4QN5vM2yovX```

OR 

```sh
curl --user dogecoinrpc:dcb436fa3db12e0e8a05c219501c66c1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "getaddressesbyaccount", "params": ["minahil"] }' -H 'content-type: text/plain;' http://127.0.0.1:44555/
```
It returns the addresses of the required account in the result key-value pair.
```sh
{
    "result": [
        "neTTsGfaz7Go7bob6ouYtb4n3RRX3eJiTW",
        "nji5zEavjzKRrJdCJmSHTiYFAESujMY3yA"
    ],
    "error": null,
    "id": "curltest"
}
```

# Get public key  
```sh
./src/dogecoin-cli -testnet validateaddress nWLC4XbD684F8ztr8os45tb4QN5vM2yovX
```
In output the pubkey attribute specifies your public key
```sh
{
  "isvalid": true,
  "address": "nWLC4XbD684F8ztr8os45tb4QN5vM2yovX",
  "scriptPubKey": "76a9141775146bb600bd58088988b4a457be2ec614141688ac",
  "ismine": true,
  "iswatchonly": false,
  "isscript": false,
  "pubkey": "03497fe2b6f51ba3b287d66c2dc221c9bff5109b3fceea35b0da868181f90004c1",
  "iscompressed": true,
  "account": "minahil's account",
  "timestamp": 1625505794,
  "hdkeypath": "m/0'/0'/8'",
  "hdmasterkeyid": "a036af087dcb8a73b741dcce63943c996cb68b72"
}
```

OR 

```sh
curl --user dogecoinrpc:dcb436fa3db12e0e8a05c219501c66c1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "validateaddress", "params": ["nWLC4XbD684F8ztr8os45tb4QN5vM2yovX"] }' -H 'content-type: text/plain;' http://127.0.0.1:44555/
```
It returns the publickey in the pubkey key-value pair.
```sh
{
    "result": {
        "isvalid": true,
        "address": "nWLC4XbD684F8ztr8os45tb4QN5vM2yovX",
        "scriptPubKey": "76a9141775146bb600bd58088988b4a457be2ec614141688ac",
        "ismine": true,
        "iswatchonly": false,
        "isscript": false,
        "pubkey": "03497fe2b6f51ba3b287d66c2dc221c9bff5109b3fceea35b0da868181f90004c1",
        "iscompressed": true,
        "account": "minahil's account",
        "timestamp": 1625505794,
        "hdkeypath": "m/0'/0'/8'",
        "hdmasterkeyid": "a036af087dcb8a73b741dcce63943c996cb68b72"
    },
    "error": null,
    "id": "curltest"
}
```

# Get private key 
```sh
./src/dogecoin-cli -testnet dumpprivkey nWLC4XbD684F8ztr8os45tb4QN5vM2yovX
```
The private key associated with given address is  provided as output. In this case private key is ```ckHwUGwTYcDUZ2zVi9HgorBHCUoqD1xUBGYvULrboQ6b4Vr9MqR2```

OR 

```sh
curl --user dogecoinrpc:dcb436fa3db12e0e8a05c219501c66c1 --data-binary '{"jsonrpc": "1.0", "id":"curltest", "method": "dumpprivkey", "params": ["nWLC4XbD684F8ztr8os45tb4QN5vM2yovX"] }' -H 'content-type: text/plain;' http://127.0.0.1:44555/
```
The private key associated with given address is  provided as output in result key-value pair.
```sh 
{
    "result": "ckHwUGwTYcDUZ2zVi9HgorBHCUoqD1xUBGYvULrboQ6b4Vr9MqR2",
    "error": null,
    "id": "curltest"
}
```

# Create and Send Raw Transaction
In the first step a raw  transaction is created  by following command 
```sh
./src/dogecoin-cli -testnet createrawtransaction "[{\"txid\":\"c06810602157c9465472a4fbb4151870f2f3fada8102633ff5915b4912e7023c\",\"vout\":0}]" "{\"neTTsGfaz7Go7bob6ouYtb4n3RRX3eJiTW\":88.01}"
```
It returns the hex of hex string of the transaction like ```01000000013c02e712495b91f53f630281dafaf3f2701815b4fba4725446c95721601068c00000000000ffffffff01409a940c020000001976a9147096311efc9f506355118400fc3e1d83c7c1caba88ac00000000```


In the second step the  hex of transaction is signed with command given below 
```sh
./src/dogecoin-cli -testnet signrawtransaction 01000000013c02e712495b91f53f630281dafaf3f2701815b4fba4725446c95721601068c00000000000ffffffff01409a940c020000001976a9147096311efc9f506355118400fc3e1d83c7c1caba88ac00000000
```

It returns an object specifying the status 
```sh
{
  "hex": "01000000013c02e712495b91f53f630281dafaf3f2701815b4fba4725446c95721601068c0000000006a47304402205d7a7f0c0f6c39a781aede0cc2cdfdd2a85fd5067b56c25538f122b1beb10c33022025dc77b83e9ae31bb8070eb7d3e7ae175c9525dc0b7041562a4e5f0fa643dc39012102213a7a9a3a97a241b17e7b2ca0026b9c0b48e0bfe553696746fb1ac4650183c6ffffffff01409a940c020000001976a9147096311efc9f506355118400fc3e1d83c7c1caba88ac00000000",
  "complete": true
}
```
In the  final  step the raw  transaction is  sent 
```sh
./src/dogecoin-cli -testnet sendrawtransaction 01000000013c02e712495b91f53f630281dafaf3f2701815b4fba4725446c95721601068c0000000006a47304402205d7a7f0c0f6c39a781aede0cc2cdfdd2a85fd5067b56c25538f122b1beb10c33022025dc77b83e9ae31bb8070eb7d3e7ae175c9525dc0b7041562a4e5f0fa643dc39012102213a7a9a3a97a241b17e7b2ca0026b9c0b48e0bfe553696746fb1ac4650183c6ffffffff01409a940c020000001976a9147096311efc9f506355118400fc3e1d83c7c1caba88ac00000000
```
The transaction id is returned as the output ```f5ef49f9f604729191060a3ea4ad4b1bebe0553d8e3fd006e88f6e5a7392cbb```

# Postman Collection Link 
A link to postman collection is given below to try out the above requests. 
```sh
https://www.getpostman.com/collections/a7e24be6f4ec3ebc6e7a
```