<script>
    import Textfield from '@smui/textfield';
	import axios from 'axios'

	let user = '';
	let pass = '';
	let err = '';
	async function sign() {
		if (user != '' && pass != ''){
			err = '';
			// console.log({
			// username: user,
			// password: pass
			// })

			try{
			const res = await axios({
				method: 'post',
				url: 'http://localhost:3000/api/auth',
				data: {
					username: user,
					password: pass
				}
			})
			console.log(res)
			localStorage.setItem('svelte', res.data)

			} catch(err){
				console.log(err)
			}
			// localStorage.setItem('svelte', )
		} else {
			err = 'You have made error, recheck';
		}
	}
</script>

<svelte:head>
	<title>Authorisation page</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="text-column">
	<h1>Lets sign token to start</h1>

		<div class="place-center">
			<div class="text-center">
				Username
			</div>
			<Textfield bind:value={user}></Textfield>
			<div class="text-center">
				Password
			</div>
			<Textfield bind:value={pass} type='password'></Textfield>
			<button on:click={sign} class="auth-button">sign</button>
			<!-- <pre class="status">Value: {user}</pre> -->
			{#if err.length > 0}
			<h3 style="color:red; text-align: center">
				{err}
			</h3>
			{/if}
	  </div>
</div>

<style>
.place-center{
	display: grid;
	place-items: center;
	margin: 0 auto;
	width: 200px;

}
.text-center{
	text-align: center;
	margin: 10px 0;
}
.auth-button{
	width: 80px;
	border: none;
	background: orange;
	border-radius: 10px;
	color: white;
	font-weight: 800;
	margin-top: 30px;
	cursor: pointer;
}
</style>