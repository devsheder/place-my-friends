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
  let guestsTables = [[]];

  /**
   * Shuffle the array in a new array
   * @param {string[]} array of strings
   * @returns {string[]}
   */
  const shuffleGuests = (array) => {
    const copy = array.slice();
    copy.sort(() => Math.random() - 0.5);
    return copy;
  };

  /**
   * Create tables and place guests on it
   * @param {string[]} guests array of guest
   * @param {string[]} tableCount number total of expected tables
   * @returns {array[{string[]}]}
   */
  const getGuestsTables = (guests, tableCount) => {
    let guestsCopy = guests.slice();
    const guestsCount = guestsCopy.length;
    // number of expected tables great than number of guests (=> 1 guest / table)
    const tableSize =
      guestsCount > tableCount ? Math.trunc(guestsCount / tableCount) : 1;
    // check if there will be different number of guests on tables
    const otherGuestsCount = guestsCount % tableCount;
    let otherGuestsTable = [];

    // he can not have same number of guests on each table
    if (otherGuestsCount > 0 && otherGuestsCount !== guestsCount) {
      otherGuestsTable = guestsCopy.slice(guestsCopy.length - otherGuestsCount);
      guestsCopy.splice(guestsCopy.length - otherGuestsCount);
    }

    // let's fill tables with same number of guests
    const tables = [];
    for (let index = 0; index < guestsCopy.length; index += tableSize) {
      const table = guestsCopy.slice(index, index + tableSize);
      tables.push(table);
    }

    // let's dispatch other guests, one guest per table
    otherGuestsTable.forEach((element, index) => {
      tables[index].push(element);
    });

    return tables;
  };

  /**
   * Shuffled guests array
   */
  const onGenerateGuestsTables = () => {
    const shuffled = shuffleGuests(guests);
    guestsTables = getGuestsTables(shuffled, parseInt(tableCount));
  };

  /**
   * Shuffled guests array
   */
  const onClearGuestsTables = () => (guestsTables = [[]]);

  /**
   * Add a new guest on guests array
   */
  const onAddGuest = () => {
    if (!!newGuest && newGuest.trim() !== "") {
      guests = [...guests, newGuest];
      newGuest = "";
    }
  };

  /**
   * Remove a guest from guests array
   */
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
      <IconButton on:click={onAddGuest}>
        <Icon class="material-icons">add</Icon>
      </IconButton>
    </li>
  </ul>

  <Button on:click={onGenerateGuestsTables}>
    <Label>Go !</Label>
  </Button>

  <Button on:click={onClearGuestsTables}>
    <Label>Tout le monde dehors</Label>
  </Button>

  <ul>
    {#each guestsTables as table, i}
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
