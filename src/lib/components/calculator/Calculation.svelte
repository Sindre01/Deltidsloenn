<script lang="ts">
  import DataTable, { Head, Body, Row, Cell } from '@smui/data-table';
</script>

<div class= "main">
  <div>
    <h2> Utregning </h2>
  </div>
  <DataTable table$aria-label="People list" style="max-width: 100%;">
    <Head>
      <Row>
        <Cell>Kl</Cell>
        <Cell numeric>lønn</Cell>
     
        <Cell numeric>Tillegg</Cell>
    
        <Cell numeric>Sum</Cell>
      </Row>
    </Head>
    <Body>
      <Row>
        <Cell>16-17</Cell>
        <Cell>160 kr</Cell>
        <Cell numeric>45 kr</Cell>
        <Cell numeric>205 kr</Cell>
      </Row>
      <Row>
        <Cell>17-18</Cell>
        <Cell>160 kr</Cell>
        <Cell numeric>45 kr</Cell>
        <Cell numeric>205 kr</Cell>
      </Row>
      <Row >
          <Cell style="color: red;">Totalt: </Cell>
          <Cell>360 kr</Cell>
          <Cell>90 kr</Cell>
          <Cell>410 kr</Cell>
       

      </Row>
     
    
    
      
      
    </Body>
    
  </DataTable>
 
</div>

<style>
div{
  justify-content: center;
  align-items: center;
}
.tot{
  color: red;
  font-weight: bold
}

</style>