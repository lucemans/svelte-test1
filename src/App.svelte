<script lang="ts">
  import { onMount } from "svelte";
  import Upgrade from './Upgrade.svelte';

  export let cookieCount = 0;
  export let upgrades = 0;

  const clickCookie = () => {
    cookieCount += 1;
  };

  const buyUpgrade = (price: number, amount: number) => () => {
    if (cookieCount >= price) {
      cookieCount -= price;
      upgrades += amount;
    }
  };

  onMount(() => {
    const interval = setInterval(() => {
      cookieCount += upgrades;
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });
</script>

<div class="wrapper">
  <main>
    <img
      src="https://freesvg.org/img/1548612994.png"
      alt=""
      on:click={clickCookie}
    />
    <h1>You have {cookieCount} cookies!</h1>
    {#if upgrades > 0}
    <h2>Auto-farming {upgrades} per second</h2>
    {/if}
    <div class="upgrades">
      <Upgrade upgradeLabel="Farmer" upgradeCost={10} upgradeCps={1} cookieCount={cookieCount} buyUpgrade={buyUpgrade}/>
      <Upgrade upgradeLabel="Machinery" upgradeCost={20} upgradeCps={5} cookieCount={cookieCount} buyUpgrade={buyUpgrade}/>
      <Upgrade upgradeLabel="Bakery" upgradeCost={50} upgradeCps={10} cookieCount={cookieCount} buyUpgrade={buyUpgrade}/>
    </div>
  </main>
  <a class="copyright" href="https://github.com/lucemans" target="_blank"
    >Luc van Kampen</a
  >
</div>

<style lang="scss">
  :global(html),
  :global(body) {
    margin: 0;
    padding: 0;
  }
  * {
    box-sizing: border-box;
  }
  .wrapper {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: radial-gradient(#4c7aab, #7199c3);
    /* background: radial-gradient(#111, #222); */
    user-select: none;
    .copyright {
      position: absolute;
      bottom: 1em;
      right: 1em;
      color: white;
      text-decoration: underline;
      &:hover {
        font-weight: bolder;
      }
    }
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 600px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    img {
      height: 200px;
      width: 200px;
      max-width: 80%;
      object-fit: contain;
      transition: 250ms;
      cursor: pointer;
      -webkit-user-drag: none;
      -khtml-user-drag: none;
      -moz-user-drag: none;
      -o-user-drag: none;
      user-drag: none;
      &:hover {
        transform: scale(1.05);
      }
      &:active {
        transform: scale(0.9);
      }
    }
    .upgrades {
      margin-top: 2rem;
      display: flex;
      justify-content: flex-start;
      align-items: stretch;
      flex-direction: column;
      border: 1px solid white;
      border-radius: 5px;
      padding: 1rem;
      color: white;
      gap: 1rem;
    }
  }

  h1 {
    /* color: #411c10; */
    color: white;
    text-transform: uppercase;
    font-size: 3em;
    font-weight: 100;
    margin-bottom: 0;
  }
  h2 {
    /* color: #411c10; */
    color: rgba(255, 255, 255, 0.651);
    font-size: 2em;
    font-weight: 100;
    margin: 0;
    padding: 0;
  }
</style>
