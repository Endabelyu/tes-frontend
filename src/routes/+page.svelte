<script>
// @ts-nocheck

import { goto } from '$app/navigation';
import Swal from 'sweetalert2';
import { onMount } from 'svelte';

let results= '';
    let unRegister = false,
    username='',
    profile= '',
    password='',
	 url_api = import.meta.env.VITE_API_DIGITAL,
   tokens= '';

   onMount(async () => {
   tokens= localStorage.getItem('token')

   })


   if(tokens){
    goto('/dashboard')
   }

    const register = () => {
		fetch(`${url_api}/auth/register`, {
			method: 'POST',
			body: JSON.stringify({
				password: password,
				profileName: profile,
				username: username
			}),
			headers: {
				'Content-Type': 'application/json'
			}
		})
			.then(async (response) => {
				if (response.status === 200) {
          await Swal.fire({
						imageUrl: '/alertsucc.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Success!',
						text: 'Successfully logged in',
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
				}
        location.reload()
			})
			.catch(async(error) => {
				console.log(error);
        await Swal.fire({
						imageUrl: '/alertfail.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Failed!',
						text: 'Incorrect password, please login again'
					});
			});
	};
    const login = () => {
		fetch(`${url_api}/auth/login`, {
			method: 'POST',
			body: JSON.stringify({
				password: password,
				username: username
			}),
			headers: {
				'Content-Type': 'application/json'
			}
		})
			.then(async (response) => {
				if (response.status === 200) {
          const result = await response.json()
          localStorage.setItem('token', result.data.token);
          localStorage.setItem('username', result.data.username);
          await Swal.fire({
						imageUrl: '/alertsucc.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Success!',
						text: 'Successfully logged in',
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
				}
        goto('/dashboard')
			})
			.catch(async(error) => {
				console.log(error);
        await Swal.fire({
						imageUrl: '/alertfail.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Failed!',
						text: 'Incorrect password, please login again'
					});
			});
	};
</script>


<div class='flex h-[95vh] pt-[10rem] mb-'>
    <div class="w-1/2 mx-auto">
        <img src="/logo1.png" alt="" class="mx-auto">
        <div class="mx-auto text-center text-blue-400">

            <h1 class="text-4xl font-bold">Selamat Datang </h1>
            <p class="font-bold">MARKETPLACE Sinau Koding</p>
        </div>
    </div>

    {#if unRegister}
         <!-- content here -->
         <div class="w-1/2 mt-[3rem]">
          <form on:submit|preventDefault={register}>
            <div class="w-4/5 ">
              
             <div class="bg-sky-200 text-center w-full rounded-t-lg text-blue-400 py-3"><h5 class="text-xl">Register</h5></div>
             <div class="border bg-white  rounded-b-lg p-4">
                <div class="form-control rounded">
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label class="label">
                      <span class="label-text">Username</span>
                    </label>
                    <label class="input-group input-group-vertical">
                      <input type="text" placeholder="Input username" class="input input-bordered bg-white border-2 h-10" bind:value={username} />
                    </label>
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label class="label">
                      <span class="label-text">
                        Profile Name
                      </span>
                    </label>
                    <label class="input-group input-group-vertical">
                      <input type="text" placeholder="Input profile name" class="input input-bordered bg-white border-2 h-10" bind:value={profile} />
                    </label>
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label class="label">
                      <span class="label-text">
                        Password
                      </span>
                    </label>
                    <label class="input-group input-group-vertical">
                      <input type="password" placeholder="Input password" class="input input-bordered bg-white border-2 h-10" bind:value={password} />
                    </label>
                    <button class="btn btn-info mx-auto text-white bg-sky-700 mt-4" on:click={register}>Daftar</button>
                    <a href="#" class="text-blue-400 link text-center" on:click={() => unRegister = false}>Sudah punya akun</a>
                  </div>
             </div>
        </div>
          </form>
        </div>
        {:else}
        <div class="w-1/2 mt-[3rem]">
          <form on:submit|preventDefault={login}>

            <div class="w-4/5 ">
    
             <div class="bg-sky-200 text-center w-full rounded-t-lg text-blue-400 py-3"><h5 class="text-xl">Login</h5></div>
             <div class="border bg-white  rounded-b-lg p-4">
                <div class="form-control rounded">
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label class="label">
                      <span class="label-text">Username</span>
                    </label>
                    <label class="input-group input-group-vertical">
                      <input type="text" placeholder="Input username" class="input input-bordered bg-white border-2 h-10" bind:value={username} />
                    </label>
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                    <label class="label">
                      <span class="label-text">
                        Password
                      </span>
                    </label>
                    <label class="input-group input-group-vertical">
                      <input type="password" placeholder="Input password" class="input input-bordered bg-white border-2 h-10" bind:value={password} />
                    </label>
                    <button class="btn btn-info mx-auto text-white bg-sky-700 mt-4">Masuk</button>
                    <a href="#" class="text-blue-400 link text-center" on:click={() => unRegister = true}>Belum punya akun</a>
                  </div>
             </div>
        </div>
          </form>
        </div>
        {/if}
    
   
</div>