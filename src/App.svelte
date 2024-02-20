<script>
  import * as d3 from 'd3';
  import Header from './components/Header.svelte';
  import Select from 'svelte-select';
  import Scatterplot from './components/Scatterplot.svelte';
  import Footer from './components/Footer.svelte';
  import { players } from '../public/data/players2023.js';

  let nbaStats;
  let val = "";
  let selectedPosition = "allPositions";
  let filteredData;

  $: value = null;

  d3.csv('../data/nba2023.csv').then(data => (nbaStats = data));

  const handleSelect = event => {
    value = event.detail.value;
    updateFilteredData();
  };

  const handleClear = () => {
    value = null;
  };

  const updateFilteredData = () => {
    if (selectedPosition == "allPositions") {
      filteredData = nbaStats;
    } else {
      filteredData = nbaStats.filter(d => d.position == selectedPosition);
    }
  };
</script>

<main>
  <div class="app">
    <Header />
    <label for="positionSelector">Select Player Position:</label>
    <select bind:value={val} id="positionChoice">
      <option value="allPositions">All Positions</option>
      <option value="PG">Point Guard</option>
      <option value="SG">Shooting Guard</option>
      <option value="SF">Small Forward</option>
      <option value="PF">Power Forward</option>
      <option value="C">Center</option>
      <!-- Add more options based on your data -->
    </select>


    <div class="selector">
      <Select
        items={players}
        placeholder="Select player..."
        inputStyles="font-family: Source Sans Pro;"
        on:select={handleSelect}
        on:clear={handleClear}
      />
    </div>

    {#if nbaStats}
      <Scatterplot data={nbaStats} selectedPlayer={value} selectedPosition={val}/>
    {/if}

    <Footer />
  </div>
</main>

<style>
  @font-face {
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 700;
    src: local(''),
      url('../fonts/merriweather-v25-latin-700.woff2') format('woff2'),
      url('../fonts/merriweather-v25-latin-700.woff') format('woff');
  }

  @font-face {
    font-family: 'Source Sans Pro';
    font-style: normal;
    font-weight: 400;
    src: local(''),
      url('../fonts/source-sans-pro-v14-latin-regular.woff2') format('woff2'),
      url('../fonts/source-sans-pro-v14-latin-regular.woff') format('woff');
  }

  :root {
    font-family: 'Source Sans Pro', sans-serif;
    font-size: 16px;
    color: #000000;
    background: #ffffff;
;
    margin: 0 15px;
  }

  .app {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;
    width: 100%;
    user-select: none;
  }

  .selector {
    width: 200px;
    margin-bottom: 10px;
    --border: 2px solid #bdc3c7;
    --borderFocusColor: #4cc9f0;
    --borderHoverColor: #4cc9f0;
    --borderRadius: 2px;
    --clearSelectColor: #bdc3c7;
    --clearSelectFocusColor: #4cc9f0;
    --clearSelectHoverColor: #4cc9f0;
    --inputColor: #282828;
    --inputFontSize: 16px;
    --itemColor: #282828;
    --itemIsActiveBG: #4cc9f0;
    --itemIsActiveColor: #ffffff;
    --itemHoverBG: rgb(76, 201, 240, 0.3);
    --listBorderRadius: 2px;
    --placeholderColor: #282828;
  }

</style>
