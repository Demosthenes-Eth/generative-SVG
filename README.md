# generative-SVG
Attempt at creating a generative SVG with the ability to iterate and evolve over multiple generations.

I'm writing this initial proof-of-concept using Javascript with the intention to then rewrite the code in Solidity once I have the architecture down.  The end goal is to eventually try deploying an NFT contract that will mint NFTs featuring an algorithmically determined SVG image while also deploying new NFT contracts once the contract holds enough $ETH to do so.  The goal is for each new contract to inherit and then modify the existing SVG XML of its direct predecessor.  Additionally, I'm considering adding a kind of ownership aspect where if a user ends up deploying a new contract, they can collect a small percentage of the $ETH paid to mint the resulting NFT from that contract.  This would potentially provide incentivization for people to try to get the contracts to multiply.  My hope in the experiment is to observe the SVG imagery experiencing selective pressures as users choose to mint some branches of the contract lineage more than others, causing the contract lineage to diverge over time.

**Current Status:**
- Declared arrays to hold the SVG elements and their respective attributes.
- Declared arrays to hold the possible options for various element attributes.
- Declared sets to hold unique element Ids and Classes.
- In the process of writing helper functions to generate and return specific values for different types of properties.  These will be called when the algorithm needs to generate an element and attribute that requires a value in an attribute-specific format.

**Next Steps:**
- Finish writing helper functions
- Write element generator functions
- Write main SVG generator function
- Test vanilla JS proof-of-concept
- Rewrite the proof-of-concept using Solidity and incorporate into an NFT smart contract
- Test initial inefficient smart contract version
- Potentially incorporate gas sponsorship logic using ERC-4337
- Test final smart contract(s) on local testnet
- Deploy final smart contract(s) to Base, Optimism, Arbitrum, or other L2

**General Conceptualization:**
- The SVG markup will be conceived of a stack with each layer of the stack representing a layer in the SVG.  The `svgStackSize` variable defines the number of layers available to the SVG image and can be modified per generation like most other aspects of the SVG.  The main SVG generator function will loop using the `svgStackSize` as its counter value and store each returned layer of SVG markup in the `svgStack` array.  The loop will employ `Math.floor(Math.random())` to randomly select an index value for the `svgElements` array which will determine what element gets placed next in the stack.  Once the element has been chosen, the algorithm will call the appropriate element generator function to iterate over the attribute properties of that specific element and call all necessary helper functions to provide the attribute values.

**Areas Requiring Additional Thought:**
- Determine the logic how the SVG will handle inherited markup and incorporate the use of inherited markup into the main generator logic.  Right now, my plan is to have the algorithm store inherited markup as `<defs>` and implement them with `<use>`, which is one reason why I'm including id generation in the algorithm.
- Determine the logic for how the SVG will handle nested elements in relationship to the SVG stack.  Does `<g></g>` count as 1 stack layer or two?  And what determines if a subsequent element exists inside the container element or outside of it?

**Other Notes:**
- I am currenly leaving clipping masks, SVG filter effects, and SVG animations out of the algorithm for now because of the added complexity they bring to the table.  But in the future, these could greatly increase the amount of interesting variation possible for each new generation.
- When converting from Javascript to Solidity, I will likely transition from using Javascript sets to track unique element ids to using solidity mappings instead.  That way, I could just require that the mapped value of a specific id != 0 to determine whether that id already exists.
