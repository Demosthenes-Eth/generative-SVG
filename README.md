# generative-SVG
Attempt at creating a generative SVG with the ability to iterate and evolve over multiple generations.

I'm writing this initial proof-of-concept using Javascript with the intention to then rewrite the code in Solidity once I have the structure down.  The end goal is to eventually try deploying an NFT contract that will mint NFTs featuring an algorithmically determined SVG image while also deploying new NFT contracts using CREATE2 once the contract holds enough $ETH to do so.  The goal is for each new contract to inherit and then modify the existing SVG XML of its direct predecessor.  My hope in the experiment is to observe the SVG imagery experiencing selective pressures as users choose to mint some branches of the contract lineage more than others, causing the contract lineage to diverge over time.
