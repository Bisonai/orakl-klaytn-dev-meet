# Orakl Network Data Feed

Everything in this document should be executed from the root directory of the following git repository.

```
git clone https://github.com/Bisonai/data-feed-consumer
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

https://github.com/Bisonai/data-feed-consumer/blob/master/contracts/DataFeedConsumer.sol

```Solidity
function latestRoundData()
    external
    view
    returns (
        uint80 id,
        int256 answer,
        uint256 startedAt,
        uint256 updatedAt,
        uint80 answeredInRound
    );
```

## 6. Deploy to Baobab

```
yarn compile
npx hardhat deploy --network baobab
```

## 7. Read from Orakl Network Data Feed

```
npx hardhat run scripts/read-data.ts --network baobab
```
