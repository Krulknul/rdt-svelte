# rdt-svelte

A Svelte 5 component to quickly get up and running with the [Radix dApp Toolkit](https://github.com/radixdlt/radix-dapp-toolkit) and its Connect Button.

# Installation
```bash
npm install rdt-svelte
```

# How to use

```ts
<script lang="ts">
    // Import the component
    // (Any other RDT types are re-exported by the package)
    import { ConnectButton, DataRequestBuilder } from "rdt-svelte";

    // Set up a reactive state variable to hold the button instance
    let button: ConnectButton | undefined = $state();

    // You can use $effect to use the button's api when it is ready.
    // Of course, the button will only be ready after the ConnectButton component is mounted.
    $effect(() => {
        button?.rdt?.walletApi.setRequestData(
            DataRequestBuilder.accounts().exactly(1),
        );
    });
</script>

<div class="connect-button">
    <!-- Use the component to put the button where you need it, and bind it to the reactive variable -->
    <ConnectButton bind:this={button} />
</div>

<p>{button?.walletData?.accounts[0]?.address}</p>

<style>
    .connect-button {
        position: fixed;
        top: 10px;
        right: 10px;
    }
</style>
```