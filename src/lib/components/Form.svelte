<script>
  import Select, { Option } from '@smui/select';
  import Textfield from '@smui/textfield';
  import Icon from '@smui/select/icon';
  import UB from "$lib/data/UB.json";
  
  let days = ["Mandag", "Tirsdag", "Onsdag", "Torsdag", "Fredag", "Lørdag", "Søndag"];
  let times= ["00:00", "01:00", "02:00", "03:00", "04:00", "05:00", "06:00", "07:00", "08:00", "09:00", "10:00", "11:00", "12:00", "13:00", "14:00", "15:00", "16:00", "17:00", "18:00", "19:00", "20:00", "21:00", "22:00", "23:00"];
  let day = "";
  let startTime = "";
  let endTime = "";
  let hourWage = 0;
  let money = 0;

  $: if ((times.includes(startTime)) && (times.includes(endTime)) && (days.includes(day))){

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
    money = 0;
    //Calculates the salary from start time to end time:
    while (endTime != time) {
      //Check if a new hour addition is being active
      additonsArr.forEach((timeObj) => {
        if (timeObj.time == time){
          startAddition = timeObj.addition
          console.log("new addition: " + startAddition)
        }
      })
      money += (startAddition + Number(hourWage))
      console.log(money)
      
      j++
      if (j == times.length) {
        //Start from the start of the array again
        j = 0;
      } 
      //Next index
      time = times[j]
    }

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

</script>

<div class="main">


  <Select class="shaped-outlined" variant="outlined" bind:value={day} label="Dag">
    <Icon class="material-icons" slot="leadingIcon">event</Icon>
    
    {#each days as day}
    <Option value={day}>{day}</Option>
    {/each}
  </Select>
  
  <!-- <h2> Klokkeslett: </h2> -->
  <div>
    <Select class="shaped-outlined" variant="outlined" bind:value={startTime} label="Begynner">
        <Icon class="material-icons" slot="leadingIcon">event</Icon>
        
        {#each times as time}
          <Option value={time}>{time}</Option>
        {/each}
    </Select>
    <Select class="shaped-outlined" variant="outlined" bind:value={endTime} label="Slutter">
        <Icon class="material-icons" slot="leadingIcon">event</Icon>
    
        {#each times as time}
          <Option value={time}>{time}</Option>
        {/each}
    </Select>
  </div>
  <Textfield
  bind:value={hourWage}
  label="Timeslønn"
  suffix="KR"
  input$pattern="\d+"
/>

  <div class="money">
    <p>{money} Kroner</p>
  </div>
</div>

  <style>
    .main{
      display: flex;
      flex-direction: column;
    }
    /* * :global(.shaped-outlined), * :global(.shaped-outlined .mdc-select__anchor) {
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
    } */
    </style>