<script lang="ts">
    import {
        DataRequestBuilder,
        RadixDappToolkit,
        type RadixDappToolkitOptions,
        type WalletDataState,
    } from "@radixdlt/radix-dapp-toolkit";

    let rdt: RadixDappToolkit | undefined = $state();
    let walletData: WalletDataState | undefined = $state();
    export { rdt, walletData };

    let { options }: { options: RadixDappToolkitOptions } = $props();

    $effect(() => {
        // Initialize the toolkit
        const toolkit = RadixDappToolkit(options);
        // bridge the wallet data to Svelte reactive state
        toolkit.walletApi.walletData$.subscribe((data) => {
            walletData = data;
        });
        rdt = toolkit;
        return () => {
            rdt?.destroy();
        };
    });
</script>

<radix-connect-button></radix-connect-button>

<style>
    radix-connect-button {
        --radix-connect-button-border-radius: 5px;
        --radix-connect-button-width: 36px;
    }
    @media (min-width: 640px) {
        radix-connect-button {
            --radix-connect-button-width: 140px;
        }
    }
</style>
