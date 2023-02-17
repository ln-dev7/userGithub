<script>
  import { onMount } from "svelte";

  let pseudo = "ln-dev7";

  let exist = true;

  let avatar;
  let name;
  let company;
  let login;
  let bio;
  let followers;
  let following;
  let repo;
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
    twitter = data.twitter_username;
    blog = data.blog;
    company = data.company;
  });

  async function search() {
    const url = `https://api.github.com/users/${pseudo}`;
    const reponse = await fetch(url);
    const data = await reponse.json();
    if (data.message == "Not Found") {
      exist = false;
    } else {
      exist = true;
      avatar = data.avatar_url;
      name = data.name;
      login = data.login;
      bio = data.bio;
      followers = data.followers;
      following = data.following;
      repo = data.public_repos;
      twitter = data.twitter_username;
      blog = data.blog;
      company = data.company;
    }
  }
</script>

<main class="main">
  <div class="main__container">
    <div class="main-header">
      <h1>
        Find a <a href="https://github.com/ln-dev7/userGithub">GitHub</a> profile
      </h1>
    <form on:submit|preventDefault={search}>
      <div class="main-header__search">
            <input type="text" placeholder="Entrez le pseudo" bind:value={pseudo} />
            <button on:click={search}> Search </button>
      </div>
    </form>
    </div>
    <div class="main-body">
      {#if exist}
        <div class="card">
          <div class="card-header">
            <div class="card-header__image">
              <img src={avatar} alt="avatar" />
            </div>
            <div class="card-header__text">
              {#if name}
                <h2>{name}</h2>
              {/if}
              <a class="text-pseudo" href={"https://github.com/" + login}>@{login}</a>
              {#if company}
                <a class="text-company" href={"https://github.com/" + company}>{company}</a>
              {/if}
            </div>
          </div>
          {#if bio}
            <div class="card-bio">
              <p>{bio}</p>
            </div>
          {/if}
          <div class="card-infos">
            <div class="card-infos__item">
              <p>Repos</p>
              <h3>{repo}</h3>
            </div>
            <div class="card-infos__item">
              <p>Followers</p>
              <h3>{followers}</h3>
            </div>
            <div class="card-infos__item">
              <p>Following</p>
              <h3>{following}</h3>
            </div>
          </div>
          <div class="card-other">
            {#if blog}
              <a href={"https://twitter.com/" + blog} class="card-other__item">
                <svg
                  width="35"
                  height="35"
                  fill="none"
                  stroke="#ffffff"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path d="M12 2a10 10 0 1 0 0 20 10 10 0 1 0 0-20z" />
                  <path d="M2 12h20" />
                  <path
                    d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"
                  />
                </svg>
                <span>Website</span>
              </a>
            {/if}
            {#if twitter}
              <a
                href={"https://twitter.com/" + twitter}
                class="card-other__item"
              >
                <svg
                  width="35"
                  height="35"
                  fill="none"
                  stroke="#ffffff"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5 0-.278-.028-.556-.08-.83A7.72 7.72 0 0 0 23 3Z"
                  />
                </svg>
                <span>@{twitter}</span>
              </a>
            {/if}
          </div>
        </div>
      {:else}
        <div class="main-body__notfound">
          <p>This user does not exist</p>
        </div>
      {/if}
    </div>
    <a class="main-coffee" href="https://buymeacoffee.com/lndev">
      <span>buy me a coffee</span></a
    >
  </div>
</main>

<style type="text/scss">
  .main {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    padding: 3rem 1rem 3rem 1rem;
    min-height: 100vh;
  }
  .main__container {
    width: 100%;
    max-width: 560px;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .main-header {
    width: 100%;
  }
  .main-header h1 {
    font-family: "Clash Display", sans-serif;
    font-size: 2.5rem;
    text-align: center;
    font-weight: 700;
    margin-bottom: 1rem;
    color: #fff;
  }
  .main-header h1 a {
    font-family: "Clash Display", sans-serif;
    font-size: inherit;
    font-weight: inherit;
    background: linear-gradient(90deg, #38bdf8 0%, #3b82f6 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  @media screen and (max-width: 768px) {
    .main-header h1 {
      font-size: 1.8rem;
    }
  }
  .main-header__search {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
  }
  .main-header__search input {
    width: 100%;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 700;
    color: #333;
    background: #fff;
    outline: none;
    transition: 0.3s ease;
  }
  .main-header__search input:focus {
    box-shadow: 0 0 0 3px #38bdf8, 0 0 0 3px #38bdf8;
  }
  .main-header__search button {
    width: 100%;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 0.5rem;
    font-size: 1rem;
    font-weight: 700;
    color: #fff;
    background: #38bdf8;
    outline: none;
    transition: 0.3s ease;
    cursor: pointer;
  }
  .main-header__search button:hover {
    opacity: 0.95;
  }
  .main-body {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    background: #334155;
    border-radius: 0.5rem;
    padding: 0.25rem;
  }
  .main-body .card {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    background: #1f2937;
    border-radius: 0.5rem;
    padding: 0.75rem;
  }
  .main-body .card-header {
    width: 100%;
    display: flex;
    align-items: flex-start;
    align-items: center;
    justify-content: center;
    gap: 1rem;
  }
  .main-body .card-header__image {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    overflow: hidden;
    border: 3px solid #38bdf8;
    flex-shrink: 0;
  }
  .main-body .card-header__image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .main-body .card-header__text {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
  }
  .main-body .card-header__text h2 {
    font-size: 1.5rem;
    font-weight: 700;
    color: #fff;
    font-family: "Clash Display", sans-serif;
  }
  .main-body .card-header__text .text-pseudo {
    color: #38bdf8;
    font-weight: 500;
  }
  .main-body .card-header__text .text-company {
    font-weight: 400;
    color: #fff;
    font-style: italic;
    opacity: 0.5;
  }
  .main-body .card-bio {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    gap: 1rem;
  }
  .main-body .card-bio p {
    font-size: 1.2rem;
    font-weight: 400;
    color: #fff;
    font-family: "Clash Display", sans-serif;
  }
  .main-body .card-infos {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
    grid-gap: 1rem;
  }
  @media screen and (max-width: 490px) {
    .main-body .card-infos {
      grid-template-columns: repeat(1, 1fr);
      grid-gap: 0.5rem;
      gap: 0.5rem;
    }
  }
  .main-body .card-infos__item {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column-reverse;
    gap: 0.25rem;
    padding: 1rem;
    border-radius: 0.5rem;
    background: #334155;
    transition: 0.3s ease;
  }
  .main-body .card-infos__item h3 {
    font-size: 1.2rem;
    font-weight: 700;
    color: #fff;
    font-family: "Clash Display", sans-serif;
  }
  .main-body .card-infos__item p {
    font-size: 1rem;
    font-weight: 700;
    color: #677a94;
  }
  .main-body .card-other {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
  }
  .main-body .card-other__item {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    gap: 0.5rem;
    padding: 1rem;
    border-radius: 0.5rem;
    background: #334155;
    border: 2px solid #38bdf8;
    transition: 0.3s ease;
  }
  .main-body .card-other__item:hover {
    background: #1f2937;
  }
  .main-body .card-other__item svg {
    width: 1.5rem;
    height: 1.5rem;
  }
  .main-body .card-other__item span {
    font-size: 1rem;
    font-weight: 600;
    color: #fff;
  }
  @media screen and (max-width: 490px) {
    .main-body .card-other__item span  {
      display: none;
    }
  }
  .main-body__notfound p {
    font-size: 1.2rem;
    font-weight: 700;
    color: #fff;
  }
  .main-coffee {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    border-radius: 0.5rem;
    padding: 0.5rem;
    background: linear-gradient(90deg, #ffdd00 0%, #ffdd00 50%, #ffdd00 100%);
  }
  .main-coffee span {
    font-size: 1.2rem;
    font-weight: 700;
    color: #000;
  }
</style>
