
Get your accounts in Truffle console.

In the Truffle console, enter:

```javascript
const accounts = await web3.eth.getAccounts()
```

Don’t worry about the `undefined` return, it is ok. See the addresses after it by entering the command below:

```javascript
accounts
```

To view the first account:

```javascript
accounts[0]
```

And the second account:

```javascript
accounts[1]
```

Take a look at the accounts:

![accounts](../../images/truffle/image-07.png)


### Get balance

To check the balance of an account, for example, `accounts[0]`,
run this command in Truffle console:

```javascript
(await web3.eth.getBalance(accounts[0])).toString()
```

The result is returned in `wei`:

![getBalance](../../images/truffle/image-12.png)
