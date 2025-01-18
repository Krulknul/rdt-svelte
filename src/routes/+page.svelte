<script lang="ts">
    import ConnectButton from "$lib/ConnectButton.svelte";
    import { DataRequestBuilder } from "@radixdlt/radix-dapp-toolkit";

    let button: ConnectButton | undefined = $state();

    $inspect(button?.walletData);

    $effect(() => {
        button?.rdt?.buttonApi.setTheme("black");
        button?.rdt?.walletApi.setRequestData(
            DataRequestBuilder.accounts().exactly(1),
        );
    });
</script>

<div class="connect-button">
    <ConnectButton bind:this={button} />
</div>

<p>{button?.walletData?.accounts[0]?.address}</p>

<button
    onclick={() => {
        button?.rdt?.walletApi.sendTransaction({ transactionManifest: "" });
    }}
>
    sendTransaction
</button>

<style>
    .connect-button {
        position: fixed;
        top: 10px;
        right: 10px;
    }
</style>
