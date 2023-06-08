# Orakl Network Request-Response

Everything in this document should be executed from the root directory of the following git repository.

```
https://github.com/Bisonai/request-response-consumer
```

## 0. Install dependencies

```
yarn install
```

## 1. Create mnemonics

```
npx mnemonics
```

## 2. Create `.env` file

```
MNEMONIC=<YOUR MNEMONIC FROM STEP 1>
PROVIDER=https://api.baobab.klaytn.net:8651
```

## 3. Convert mnemonic to address

```
npx hardhat address --mnemonic "<YOUR MNEMONIC FROM STEP 1>"
```

## 4. Request $KLAY

Insert your address from previous step and request $KLAY.

https://baobab.wallet.klaytn.foundation/faucet

## 5. Examine consumer smart contract code

https://github.com/Bisonai/request-response-consumer/blob/master/contracts/RequestResponseConsumer.sol

### Temporary Account

```Solidity
function requestData(
    Orakl.Request memory req,
    uint32 callbackGasLimit,
    uint8 numSubmission,
    address refundRecipient
) external payable returns (uint256);
```

### Permanent Account

```Solidity
function requestData(
    Orakl.Request memory req,
    uint32 callbackGasLimit,
    uint64 accId,
    uint8 numSubmission
) external returns (uint256);
```

## 6. Deploy to Baobab

```
yarn compile
```

```
npx hardhat deploy --network baobab
```

## 7. Request data with a temporary account

```
npx hardhat run scripts/read-response.ts --network baobab
```

```
npx hardhat run scripts/request-data-direct.ts --network baobab
```

## 8. Create a permanent account and deposit $KLAY

```
npx hardhat createAccount --network baobab
```

```
npx hardhat deposit \
    --account-id $ACCOUNT \
    --amount $AMOUNT \
    --network baobab
```

## 9. Add a consumer to a permanent account

```
npx hardhat addConsumer \
    --consumer $CONSUMERADDRESS \
    --account-id $ACCOUNT \
    --network baobab
 ```

## 10. Request data with a permanent account

```
npx hardhat run scripts/read-response.ts --network baobab
```

```
npx hardhat run scripts/request-data.ts --network baobab
```
