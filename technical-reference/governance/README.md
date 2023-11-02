# Governance

Canto introduces a new paradigm for governance called **unified governance** where governance of both the network itself _and_ Free Public Infrastructure applications is controlled by network token stakeholders.

At launch, this means that Canto stakers can participate in governance of the Canto Lending Market, the Canto DEX, and the network itself. Any new primitives built under the Free Public Infrastructure model will also leverage unified governance as appropriate.

## Overview

Canto governance is based on the Cosmos SDK `x/gov` module with the addition of a custom-built module, `x/govshuttle`. The GovShuttle module is responsible for pushing passed proposal data from the governance module to a storage smart contract in the Canto EVM so that it can be read by DApps.
