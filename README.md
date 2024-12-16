This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-wagmi`](https://github.com/wevm/wagmi/tree/main/packages/create-wagmi).


Here are the commands to bootrap a WAGMI CLI project generating the methods for frontend integration
from scratch.

# Init Wagmi project. 
### Select a React framework project and open with NEXT.

```npm create wagmi@latest```

Once complete, run ```npm i``` inside the project
then you can start the project in browser by running ```npm run dev```

Let's install RainbowKit. It is an easy to use library to help developers easily allow their users to connect to your dApps with all sorts of different wallets. By default RainbowKit supports injected providers like Metamask, Rainbow, Coinbase Wallet, WalletConnect etc. Open up a terminal pointing to your directory and execute this command to install RainbowKit and its peer dependencies.

```npm install @rainbow-me/rainbowkit wagmi viem@2.x @tanstack/react-query```

In your main app page, perhaps within next.js its "app.ts" you could import the above libraries like this.

Compare with https://github.com/joedakwa/CryptoDAO-Wagmi for clarity on boilerplate.

DONT forget to visit https://cloud.reown.com/sign-in and create a project, then grab the project Id and place it over ```"projectId: "YOUR_PROJECT_ID",``` below

```
"use client";

import * as React from "react";
import {
  RainbowKitProvider,
  getDefaultWallets,
  getDefaultConfig,
  darkTheme,
} from "@rainbow-me/rainbowkit";

import {
  argentWallet,
  trustWallet,
  ledgerWallet,
} from "@rainbow-me/rainbowkit/wallets";

//importing the chains we need (here, just Sepolia)
import {
  sepolia
} from "wagmi/chains";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { WagmiProvider } from "wagmi";

const { wallets } = getDefaultWallets();

export const config = getDefaultConfig({
  appName: "ENS dapp",
  projectId: "YOUR_PROJECT_ID",
  // the above value needs to be replaced. You can do this here: https://cloud.reown.com/sign-in
  wallets: [
    ...wallets,
    {
      groupName: "Other",
      wallets: [argentWallet, trustWallet, ledgerWallet],
    },
  ],
  chains: [
   sepolia
  ],
  ssr: true,
});

// TanStack Query is a library that makes it very easy to fetch, cache and handle data.
// It gives you declarative, always-up-to-date auto-managed queries and mutations.
export const queryClient = new QueryClient();

export function Providers({ children }) {
  return (
    <WagmiProvider config={config}>
      <QueryClientProvider client={queryClient}>
        <RainbowKitProvider theme={darkTheme()}>{children}</RainbowKitProvider>
      </QueryClientProvider>
    </WagmiProvider>
  );
}
```


# Install Wagmi CLI

```
npm i @wagmi/cli
```

# Init Wagmi

```npx wagmi init```

# Generating methods

(Make sure you have an ETH API KEY in your .env file)

BEFORE you run the below command, you need to have deployed your contracts and imported the ABI into the WAGMI.CONFIG.TS file.

Refereced here: https://wagmi.sh/cli/getting-started

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


