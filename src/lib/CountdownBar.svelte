<script lang="ts">
  import type { CoundownTriggers } from "$lib/types.ts";
  // type CoundownTriggers={start:boolean, pause:boolean, reset:boolean};

  interface P{
    triggers:CoundownTriggers,
    times:{duration:number, remaining:number},
    end:boolean
  }

  let {triggers=$bindable(), times=$bindable(), end=$bindable()}:P = $props();

  let progress:number = $state(100);
  let intervalId:number=0;

  function start() {
    // Si un interval était déjà en cours : évite les doublons
    reset();
    // Lance l'interval
    intervalId = setInterval(() => {
      if (progress > 0) {
        progress -= 1;
        times["remaining"] -= times["duration"]/100;
      } else {
        pause();
        end=true;
      }
    }, times["duration"]/100);
  }

  function pause() {
    clearInterval(intervalId);
    intervalId = 0;
  }
  
  function reset() {
    progress = 100;
    times["remaining"] = times["duration"];
    end=false;
    clearInterval(intervalId);
    intervalId = 0;
  }

  // Réagir aux changements des props
  $effect(()=>{
    if (triggers["start"]) {
      console.log("start");
      start();
      triggers["start"] = false;
    }
  });
  $effect(()=>{
    if (triggers["pause"]) {
      pause();
      triggers["pause"] = false;
    }
  });
  $effect(()=>{
    if (triggers["reset"]) {
      reset();
      triggers["reset"] = false;
    }
  });
</script>


<div class="container">
  <div class="progress-bar" style="width: {progress}%"></div>
</div>

<style>
  .container{
    width:100%;
    margin:0;
    padding:0;
  }
  .progress-bar{
    width: 100%;
    height: 10px;
    background-color: lightcoral;
    transition: width 0.03s linear;
  }
</style>