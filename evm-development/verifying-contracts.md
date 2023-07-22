# Verifying Contracts

The contributor-operated block explorer at [https://tuber.build/](https://tuber.build/) supports contract verification, allowing you to share your smart contracts' source code, methods, and ABIs with users and developers through the explorer itself.

Another 3rd-party operated block explorer at [https://canto.dex.guru/](https://canto.dex.guru/) supports smart contract verification with a native UI for Sourcify.


## Verifying with Sourcify

At present, the explorer only supports contract verification via Sourcify. To verify a contract, follow these steps:

1. Navigate to the contract you would like to verify on the Canto block explorer.
2. On the _Code_ tab, click _Verify & Publish._
3. Select verification via Sourcify and click _Next._
4. Import or upload your project's source files and metadata.
   * For Hardhat, include the JSON file located at `artifacts/build-info`/
   * For Truffle, include the JSON file located at `build/contracts/`
5. Click _Verify & publish._ The contract will become verified within several minutes.

You can also verify contracts through the [Sourcify website](https://sourcify.dev/#/verifier). For more information on how to do so, as well as guidelines on how partial matches, libraries, and more are handled, see the [documentation](https://docs.sourcify.dev/docs/how-to-verify/).
