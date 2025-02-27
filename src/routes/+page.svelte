<script lang="ts">
  import CountdownBar from "$lib/CountdownBar.svelte";

  let CountdownBarData = $state({
    triggers:{start:false, pause:false, reset:false},
    times:{duration:3000, remaining:0},
    end:false
  });
</script>

<h2>Présentation des composants game-utils</h2>
<div class="container">
  <h3>CountdownBar</h3>
  <div class= CountdownBar>
    <CountdownBar bind:triggers={CountdownBarData["triggers"]} bind:times={CountdownBarData["times"]} bind:end={CountdownBarData["end"]}/>
    <div class="settings">
      <div><span class="settingTitle">Triggers :</span> 
        <div>
          <label for="start">Start Countdown</label>
          <input type="checkbox" name="start" bind:checked={CountdownBarData["triggers"]["start"]}>
        </div>
        <div>
          <label for="start">Pause Countdown</label>
          <input type="checkbox" name="start" bind:checked={CountdownBarData["triggers"]["pause"]}>
        </div>
        <div>
          <label for="start">Reset Countdown</label>
          <input type="checkbox" name="start" bind:checked={CountdownBarData["triggers"]["reset"]}>
        </div>
      </div>
      <div><span class="settingTitle">Times :</span>
        <div>
          <label for="duration">Duration</label>
          <input type="number" bind:value={CountdownBarData["times"]["duration"]}>
        </div>
        <div>
          <label for="remaining">Remaining</label>
          <input type="number" bind:value={CountdownBarData["times"]["remaining"]}>
        </div>
      </div>
      <div><span class="settingTitle">End :</span>
        <div>
          <input type="checkbox" name="start" checked={CountdownBarData["end"]} disabled>
        </div>
      </div>
    </div>
  </div>
  <h3>CountdownTime</h3>
  <div>WIP</div>
</div>

<style>
  .container{
    padding: 20px 2%;
    width: 96%;

    display:flex;
    flex-direction: column;
    justify-content: center;
  }
  .container > div{
    width: calc(100%-20px);
    padding: 5px 10px;
    display: grid;
    grid-template-columns: 3fr 1fr;
    align-items: center;
  }
  .container > div > .settings{
    display:flex;
    flex-direction: column;
    align-items:start;
    /* justify-content: center; */
    border: solid black 2px;
    padding: 5px 10px;
    margin-left:5px;

  }
  .settingTitle{
    font-weight:bold;
    text-decoration-line: underline;
  }
</style>