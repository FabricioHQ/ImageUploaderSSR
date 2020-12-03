<script context="module">
	export async function preload(page) {
    let id = page.params;
    console.log(id.id)
		const response = await this.fetch(`https://imageuploader-server.herokuapp.com/api/auth/user/id/${id.id}`);
    const userData = await response.json();
    if (userData.message) {
      this.error(404, 'Not found');
    } else {
      return { user : userData };
    }
	}
</script>
<script>
  export let user;
</script>
<style>
    .containe{
        width: 100%;
        height: 100vh;
        background-color: #f0f2f5;
        display: grid;
        place-items: center;
    }
    .User{
        width: 40%;
        min-width: 360px;
        padding: 2rem 3rem;
        background: #fff;
        display: flex;
        flex-direction: column;
        align-items: center;
        box-shadow: var(--box-shadow);
        border-radius: 1rem;
    }
    .img{
        width: 11.5rem;
        height: 11.5rem;
        display: grid;
        place-items: center;
        border: 3px solid var(--color-primary);
        border-radius: 50%;
        margin-bottom: 1.25rem;
    }
    img{
        width: 10rem;
        height: 10rem;
        object-fit: cover;
        border-radius: 50%;
    }
    span{
        font-family: Sansita;
        font-size: 1.5rem;
    }
</style>
<svelte:head>
    <title>{user.username.slice(1, user.username.length)}</title>
</svelte:head>


<div class="containe">
  <div class="User">
    <div class="img">
      <img src="{user.pathImage}" alt="User Foto" />
    </div>
    <span>{user.username}</span>
  </div>
</div>