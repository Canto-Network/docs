# Troubleshooting

## Common Errors and Solutions

Here are a list of common errors when launching a node and their recommended solutions:

<table><thead><tr><th width="417">Error Description</th><th>Recommended Solution(s)</th></tr></thead><tbody><tr><td>Default gas fails when staking</td><td>Use <code>--gas auto</code></td></tr><tr><td><code>Error: couldn't read GenesisDoc file: open /root/.cantod/config/genesis.json: no such file or directory</code></td><td><p>Put the <code>genesis.json</code> file in the specified location, such as:</p><p><code>sudo wget https://github.com/Canto-Network/Canto/raw/main/Mainnet/genesis.json -P/root/.cantod/config/</code></p></td></tr><tr><td><code>Error during handshake: error on replay: validator set is nil in genesis and still empty after InitChain</code></td><td>Local: Remove <code>datadir</code> and restart<br><br>Cloud: Start a new instance</td></tr><tr><td><code>Failed to execute message; message index: 0: failed to delegate; acanto is smaller than acanto: insufficient funds"</code></td><td>Decrease the amount to less than your total $CANTO balance</td></tr><tr><td><code>Stopping peer for error</code></td><td>No action required</td></tr></tbody></table>

## Tip: Rebuild from Scratch

If you run into unexpected issues when launching your node, it's worth rebuilding from scratch prior to any troubleshooting efforts. Follow these steps:

1. Delete `addressbook.json` in the config
2. Remove all old peers
3. Update persistent peers and seeds to newly shared
4. Fetch the new genesis file
5. Ensure binary is up to date
6. Start your node

## Tip: Consult EVMOS Docs

If you get stuck with something that isn't explained here, a good place to look for more information about your issue is the EVMOS community and docs.
