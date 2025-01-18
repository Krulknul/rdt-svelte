<script lang="ts">
    import ConnectButton from "$lib/ConnectButton.svelte";

    let button: ConnectButton | undefined = $state();

    $inspect(button?.walletData);
</script>

<div class="connect-button">
    <ConnectButton bind:this={button} />
</div>

<p>{button?.walletData?.accounts[0].address}</p>

<button
    onclick={() => {
        button?.rdt.walletApi.sendTransaction({ transactionManifest: "" });
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
