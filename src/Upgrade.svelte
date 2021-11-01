<script lang="ts">
  export let upgradeCost = 0;
  export let upgradeCps = 0;
  export let buyUpgrade: (id: string) => () => void =
    () => () => {};
  export let cookieCount;
  export let upgradeLabel = "";
  export let upgradeId = '';
  export let upgradeCount = 0;
</script>

<div class="upgrade">
  {upgradeCount}x {upgradeLabel} ({upgradeCps}cps) <button
    on:click={buyUpgrade(upgradeId)}
    disabled={cookieCount < upgradeCost}>{upgradeCost}</button
  >
</div>

<style lang="scss">
    .upgrade {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    button {
        padding: 0.5em 2em;
        background: #75a1cf;
        border: none;
        color: white;
        margin-left: 1rem;
        margin-bottom: 0;
        &:disabled {
          background: transparent;
          border: 1px solid #75a1cf;
        }
      }
</style>
