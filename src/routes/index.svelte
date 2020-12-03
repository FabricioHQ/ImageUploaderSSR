<script>
import { goto } from '@sapper/app';

  let files;
  $: if(files && files[0]){
		let reader = new FileReader();
			reader.onload = function(e) {
				url = e.target.result
		}
		reader.readAsDataURL(files[0]);
  }
  let username;
  let url = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAAADhCAMAAAAJbSJIAAAAM1BMVEXFxcX////CwsL8/PzHx8fc3NzT09PJycn39/fMzMzs7Oz19fXZ2dnk5OTf39/v7+/o6OgDKYFyAAAE00lEQVR4nO2dx5qrMAxGQfTO+z/tjSFMGgnFEvrh6qxmMQvOZ1lyTxAYhmEYhmEYhmEYhmEYhmEYhmEYhmEYhmEYhmEYhmEYhiEBET3/TT/+9Xw4nbRN2nCiS9okiIOLWFIQ122eR+Ebed4nxfmbkiiu+w+5P6IqKU7dkk4v/6p3l+xuLan9oTuhLFnSu0uW53SM23V+g2NfaH/uZihd7zc4Nufqj1SUm/wcea391Vuov6fPH5TZSZqRsn6Pn2vGVPvbV7G1Bz4T9dpfvwJKd0XoRA8fqJT6+A2K4I7bc+g7OXZp3JtjnomAFb1DdAS3L3ommRMo8rSgo9RWmSdmakFHjdiKWccnCDm6oXb5uzdQaft8wpVlJuCyDXHG6ABYVWSqhM+A5dN4/3ziKwlSnDKnmZE809Z6ImNOMyOtttYDaiQEwwqnEWWa8NYTtcUmKJERDDttsz/Ya+EdmJliJlAqRkCWUKmWEgw7kJIoFaQhytBNLkhBwlQwSCHCNA4CiRHbRBVrCzoqQcMQYq4vmGhuhgBhKtkNbx1Rf2wqbAgw+pY21E81KcdWxXfyRFuR/DebFtAOU3nD67ehGZqhGZqhGfqjXQ+DTGopcaTSX8ewkfcFDAvBhagwbLQTjeP6qxiyhvqrGJdfTRQ2LBEMRfbwJyC6YRDI7AA7QLby/4O9J7kwBQlSnpPBc8AciBYLU6BjUUJhChOkUo2IkmcGREZuEBvAd0QaEec0jYMEGhGnFw7wH/yCOnwZCBzey7WNPuCe6qM1IXuywZg2vcF56gRg+34OxnyKsHgxQ8ymCHkpyMGlCCvIVRXx0ugTHJsYHcIi8Feo9i6LPbSge27Asy8C98EJv3RzAkGvq5b5KQQ9BnAl+msDD4o9kRrBXJFZQ1xvdYwalKXDlVC8bRG1Ah2J/oKycvUI5+Z3NkGiIi2rtYZR1abZmRwpKPrNFSPv2pO8wHfTa/bW/K7FfymKKPUbtZUxtCPFrf/0Ka9hX26jdOUrgktUNeQrg1Qw7iJGLVywUvbjDc895AlYrDb8t7mR5hlUyFzuakBqB2sHfCVqELojw8rMDzr9rBrLHRcaiLQ3gmUPlw6UmlsYIo+2fBDpRerud0o3kqs94yJ6AfiFRqMV2Z4QXIXCIcVjBRWOuB0t6K4lHBqpJDAOXVQ8cpxKByXRN45bcBR6+ApI8ZA6P0d0jKLYu1coiqLXK1YoHmAoP9b+xQGPfh43VJunFVaMxS/FLiK7y6iZZSZEn6mjAya8y0geWyyOH6vNIXcNQ20s845YVVSthM9EQrPFWLtQPJCZ8x+z7LQSkTg9fM77C4lr+vIPYGxCYGiTaTu9wn8dQ/I68y64iyLCcO0V7sEb3zF8NhpWQd1p7zzMK6g4xf4B526GwG87MMC60o/YhKz3MiCb8NaIbPcW+H9hhQm2HXDAUjHCNsUALBUjXPNE2CBlyzUQy0/zMP3uFWgmdUQ82RQ3SJlyza77L0fBMocCDlKmbApbKxwss0TkbsjTES9vCN0NWTri9Q2xg5RjuQa5Gjq8OyLwsHvE2xBkU/Q73jsY4ImGoeaboTq+hgXStugsUeKliLchM4PXUoYZQmCGZoiPGZohPmZohvj4bUBl0OvBjij1nAJffvZkhvosGv4DMjNa45M9cp4AAAAASUVORK5CYII=";

  const SignUp = async () => {
      const response = await fetch(`https://imageuploader-server.herokuapp.com/api/auth/signup`, {
        method: "POST",
        headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
        body: JSON.stringify({ username })
      });
      console.log("asd")
      return await response.json();
  };
  const SignUpImg = async () => {
    const respose2 = await SignUp();
    console.log(respose2);
    const formData = new FormData();
    formData.append("image", files[0]);
    const response = await fetch(`https://imageuploader-server.herokuapp.com/api/auth/signup/img`, {
      method: "POST",
      headers: {
        "id": respose2.savedUser._id
      },
      body: formData
    });

    const data = await response.json();
    await goto(`/${data._id}`).then(()=> {
        location.reload();
    });
  };
  
