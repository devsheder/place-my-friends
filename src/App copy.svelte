<script>
  import TopAppBar, { Row, Section, Title } from "@smui/top-app-bar";
  import IconButton from "@smui/icon-button";
  import { table } from "console";

  let guests = [
    "Adrien",
    "Marine",
    "Emilie",
    "Florent",
    "Anto",
    "Nathalie",
    "JP",
    "Yohan",
    "Anne-Laure",
    "Manu",
    "Violaine",
    "Bertrand",
    "Vincent & Anne-Laure",
  ];

  let tableCount = 2;

  //   let tables = [[]];

  //   const shuffleGuests = (array) => {
  //     const copy = array.slice();
  //     array.sort(() => Math.random() - 0.5);
  //     return copy;
  //   };

  //   const getTables = (guests) => {
  //     const tableSize = Math.trunc(guests.length / tableCount);
  //     const other = guests.length % tableCount;
  //     let lastTableSize = tableSize;
  //     if (other > 0) {
  //       lastTableSize = other;
  //     }
  //     console.log(lastTableSize);
  //     const tables = [];

  //     for (let index = 0; index < guests.length; index += tableSize) {
  //       const table = guests.slice(index, index + tableSize);
  //       tables.push(table);
  //     }

  //     return tables;
  //   };

  const generateTables = () => {
    // const shuffled = shuffleGuests(guests);
    // console.log(getTables(shuffled));
  };
</script>

<style>

</style>

<TopAppBar variant="static" dense={false} color={'primary'}>
  <Row>
    <Section>
      <IconButton class="material-icons">menu</IconButton>
      <Title>Place My Friends</Title>
    </Section>
  </Row>
</TopAppBar>
<div>
  <p>
    Nombre de tables :
    <input type="text" bind:value={tableCount} size="2" max="99" />
  </p>
  <p>Liste des invités :</p>
  {#each guests as guest, i}
    <ul>
      <input type="text" bind:value={guest} />
    </ul>
  {/each}
  <button on:click={generateTables}>Go !</button>
</div>
