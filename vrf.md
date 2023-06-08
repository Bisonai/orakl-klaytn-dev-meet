# Orakl Network VRF (Verifiable Random Function)

Everything in this document should be executed from the root directory of the following git repository.

```
git clone https://github.com/Bisonai/vrf-consumer
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

https://github.com/Bisonai/vrf-consumer/blob/master/contracts/VRFConsumer.sol

### Temporary Account

```Solidity
function requestRandomWords(
    bytes32 keyHash,
    uint32 callbackGasLimit,
    uint32 numWords,
    address refundRecipient
) external payable returns (uint256 requestId);
```

### Permanent Account

```Solidity
function requestRandomWords(
    bytes32 keyHash,
    uint64 accId,
    uint32 callbackGasLimit,
    uint32 numWords
) external returns (uint256 requestId);
```

## 6. Deploy to Baobab

```
yarn compile
```

```
npx hardhat deploy --network baobab
```

## 7. Request for VRF with a temporary account

```
npx hardhat run scripts/read-vrf.ts --network baobab
```

```
npx hardhat run scripts/request-vrf-direct.ts --network baobab
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

## 10. Request for VRF with a permanent account

```
npx hardhat run scripts/read-vrf.ts --network baobab
```

```
npx hardhat run scripts/request-vrf.ts --network baobab
```
