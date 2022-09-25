<script>
  import Select, { Option } from '@smui/select';
  import Textfield from '@smui/textfield';
  import Icon from '@smui/select/icon';
  import UB from "$lib/data/UB.json";
  import {isMobile} from "$lib/store/store.js"

  let days = ["Mandag", "Tirsdag", "Onsdag", "Torsdag", "Fredag", "Lørdag", "Søndag"];
  let times= ["00:00", "01:00", "02:00", "03:00", "04:00", "05:00", "06:00", "07:00", "08:00", "09:00", "10:00", "11:00", "12:00", "13:00", "14:00", "15:00", "16:00", "17:00", "18:00", "19:00", "20:00", "21:00", "22:00", "23:00"];
  let day = "Monday";
  let startTime = "16:00";
  let endTime = "23:00";
  let hourWage = 166;
  let money = 0;

  let upgrade = 0 //-1: salary went down, 0: salary stayed the same, 1: salary went up

  $: if ((times.includes(startTime)) && (times.includes(endTime)) && (days.includes(day)) && !isNaN(hourWage)){
    console.log("Hour wage: " + hourWage)


    //Find the additions for the chosen day
    let additonsArr = find_day_additions()
    
    //Index of the chosen start time
    let timeIndex = times.indexOf(startTime)

    let startAddition = 0;
    let i = 0;

    //find out wich addition the shift start with
    while (timeIndex > times.indexOf(additonsArr[i].time)){
      startAddition = additonsArr[i].addition
      if (i == additonsArr.length - 1) {
        break;
      }
      i++;
    }

    let time = times[timeIndex]
    let j = timeIndex
    let newMoney = 0;
    //Calculates the salary from start time to end time:
    while (endTime != time) {
      //Check if a new hour addition is being active
      additonsArr.forEach((timeObj) => {
        if (timeObj.time == time){
          startAddition = timeObj.addition
          console.log("new addition: " + startAddition)
        }
      })
      console.log(hourWage)
      newMoney += (Number(startAddition) + Number(hourWage))
      console.log(newMoney)
      
      j++
      if (j == times.length) {
        //Start from the start of the array again
        j = 0;
      } 
      //Next index
      time = times[j]
    }
 
    animateValue("money", money, newMoney, 500);
    money = newMoney

  }

  function find_day_additions(){
    if (day == "Søndag"){
      return UB.Sunday
    } else if (day == "Lørdag"){
      return UB.Saturday
    } else {
      //Weekday
      return UB.Weekday
    }
  }

/**
	 * @param {string} id
	 * @param {number} start
	 * @param {number} end
	 * @param {number} duration
	 */
function animateValue(id, start, end, duration) {
    // assumes integer values for start and end
    
    var obj = document.getElementById(id);
    if (obj == null) {
      return;
    }
    if (start < end){
        obj.style.color = "lightgreen"
        upgrade = 1
        console.log("Green")
      } else if (start > end){
        console.log("Red")
        obj.style.color = "red"
        upgrade = -1
      } else {
        console.log("whitesmoke")
        obj.style.color = "whitesmoke"
        upgrade = 0
      }

    var range = end - start;
    // no timer shorter than 50ms (not really visible any way)
    var minTimer = 50;
    // calc step time to show all interediate values
    var stepTime = Math.abs(Math.floor(duration / range));
    
    // never go below minTimer
    stepTime = Math.max(stepTime, minTimer);
    
    // get current time and calculate desired end time
    var startTime = new Date().getTime();
    var endTime = startTime + duration;
    /**
	 * @type {string | number | NodeJS.Timer | undefined}
	 */
    var timer;
  
    function run() {
        var now = new Date().getTime();
        var remaining = Math.max((endTime - now) / duration, 0);
        var value = Math.round(end - (remaining * range));
        if (obj != null){
          obj.innerHTML = value.toString();
        }
        if (value == end) {
            clearInterval(timer);
        }
    }
    
    timer = setInterval(run, stepTime);
    run();
}



</script>

<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@48,400,0,0" />

<div class="main">


  <Select class="shaped-outlined" variant="outlined" bind:value={day} label="Dag">
    <Icon class="material-icons" slot="leadingIcon">event</Icon>
    
    {#each days as day}
    <Option value={day}>{day}</Option>
    {/each}
  </Select>
  
  <!-- <h2> Klokkeslett: </h2> -->
  <div class = "clocking">
    <Select class="shaped-outlined" variant="outlined" bind:value={startTime} label="Begynner">
        <Icon class="material-icons" slot="leadingIcon">schedule</Icon>
        
        {#each times as time}
          <Option value={time}>{time}</Option>
        {/each}
    </Select>
    {#if !($isMobile)}
      <p style = "margin-left: 10px; margin-right: 10px"><span class="material-symbols-outlined">
        <span class="material-symbols-outlined">
          trending_flat
          </span>
        </span>
      </p>
    {/if}

    <Select class="shaped-outlined" variant="outlined" bind:value={endTime} label="Slutter">
        <Icon class="material-icons" slot="leadingIcon">schedule</Icon>
    
        {#each times as time}
          <Option value={time}>{time}</Option>
        {/each}
    </Select>
  </div>

  <Textfield
  bind:value={hourWage}
  label="Timeslønn"
  type="number"
  suffix="KR"

/>

  <div class="money">

    {#if upgrade == 1}
      <Icon class="material-icons" slot="leadingIcon" style="color: lightgreen; margin-right: 10px; font-size: 30px">trending_up</Icon>
    {:else if upgrade == -1}
      <Icon class="material-icons" slot="leadingIcon" style="color: red; margin-right: 10px; font-size: 30px">trending_down</Icon>
    {:else} 
      <Icon class="material-icons" slot="leadingIcon" style="color: whitesmoke; margin-right: 10px; font-size: 30px">trending_flat</Icon>
    {/if}

    <p id = "money">{money} </p>

    <p class = "money-currency">KR</p>
  </div>
</div>

  <style>
    .main{
      display: flex;
      flex-direction: column;
    }
    .clocking{
      display: flex;
      flex-direction: row;
      margin: 20px;
    }
    #money{
      margin-right: 10px;
      font-size: 40px;

    }
    .money-currency { 
      font-size: 20px;
      /* font-weight: bold; */
    }
    .money{
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      margin-top: 50px;
      
    }
    * :global(.shaped-outlined), * :global(.shaped-outlined .mdc-select__anchor) {
        border-radius: 28px;
    }
    * :global(.shaped-outlined .mdc-text-field__input) {
      padding-left: 32px;
      padding-right: 0;
    }
    * :global(.shaped-outlined
        .mdc-notched-outline
        .mdc-notched-outline__leading) {
      border-radius: 28px 0 0 28px;
      width: 28px;
    }
    * :global(.shaped-outlined
        .mdc-notched-outline
        .mdc-notched-outline__trailing) {
      border-radius: 0 28px 28px 0;
    }
    * :global(.shaped-outlined .mdc-notched-outline .mdc-notched-outline__notch) {
      max-width: calc(100% - 28px * 2);
    }
    * :global(.shaped-outlined.mdc-select--with-leading-icon
      .mdc-notched-outline:not(.mdc-notched-outline--notched)
      .mdc-floating-label) {
      left: 16px;
    }
    </style>