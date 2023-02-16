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
      console.log(data);
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
    <div class="head">
      <h1>Trouvez un profil GitHub</h1>

      <div class="search">
        <input type="text" placeholder="Entrez le pseudo" bind:value={pseudo} />
        <button on:click={search}>Rechercher</button>
      </div>
    </div>

    {#if exit}
      <div class="card">
        <div class="profile">
          <div>
            <h2>{name}</h2>
          </div>

          <img src={avatar} alt="profil avatar" />
          <div>
            <h3>@{login}</h3>
          </div>
        </div>

        <div>
          <p>{bio}</p>
          <div class="follo">
            <div>
              <h3>Repo</h3>
              <h2>{repo}</h2>
            </div>
            <div>
              <h3>Followers</h3>
              <h2>{followers}</h2>
            </div>
            <div>
              <h3>Following</h3>
              <h2>{following}</h2>
            </div>
          </div>
          <div class="infos">
            {#if local}
              <div class="flex">
                <img class="icons" src="./icons/map.svg" alt="localisation" />
                <h3>
                  {local}
                </h3>
              </div>
            {/if}

            {#if twitter}
              <div class="flex">
                <img
                  class="icons"
                  src="./icons/twitter.svg"
                  alt="localisation"
                />
                <h3>@{twitter}</h3>
              </div>
            {/if}

            {#if blog}
              <div class="flex">
                <img
                  class="icons"
                  src="./icons/browser.svg"
                  alt="localisation"
                />
                <h3>{blog}</h3>
              </div>
            {/if}
          </div>
        </div>
      </div>
    {:else}
      <h1>le profil "@{pseudo}" n'existe pas</h1>
    {/if}
  </div>
</div>

<style>
  :root {
    --primary-color: rgba(17, 179, 230, 0.61);
  }
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .flex {
    display: flex;
    align-items: center;
  }

  .head {
    padding: 40px;
    margin: 20px;
    background-color: white;
    border-radius: 15px;
    border: 2px solid rgba(17, 179, 230, 0.61);
  }

  .head input {
    width: 100%;
    height: 40px;
    border: 1px solid rgba(17, 179, 230, 0.61);
    border-radius: 15px;
    background-color: white;
    color: black;
  }

  .head button {
    width: 100%;
    height: 40px;
    border-radius: 15px;
    background-color: rgba(17, 179, 230, 0.61);
    color: black;
    cursor: pointer;
  }

  .card {
    display: flex;
    flex-direction: row;
    border: 2px solid var(--primary-color);
    border-radius: 15px;
    padding: 10px;
  }

  .profile {
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    align-items: center;
    margin: 10px;
    padding: 10px;
    border-right: 2px solid var(--primary-color);
  }
  .center {
    width: 80%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  .profile img {
    width: 75px;
    height: 75px;
    border-radius: 50%;
    border: 1px solid var(--primary-color);
    object-fit: cover;
  }
  .follo {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: center;
  }

  .icons {
    width: 25px;
    height: 25px;
    object-fit: cover;
    margin-right: 5px;
  }

  .follo div {
    border: 1px solid var(--primary-color);
    height: 100px;
    width: 100px;
    text-align: center;
    padding: 5px;
    border-radius: 15px;
  }

  .follo div h2 {
    color: var(--primary-color);
  }

  .infos {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin: 10px;
    padding: 10px;
  }

  p {
    text-align: center;
  }

  @media screen and (max-width: 459px) {
    .infos,
    .follo,
    .card {
      flex-direction: column;
    }
    .card .profile {
      flex-direction: row;
      border: none;
    }
    .card .profile img,
    .follo div {
      margin: 5px;
    }

    h1 {
      font-size: 1rem;
      text-align: center;
    }
  }
</style>
