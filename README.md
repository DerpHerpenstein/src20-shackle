# SRC-20 OP: Shackle

## Introduction
The Bitcoin Stamps ecosytem was built on Counterparty.  Art stamps remain 100% useable on Counterparty, but due to some internal conflict in the past, the SRC-20 token standard no longer has any connection to the broader Counterparty ecosystem. This issue divides and confuses the community, and makes it more difficult to build infrastructure.  

Since ths Stamps indexer utilizes a Counterparty indexer, it would be possible to make a small update to the SRC-20 token standard that allows SRC-20 tokens to be attached to Stamps. This is desireable because it will allow for SRC-20 to take advantage of the new developments in the Counterparty protocol, and it will allow SRC20 tokens to bring liquidity into the Counterparty ecosystem.

## Operations
### SHACKLE
Shackling an SRC-20 will attach it to a Stamp.  This operation will deduct the SRC-20 tokens from the callers wallet and move them into the "to" Stamp.
#### Note: The logic for this will be similar to "TRANSFER".  The main difference being that the "to" destination is not an address.  Instead, STAMP_CPID would be the new owner of these tokens
```
{
    "p": "src-20",
    "op": "shackle",
    "tick": "STAMP",
    "amt": "100"
    "to": "A12345678912345678",   
}  
```

### UNSHACKLE
Unshackling an SRC-20 will remove it from Stamp.  This operation will deduct the SRC-20 tokens from the Stamp and move them from the "from" field into the callers wallet.
#### Note: The logic for this will be similar to "TRANSFER".  The main difference being that the source is not an address, and there would need to be a check to verify that the caller is the owner of the "from" Stamp before moving the tokens from STAMP_CPID to the callers address. 
```
{
    "p": "src-20",
    "op": "shackle",
    "tick": "STAMP",
    "amt": "100"
    "from": "A12345678912345678",   
}  
```

### RESHACKLE
Reshackling an SRC-20 will remove it from the "from" Stamp and move it to the "to" Stamp.
#### Note: The logic for this will be similar to "TRANSFER".  The main difference being that the source is not an address, and there would need to be a check to verify that the caller is the owner of the "from" Stamp before moving the tokens to the "to" destination
```
{
    "p": "src-20",
    "op": "shackle",
    "tick": "STAMP",
    "amt": "100"
    "from": "A12345678912345678",
    "to": "A333333333333333333",  
}  
```

## SRC-20 Shackle Requirements
The CPID that the SRC-20 is being shackled to:
1. Must be a valid stamp
2. Must have a locked supply
3. Must have a value of 1
4. Must not be divisible
