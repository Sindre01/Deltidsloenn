<script lang="ts">
  import DataTable, { Head, Body, Row, Cell } from '@smui/data-table';
  export let calculationsObj = {hourWage: 0, timesAndAdditions: [["", 0]], sumSalary: 0, sumAdditions: 0}
</script>

<div class= "main">
  <div>
    <h2> Time for time utregning </h2>
  </div>
  <DataTable table$aria-label="People list" style="max-width: 100%;">
    <Head>
      <Row>
        <Cell>Time</Cell>
        <Cell numeric>lønn</Cell>
        <Cell numeric>Tillegg</Cell>
        <Cell numeric>Sum</Cell>
      </Row>
    </Head>

    <Body>
      {#each calculationsObj.timesAndAdditions as arr}
      <Row>
        <Cell>{arr[0]}</Cell>
        <Cell numeric>{calculationsObj.hourWage} </Cell>
        <Cell numeric>{arr[1]} </Cell>
        <Cell numeric>{Number(calculationsObj.hourWage) + Number(arr[1])} kr</Cell>
      </Row>
      {/each}

      <Row >
          <Cell style="color: red; border-top: 1px solid red; ">Totalt: </Cell>
          <Cell numeric style="border-top: 1px solid red; ">{calculationsObj.sumSalary} </Cell>
          <Cell numeric style="border-top: 1px solid red; ">{calculationsObj.sumAdditions} </Cell>
          <Cell numeric style="border-top: 1px solid red; ">{calculationsObj.sumSalary + calculationsObj.sumAdditions} kr</Cell>
      </Row> 
    </Body>
    
  </DataTable>
 
</div>

<style>
div{
  justify-content: center;
  align-items: center;
}

</style>