<script>
  import { onMount } from "svelte";

  let pseudo = "ln-dev7";

  let exit = true;

  let avatar;
  let name;
  let login;
  let bio;
  let followers;
  let following;
  let repo;
  let local;
  let twitter;
  let blog;

  onMount(async function () {
    const url = `https://api.github.com/users/${pseudo}`;
    const reponse = await fetch(url);
    const data = await reponse.json();
    avatar = data.avatar_url;
    name = data.name;
    login = data.login;
    bio = data.bio;
    followers = data.followers;
    following = data.following;
    repo = data.public_repos;
    local = data.location;
    twitter = data.twitter_username;
    blog = data.blog;
  });

  async function search() {
    const url = `https://api.github.com/users/${pseudo}`;
    const reponse = await fetch(url);
    const data = await reponse.json();
    if (data.message == "Not Found") {
      exit = false;
    } else {
		exit = true;
      avatar = data.avatar_url;
      name = data.name;
      login = data.login;
      bio = data.bio;
      followers = data.followers;
      following = data.following;
      repo = data.public_repos;
      local = data.location;
      twitter = data.twitter_username;
      blog = data.blog;
    }
  }
</script>

<div class="container">
  <div class="center">
    <h1>Trouvez un profil GitHub</h1>

    <div class="search">
      <input type="text" placeholder="Entrez le pseudo" bind:value={pseudo} />
      <button on:click={search}>Rechercher</button>
    </div>

    {#if exit}
      <div class="card">
        <img src={avatar} alt="photo" />
        <h2>{name}</h2>
        <h3>@{login}</h3>
        <p>{bio}</p>
        <div class="follo">
          <div>
            <h3>Repo</h3>
            <h3>{repo}</h3>
          </div>
          <div>
            <h3>Followers</h3>
            <h3>{followers}</h3>
          </div>
          <div>
            <h3>Following</h3>
            <h3>{following}</h3>
          </div>
        </div>
        <div>
          <h3>Localisation : {local}</h3>
        </div>
        <div>
          <h3>Twitter : @{twitter}</h3>
        </div>
        <div>
          <h3>Site web : {blog}</h3>
        </div>
      </div>
    {:else}
      <h1>le profil "@{pseudo}" n'existe pas</h1>
    {/if}
  </div>
</div>

<style>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .center {
    width: 80%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  img {
    width: 75px;
    height: 75px;
    border-radius: 50%;
    border: 1px solid #333;
    object-fit: cover;
  }
  .follo {
    background: #ccc;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
  }
</style>
