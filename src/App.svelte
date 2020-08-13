<script>
  import TopAppBar, { Row, Section, Title } from "@smui/top-app-bar";
  import IconButton from "@smui/icon-button";
</script>

<style>
  @import "@material/typography/mdc-typography";

  .container {
    width: 100%;
    height: 100%;
  }
</style>

<div class="container">
  <TopAppBar variant="static" dense={false} color={'primary'}>
    <Row>
      <Section>
        <IconButton class="material-icons">menu</IconButton>
        <Title>Place My Friends</Title>
      </Section>
    </Row>
  </TopAppBar>
</div>
