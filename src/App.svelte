<script>
  import TopAppBar, { Row, Section, Title } from "@smui/top-app-bar";
  import IconButton, { Icon } from "@smui/icon-button";
  import Button, { Label } from "@smui/button";

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
  let newGuest = "";
  let tableCount = 2;
  let tables = [[]];

  const shuffleGuests = (array) => {
    const copy = array.slice();
    array.sort(() => Math.random() - 0.5);
    return copy;
  };

  const getTables = (guests, tableCount) => {
    const guestsCount = guests.length;
    const tableSize = Math.trunc(guestsCount / tableCount);
    const other = guestsCount % tableCount;
    let lastTableSize = tableSize;
    if (other > 0) {
      lastTableSize = tableSize + other;
    }
    const tables = [];

    for (let index = 0; index < guestsCount; index += tableSize) {
      let maxSliceIndex = index + tableSize;
      if (maxSliceIndex + tableSize > guestsCount) {
        const table = guests.slice(index, index + lastTableSize);
        tables.push(table);
        break;
      } else {
        const table = guests.slice(index, maxSliceIndex);
        tables.push(table);
      }
      console.log(tables.length, tableCount);
      if (tables.length + 1 > tableCount) {
        break;
      }
    }

    console.log(tables);

    return tables;
  };

  const generateTables = () => {
    const shuffled = shuffleGuests(guests);
    tables = getTables(shuffled, parseInt(tableCount));
  };

  const clearTables = () => (tables = [[]]);

  const addGuest = () => {
    if (!!newGuest && newGuest.trim() !== "") {
      guests = [...guests, newGuest];
      newGuest = "";
    }
  };

  const removeGuest = (index) => {
    const copy = guests.slice();
    copy.splice(index, 1);
    guests = copy;
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
  <ul>
    {#each guests as guest, i}
      <li>
        <input type="text" bind:value={guest} />
        <IconButton on:click={() => removeGuest(i)}>
          <Icon class="material-icons">delete</Icon>
        </IconButton>
      </li>
    {/each}
    <li>
      <input type="text" bind:value={newGuest} />
      <IconButton on:click={addGuest}>
        <Icon class="material-icons">add</Icon>
      </IconButton>
    </li>
  </ul>

  <Button on:click={generateTables}>
    <Label>Go !</Label>
  </Button>

  <Button on:click={clearTables}>
    <Label>Tout le monde dehors</Label>
  </Button>

  <ul>
    {#each tables as table, i}
      {#if table.length > 0}
        <li>
          Table n°{i + 1} :
          <ul>
            {#each table as guest, j}
              <li>{guest}</li>
            {/each}
          </ul>
        </li>
      {/if}
    {/each}
  </ul>
</div>