</script>

<style>
  main{
    width: 100%;
    height: 100vh;
    background-color: #f0f2f5;
    display: grid;
    place-items: center;
  }
  .container{
    width: 30%;
    min-width: 360px;
  }
  .img-form{
    width: 100%;
    max-width: 360px;
  }
  .form{
    width: 100%;
    margin-bottom: 1rem;
    background-color: #fff;
    border: 1px solid rgba(26, 26, 26, .15);
    border-radius: 16px;
    box-shadow: var(--box-shadow);
    display: flex;
    flex-direction: column;
  }
  .form-logo{
    width: 100%;
    display: flex;
    justify-content: center;
    margin: 1.5rem 0 .75rem 0;
  }
  .form-logo img{
    width: 4rem;
    height: 4rem;
  }
  .form-text{
    width: 70%;
    font-family: Sansita, sans-serif;
    align-self: center;
    text-align: center;
    margin-bottom: 1rem;
  }
  ._line{
    width: 50%;
    height: 1px;
    border-radius: 1px;
    background-color: rgba(26, 26, 26, .5);
    align-self: center;
    margin-bottom: 1.5rem;
  }
  .form-input{
    width: 100%;
    margin-bottom: 1.25rem;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .form-input-2{
    width: 100%;
    margin-bottom: 1rem;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  input[type="file"]{
    width: 0.1px;
    height: 0.1px;
    opacity: 0;
    overflow: hidden;
    position: absolute;
    z-index: -1;
  }
  input[type="text"]{
    width: 80%;
    height: 2.25rem;
    border: 1px solid rgba(26, 26, 26, .4);
    border-radius: 1rem;
    padding: 0 1rem;
    font-family: Sansita;
  }
  input[type="text"]:focus{
    outline: none;
  }
  .img-user-border{
    width: 145px;
    height: 145px;
    border-radius: 50%;
    border: 2px solid var(--color-primary);
    display: grid;
    place-items: center;
  }
  label[for="img-user"]{
    width: 125px;
    height: 125px;
    border-radius: 50%;
    
    background-size: cover;
    background-position: center;
    object-fit: cover;
    display: inline-block;
    transition: .3s;
  }
  label[for="img-user"]:hover{
    filter: grayscale(50%);
    cursor: pointer;
    transition: .3s;
  }
  .user-username{
    display: flex;
    justify-content: center;
    margin: .75rem 0 1rem 0;
  }
  .user-username span{
    font-family: Sansita, sans-serif;
    font-size: 18px;
    color: var(--color-black);
  }
  input[type="submit"]{
    font-family: Sansita, sans-serif;
    font-size: 14px;
    width: 30%;
    height: 2rem;
    border-radius: 1rem;
    border: none;
    background-color: var(--color-primary);
    color: #fff;
    transition: .25s;
  }

  input[type="submit"]:hover{
    filter: brightness(1.1);
    transition: .25s;
    cursor: pointer;
  }
  input[type="submit"]:focus{
    outline: none;
  }
  .text-form-user{
    display: flex;
    justify-content: center;
    margin: 1rem 0 1rem 0;
  }
  .text-form-user span{
    font-family: Sansita, sans-serif;
    font-size: 18px;
    color: var(--color-black);
  }
</style>

<svelte:head>
  <link href="https://fonts.googleapis.com/css2?family=Kameron:wght@400;700&family=Sansita:ital,wght@0,400;0,700;1,400;1,700&display=swap" rel="stylesheet">
	<title>Image Uploader</title>
</svelte:head>

<main>
  <div class="container">
    <div class="img-form">
      <div class="form">
        <div class="form-data-user">
          <div class="text-form-user">
            <span>Ingrese su Usuario, por favor:</span>
          </div>
            <div class="form-input-2">
                <input type="text" bind:value="{username}">
              </div>
        </div>
      </div>
    </div>
    <div class="img-form">
      <div class="form">
        <div class="form-logo">
          <img src="./logo.svg" alt="logo">
        </div>
        <div class="form-text">
          <p>Seleccione su Imagen.</p>
        </div>
        <div class="_line"></div>
        <div class="form-data">
          <form on:submit|preventDefault="{SignUpImg}" method="post" enctype="multipart/form-data">
            <div class="form-input">
              <input type="file" id="img-user" name="image" bind:files >
              <div class="img-user-border">
                <label for="img-user" style="background-image: url({url});"></label>
              </div>
            </div>
            <div class="user-username">
              <span>{username}</span>
            </div>
            <div class="form-input">
              <input type="submit" value="Subir">
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</main>

