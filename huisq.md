---
timezone: Asia/Shanghai
---

---

# huisq

1. 自我介绍
编程爱好者
2. 你认为你会完成本次残酷学习吗？
会
## Notes

<!-- Content_START -->

### 2024.09.09
创建新的合约框架：
```
aptos move init --name <PROJECT_NAME>
```
其中合约框架里必须包含的有：sources/file_name.move 和 Move.toml

接下来想研究的方向：
1. composable NFT ---> done
2. sponsored transaction
3. fractionalized NFT ---> done
4. Move 2.0 Language Release ---> done
5. move prover ---> done
6. Cryptography in Move

### 2024.09.10
Composable NFT

Basically the idea of an object owning another object. Simply store the child object inside the field of the parent object. It can be detached at any times but cannot be transfered alone while attached together.
Example:
```move
    #[resource_group_member(group = aptos_framework::object::ObjectGroup)]
    /// A face token, that can wear a hat and dynamically change
    struct Face has key {
        hat: Option<Object<Hat>>,
    }

    #[resource_group_member(group = aptos_framework::object::ObjectGroup)]
    /// A hat with a description of what the hat is
    struct Hat has key {
        type: String
    }
```
Face is the parent object and Hat is the child object, below code shows how to "wear" the Hat.
```move
/// Attaches a hat from the owner's inventory
    ///
    /// The hat must not be already owned by the face, and there should be no hat already worn.
    entry fun add_hat(
        caller: &signer,
        face_object: Object<Face>,
        hat_object: Object<Hat>
    ) acquires Face, Hat, ObjectController, TokenController {
        let caller_address = signer::address_of(caller);
        assert!(caller_address == object::owner(face_object), E_NOT_OWNER);
        assert!(caller_address == object::owner(hat_object), E_NOT_OWNER);

        let face_address = object::object_address(&face_object);
        let hat_address = object::object_address(&hat_object);

        // Transfer hat to face
        object::transfer(caller, hat_object, face_address);

        // Attach hat to face
        let face = borrow_global_mut<Face>(face_address);
        assert!(option::is_none(&face.hat), E_HAT_ALREADY_ON);
        option::fill(&mut face.hat, hat_object);

        let hat = borrow_global<Hat>(hat_address);
        let token_controller = borrow_global<TokenController>(face_address);

        // Update the URI for the dynamic nFT
        // TODO: Support more hats
        if (hat.type == string::utf8(SAILOR_HAT)) {
            token::set_uri(&token_controller.mutator_ref, string::utf8(FACE_WITH_SAILOR_HAT_URI))
        } else {
            abort E_UNSUPPORTED_HAT
        };

        // Updates the description to have the new hat
        token::set_description(
            &token_controller.mutator_ref,
            string_utils::format2(&b"{} {}", string::utf8(FACE_WIF_HAT), hat.type)
        );

        // Disable transfer of hat (so it stays attached)
        let hat_controller = borrow_global<ObjectController>(hat_address);
        assert!(option::is_some(&hat_controller.transfer_ref), E_NO_TRANSFER_REF);
        let hat_transfer_ref = option::borrow(&hat_controller.transfer_ref);
        object::disable_ungated_transfer(hat_transfer_ref);
    }
```

### 2024.09.11
Lots of updates in Move 2.0 to catch up on. 
https://aptos.dev/en/build/smart-contracts/book/move-2.0

somehow resource objects require these tags now?:
```move
module 0x42::example {
  #[resource_group(scope = global)]
  struct ObjectGroup { }
 
  #[resource_group_member(group = 0x42::example::ObjectGroup)]
  struct Monkey has store, key { }
}
```

### 2024.09.12
Fractionalized NFT
--> done by fractionalize Digital Asset
- a single item is split into fractional ownership, a percentage of the full item.
- ExtendRef for allowing someone to defractionalize the asset only if they have 100% of it
- `primary_fungible_store::create_primary_store_enabled_fungible_asset` to attach the metadata
- `primary_fungible_store::mint` to mint the supply of FA

