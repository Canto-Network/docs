# Graph Node (Subgraphs)

{% hint style="info" %}
This page is a work in progress. Contributions are welcome on the [GitHub repo](https://github.com/Canto-Network/docs).
{% endhint %}

You can index historical activity on the Canto network by running a local Graph node, which custom subgraphs can be deployed to. This page contains instructions for doing so.

## Prerequisites

In order to spin up a Graph node, you will need access to a Canto node with historical data. The recommended approach is to sync your own [archive node](archive-node.md) first.

You'll also need to install Docker and Docker Compose on the machine you'll use to run the Graph node.

## Graph Node Setup

To set up the Graph node itself, start by cloning the default Graph repository:

```shell
git clone https://github.com/graphprotocol/graph-node/
```

If the Canto node you are using to sync is running on a different machine, change the RPC URL for the `ethereum` network in `graph-node/docker/docker-compose.yml`. Otherwise, the default value should work.

It is not necessary to change the name of the network, and doing so may require you to make additional config changes elsewhere.

Then run the setup file in `graph-node/docker` and start the node:

<pre class="language-shell"><code class="lang-shell"><strong># Run setup
</strong><strong>./setup.sh
</strong>
# Start Graph node
docker-compose up
</code></pre>

Optionally, use the `--detach` flag to start the Graph node in the background.

## Deploying Subgraphs

To deploy subgraphs to a Graph node, you'll need to create a subgraph specification consisting of both `subgraph.yaml` and `schema.graphql` files. Detailed information on creating subgraphs is available within [The Graph's documentation](https://thegraph.com/docs/en/developing/creating-a-subgraph/).

For contracts implementing common token standards like ERC20, ERC721, or ERC1155, you can use the [OpenZeppelin Subgraphs module](https://docs.openzeppelin.com/subgraphs/0.1.x/) to automatically generate a subgraph specification.

After compiling the specification files, run the following commands to create and deploy the subgraph:

```shell
# Create the subgraph
graph create generated/sample --node http://127.0.0.1:8020

# Deploy the subgraph
graph deploy --ipfs http://localhost:5001 --node http://localhost:8020 generated/sample ./generated/sample.subgraph.yaml
```

By default, Graph nodes host a GraphiQL user interface for each subgraph, which can be accessed at `http://localhost:8000/subgraphs/name/generated/sample`.

{% hint style="info" %}
These instructions are based on [a guide](https://medium.com/coinmonks/deploy-subgraphs-to-any-evm-aaaccc3559f) by Leon Do.
{% endhint %}
