
<div align="center" style="margin-top: 1em; margin-bottom: 3em;">
  <a href="https://npics.xyz"><img alt="NPics logo" src="./npics-transparent.png" alt="npics.xyz" width="150"></a>
</div>


# NFT-backed Position

The protocol architecture of NBP( NFT-backed Position)

## What is NBP?

One-click down payment and financing to purchase a Blue-chip, which achieved through NFT-backed Postion (NBP) in just one call.

NBP stands for NFT-backed Position protocol, a bundle of smart contracts which runs on the Ethereum blockchain now.

And the vault is a type of NFT position administered by NBP protocol. Each vault debted with a single NFT collateral. The generation and close-out of each vault are pegged to mint and burn a Neo-NFT, which stands for NFT Everlasting Option of Npics, as a synthetic version of their purchased NFT, also as an on-chain NFT position, modeled on the ERC721 standard.

Through NPics Marketplace V0.1, anyone who wants to own Blue-chip NFTs can down pay buy with 40% off price, open and close the vault backed by the loan of that NFT instantly. Meanwhile, the owner will get a NEO-NFT for the life of the loan to use according to the use case of the collection’s NFTs, anything claimable of original NFT which it be used as a collateral, including airdrops, rewards and loan interets, delivered the same digital self-expression.

## Technology

**I. Flashloan**

One of the key innovations in enabling mortgage to purchase NFTs. 
Once the user completes the purchase and pays the required down payment,  the contract  first borrows the principal through the flash loan protocols, add the down payment paid by users, then generating route to buy the specified NFT at the best price among current NFT marketpalce.

The third step is to deposit NFT and borrow funds to repay the flash loan in the  pre-selected lending pool with the  optimal LTV. Finally, the nft purchase is realized, and the user successfully opens a vault.

After that, users can choose to repay and redeem NFT by themselves, or they can directly sell the vault to settle the profit.

The platforms that support flash loan are: uniswap, aave, dydx, among which uniswap supports lending of any erc20 token, but needs to pay 0.3% of the loan as a handling fee. AAVE supports most mainstream tokens, and needs to pay 0.09% as a handling fee. Among the three, we chose dydx. Although it only supports WETH, DAI, and USDC, the fee is the lowest, only 2Gwei.

Reference: 

[https://github.com/Dapp-Learning-DAO/Dapp-Learning/blob/main/basic/20-flash-loan/readme.md](https://github.com/Dapp-Learning-DAO/Dapp-Learning/blob/main/basic/20-flash-loan/readme.md)

[https://docs.aave.com/developers/guides/flash-loans](https://docs.aave.com/developers/guides/flash-loans)


**II. NEO-NFT ( NFT Everlasting Options)** 

Once user makes their down payment, the purchase deal, ownership of the NFT will transfer to seperated contract address, NPB protocol will mint A NEO-NFT will be minted as synthetic version of the purchased NFT, which as an everlasting option, and the neo holder has the right to repay mortgage amount(prinicple and interests),  and redeem your NFT (redemption).

A NBP represents a long term bet on an underlying NFT and has no expiry, and a single floating strike. Designed for future  on-chain derivative market where for speculation instead of selling your rare NFTs. Which means users can speculate on bluechip NFTs at  cheaper price in comparison to the floor of the NFT. Imagine paying 100eth to speculate on bored ape which can now be achieved by purchasing the call option worth 1eth.

Just like warrants, CBBCs are issued with a strike or exercise price, an expiration date, a conversion ratio and other similar terms. Concept-wise, CBBCs work in much the same way as index futures to leverage on the rise or fall of a market.

Reference: 

[https://www.paradigm.xyz/2021/05/everlasting-options](https://www.paradigm.xyz/2021/05/everlasting-options)

[https://01exchange.medium.com/01s-everlasting-options-6d918d461a84](https://01exchange.medium.com/01s-everlasting-options-6d918d461a84)

[https://en.wikipedia.org/wiki/Callable_bull/bear_contract](https://en.wikipedia.org/wiki/Callable_bull/bear_contract)

[https://www.hkex.com.hk/Global/Exchange/FAQ/Products/Securities/CBBC?sc_lang=en](https://www.hkex.com.hk/Global/Exchange/FAQ/Products/Securities/CBBC?sc_lang=en)


**III. NBP- NFT-backed Position**

When depositng NFT to lend principal , the lending protocol will mint a corresponding debt NFT to user, indicating the user's NFT debt position, but it cannot be transferred. The existing NFT lending protocol and yield farming are also based on each wallet address, not a single debt. 

In order to increase the liquidity of NFT debt and allow that debt to change hands, we designed the mechanism of NEO+NBP. Each NFT debt ( bendNFT) will be held by an independent nbp (NFT Backed Position) smart contract,  which is controlled by the corresponding neo NFT. Holding a neo-NFT means having a collateralized debt position, which can be freely transferred and sold. Likewise, the address will receive all claimable yields and airdrops while holding neo-nft.

Reference:

[https://makerdao.com/en/whitepaper/sai/#collateralized-debt-position-smart-contracts](https://makerdao.com/en/whitepaper/sai/#collateralized-debt-position-smart-contracts)

[https://makerdao.com/en/whitepaper/#the-dai-stablecoin](https://makerdao.com/en/whitepaper/#the-dai-stablecoin)

**IV. Beacon Proxy**

As a highly competitive Nft-Fi product, NPics will continue to iterate rapidly in accordance with planning and industry rhythms. In order to keep pace with product upgrades, especially the above-mentioned architectures ( NEO-NFT, NBP, etc.) , we adopted the beacon
 proxy pattern (EIP-1967 standard) at the beginning, a gas-efficient pattern that allows multiple proxies to be upgraded to a different implementation in a single transaction, and the upgrade operations that are sent to the beacon instead of to the proxy contract, only underlying logic to be upgraded when needed, all proxies that follow that beacon are automatically upgraded. which is similar to the factory method of design pattern

Reference: 

https://eips.ethereum.org/EIPS/eip-1967


**V. Minimum Proxy**

In view of the logic that each NFT mortgage generation needs to create a NBP contract, in order to save gas, NPics uses the minimum proxy contract( EIP-1167 standard) as an effort to reduce gas costs as much as possible., which is only 45 bytes of proxy contract sizeand has zero impact on runtime gas costs.

Reference: 

[https://eips.ethereum.org/EIPS/eip-1167](https://eips.ethereum.org/EIPS/eip-1167)

[https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1167.md](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1167.md)


## Thanks

The NBP protocol architecture references the design management model of [CDP](https://docs.makerdao.com/smart-contract-modules/proxy-module/cdp-manager-detailed-documentation) of MarkDAO in the smart contract part and adopted [GEM.XYZ](https://www.gem.xyz) and [DYDX](https://github.com/dydxprotocol) and BendDAO(https://github.com/BendDAO/bend-protocol) part of the code.

We are very grateful to MarkDAO, GEM, DYDX and BendDAO for providing us with an excellent DeFi platform.


## Community

We welcome more volunteers to join us in building a fast-growing volunteer community , [joining us](https://discord.gg/6qb739B9)

## Getting Started


## Setup


## Markets configuration


## Test


## Deployment



## Etherscan verification

