<script lang="ts">
  export let upgradeCost = 0;
  export let upgradeCps = 0;
  export let buyUpgrade: (price: number, cps: number) => () => void =
    (price, cps) => () => {};
  export let cookieCount;
  export let upgradeLabel = "";
</script>

<div class="upgrade">
  {upgradeLabel} ({upgradeCps}cps) <button
    on:click={buyUpgrade(upgradeCost, upgradeCps)}
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
