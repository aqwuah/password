<script>
  import Password from "./Password.svelte";
</script>

<style>
  main {
    display: flex;
    align-items: center;
	flex-direction: column;
	font-family: sofia-pro, sans-serif;
	text-align: center;
  }

  h1 {
    font-family: gothic-open-shaded, sans-serif;
    font-weight: 400;
    font-style: normal;
  }
</style>

<main>

  <h1>Password Strength Checker</h1>
  <p>Your passwords are <strong><u>never</u></strong> stored.</p>
  <Password />
</main>