```move
    #[resource_group_member(group = aptos_framework::object::ObjectGroup)]
    /// A locker for a digital asset and fractionalizes it accordingly
    struct FractionalDigitalAsset has key {
        /// The address of the locked up token
        asset: Object<TokenObject>,
        /// For transferring the locked up token back out
        extend_ref: ExtendRef,
        /// For burning the tokens at the end
        burn_ref: BurnRef,
        /// For locking/unlocking the token from the object containing the token
        transfer_ref: TransferRef,
    }
```

### 2024.09.13
The Move Prover supports formal specification and verification of Move code.
My understanding as a format check?

```
aptos move prove
```
to use 

### 2024.09.14
Sponsored transaction.

Need to use Go/TS SDK to perform. 
TS SDK would be preferred personally.

TS code sample:
```typescript
/**
 * This example shows how to use the Aptos SDK to send a transaction with a sponsor.
 */
 
import {
    Account,
    Aptos,
    AptosConfig,
    Network,
} from "@aptos-labs/ts-sdk";
 
async function example() {
    console.log("This example will send a sponsored transaction from Alice to Carol.");
 
    // 0. Setup the client and test accounts
    const config = new AptosConfig({ network: Network.TESTNET });
    const aptos = new Aptos(config);
 
    let alice = Account.generate();
    let bob = Account.generate();
    let carol = Account.generate();
 
    console.log("=== Addresses ===\n");
    console.log(`Alice's address is: ${alice.accountAddress}`);
    console.log(`Bob's address is: ${bob.accountAddress}`);
    console.log(`Carol's address is: ${carol.accountAddress}`);
 
    console.log("\n=== Funding accounts ===\n");
    await aptos.fundAccount({
        accountAddress: alice.accountAddress,
        amount: 500_000_000,
    });
    await aptos.fundAccount({
        accountAddress: bob.accountAddress,
        amount: 500_000_000,
    });
    await aptos.fundAccount({
        accountAddress: carol.accountAddress,
        amount: 100,
    });
    console.log("Funded the accounts!")
 
    // 1. Build
    console.log("\n=== 1. Building the transaction ===\n");
    const transaction = await aptos.transaction.build.simple({
        sender: alice.accountAddress,
        withFeePayer: true,
        data: {
            // All transactions on Aptos are implemented via smart contracts.
            function: "0x1::aptos_account::transfer",
            functionArguments: [carol.accountAddress, 100],
        },
    });
    console.log("Built the transaction!")
 
    // 2. Sign
    console.log("\n=== 2. Signing transaction ===\n");
    const aliceSenderAuthenticator = aptos.transaction.sign({
        signer: alice,
        transaction,
    });
    const bobSenderAuthenticator = aptos.transaction.signAsFeePayer({
        signer: bob,
        transaction
    })
    console.log("Signed the transaction!")
 
    // 3. Simulate (Optional)
    console.log("\n === 3. Simulating Response (Optional) === \n")
    const [userTransactionResponse] = await aptos.transaction.simulate.simple({
        signerPublicKey: alice.publicKey,
        feePayerPublicKey: bob.publicKey,
        transaction,
    });
    console.log(userTransactionResponse)
 
    // 4. Submit
    console.log("\n=== 4. Submitting transaction ===\n");
    const committedTransaction = await aptos.transaction.submit.simple({
        transaction,
        senderAuthenticator: aliceSenderAuthenticator,
        feePayerAuthenticator: bobSenderAuthenticator,
    });
    console.log("Submitted transaction hash:", committedTransaction.hash);
 
    // 5. Wait for results
    console.log("\n=== 5. Waiting for result of transaction ===\n");
    const executedTransaction = await aptos.waitForTransaction({ transactionHash: committedTransaction.hash });
    console.log(executedTransaction)
};
 
example();
```

### 2024.09.15

<!-- Content_END -->
