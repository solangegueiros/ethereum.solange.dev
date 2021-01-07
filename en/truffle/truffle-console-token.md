
### Connect with a published Token contract

First of all, connect with your token:

```javascript
const token = await Token.deployed()
```

Now `token` variable contains an instance of the previously deployed contract.

![token deployed](../../images/truffle-sol-token-box/image-09.png)

> [!TIP]
> Don't worry about the `undefined` return, it is ok. 

### Confirm if the token's instance is OK.

Enter the instance's name:  `token`, then type `.` (dot), without space hit the <kbd>&#8677;</kbd> TAB key twice to trigger auto-complete as seen below. 
This will display the published address of the smart contract, and the transaction hash for its deployment, among other things, including all public variables and methods available.

```javascript
token. [TAB] [TAB]
```

![token tab tab](../../images/truffle-sol-token-box/image-10.png)


### Check the total supply

To check if we have tokens already minted, call the `totalSupply` function:

```javascript
(await token.totalSupply()).toString()
```

The returned value is 0, which is expected, since we did not perform any initial mint when we deployed the token.

### Check the token balance

To check the balance of an account, call the `balanceOf` function. For example, to check the balance of account 0:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

The returned value is also 0, which is expected, since we did not make any initial mint when we deployed the token, and by definition no accounts can have any tokens yet.

Take a look in the results of total supply and balanceOf:

![total supply and balanceOf 0](../../images/truffle-sol-token-box/image-13.png)

### Mint tokens

Run this command:

```javascript
token.mint(accounts[0], 10000)
```

This command sent a transaction to mint 100 tokens, with 2 decimal places (00), for account 0. 

![token.mint account 0](../../images/truffle-sol-token-box/image-14.png)

You can also mint to a specific address, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
token.mint("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79", 10000)
```

![token.mint address](../../images/truffle-sol-token-box/image-15.png)

### Reconfirm the token balance

Check the balance of account 0 again:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

The returned value is 10000, which is 100 with 2 decimal places of precision. This is exactly what we expected, as we issued 100 tokens

Also, you can get the balance of a specific address, for example, `0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79`:

```javascript
(await token.balanceOf("0xa52515946DAABe072f446Cc014a4eaA93fb9Fd79")).toString()
```

Take a look in the balances:

![balanceOf account 0 and address with 10000](../../images/truffle-sol-token-box/image-18.png)

### Check the total supply (again)

Check the total supply again:

```javascript
(await token.totalSupply()).toString()
```

![totalSupply 20000](../../images/truffle-sol-token-box/image-19.png)

The returned value is 20000, which is 200 with 2 decimal places of precision. 
After minting 100 tokens for 2 accounts, this is perfect!

### Transfer tokens

Let's transfer 40 tokens from the first account (`accounts[0]`) to the third account (`accounts[2]`). 
This can be done by calling the `transfer` function.

```javascript
token.transfer(accounts[2], 4000, {from: accounts[0]})
```

![token.transfer](../../images/truffle-sol-token-box/image-20.png)

**What's happen after the transfer?**

- accounts[2] had no tokens before the transfer, and now it should have 40. 
- accounts[0] will have 60 tokens. 
- also the total supply must be the same.

Let’s check the balance of each account and the total supply.

- Balance of accounts[2]:

```javascript
(await token.balanceOf(accounts[2])).toString()
```

- Balance of accounts[0]:

```javascript
(await token.balanceOf(accounts[0])).toString()
```

- Total supply, one more time:

```javascript
(await token.totalSupply()).toString()
```

Take a look in the results:

![balances after transfer](../../images/truffle-sol-token-box/image-21.png)

Great! The balances of both accounts and the total supply are correct.
