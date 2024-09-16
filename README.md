This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-wagmi`](https://github.com/wevm/wagmi/tree/main/packages/create-wagmi).


Here are the commands to bootrap a WAGMI CLI project generating the methods for frontend integration
from scratch.

# Init Wagmi project. 
### Select a React framework project and open with NEXT.

```npm create wagmi@latest```

Once complete, run ```npm i``` inside the project
then you can start the project in browser by running ```npm run dev```

# Install Wagmi CLI

```
npm i @wagmi/cli
```

# Init Wagmi

```npx wagmi init```

# Generating methods

(Make sure you have an ETH API KEY in your .env file)

```
npx wagmi generate
```

### Once you have deployed your contract and the ABI sits in the OUT file, you can look at running something similar to the below.

You will need to import the relevant FOUNDRY package below in order to interact with your deployed contracts

https://wagmi.sh/cli/api/plugins/foundry

```
import { useReadErc20, useReadErc20BalanceOf } from './generated'

// Use the generated ERC-20 read hook
const { data } = useReadErc20({
  address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
  functionName: 'balanceOf',
  args: ['0xA0Cf798816D4b9b9866b5330EEa46a18382f251e'],
})

// Use the generated ERC-20 "balanceOf" hook
const { data } = useReadErc20BalanceOf({
  address: '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48',
  args: ['0xA0Cf798816D4b9b9866b5330EEa46a18382f251e'],
})
```

Visit https://wagmi.sh/cli/api/plugins for various ways to retrieve generated out files and extract from various applications


