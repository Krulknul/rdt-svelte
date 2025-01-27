<script lang="ts">
    // When importing from another project, it'd be more like:
    // import { ConnectButton } from "rdt-svelte";
    import ConnectButton from "$lib/ConnectButton.svelte";
    import { DataRequestBuilder } from "@radixdlt/radix-dapp-toolkit";

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
    <ConnectButton
        bind:this={button}
        options={{
            networkId: 1,
            dAppDefinitionAddress:
                "account_rdx16xdanhhgzzyen33q3fq3ljhekjh0ezh2gnu6z0gcrtsn9u29s2rwu7",
        }}
    />
</div>

<p>{button?.walletData?.accounts[0]?.address}</p>

<style>
    .connect-button {
        position: fixed;
        top: 10px;
        right: 10px;
    }
</style>
