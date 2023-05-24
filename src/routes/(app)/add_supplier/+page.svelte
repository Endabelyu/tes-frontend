<script>
  import { goto } from '$app/navigation';
      let unRegister = false
      import Swal from 'sweetalert2';
import { onMount } from 'svelte';
let tokens='',
alamat='',
nama_supplier='',
noTelp='',
url_api = import.meta.env.VITE_API_DIGITAL

      onMount(async () => {
   // @ts-ignore
   tokens= localStorage.getItem('token')

   })

    const add_supplier = () => {
		fetch(`${url_api}/supplier/create`, {
			method: 'POST',
			body: JSON.stringify({
				alamat: alamat,
				namaSupplier: nama_supplier,
				noTelp: noTelp
			}),
			headers: {
				'Content-Type': 'application/json',
				Authorization: `Bearer ${localStorage.getItem('token')}`

			}
		})
			.then(async (response) => {
				if (response.status === 200) {
          const res= await response.json()
          console.log(res)
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
  
  
  <div class="flex h-[95vh] pt-[8rem] ">
   
          <div class="w-2/4  mx-auto px-2">
              <div class="w-4/5 mx-auto ">
      
               <div class="bg-sky-200  w-full rounded-t-lg text-blue-400 py-3 px-3"><h5 class="text-xl">Tambah Supplier</h5></div>
               <div class="border bg-white  rounded-b-lg p-4">
                  <div class="form-control rounded">
          <form on:submit|preventDefault={add_supplier}>
                    
                      <div class="flex gap-x-[4rem] mb-2">
                        <label for="nama_supplier">Nama Supplier</label>
                        <input type="text" placeholder="Masukan Nama supplier" name="nama_supplier" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200 " 
                        bind:value={nama_supplier}>
                      </div>
                      <div class="flex gap-x-[3.5rem] mb-2">
                        <label for="harga_supplier">Alamat Supplier</label>
                        <input type="text" placeholder="Masukan Alamat Supplier" name="harga_supplier" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200" bind:value={alamat}>
                      </div>
                      <div class="flex gap-x-[3.2rem] mb-2">
                        <label for="stok_supplier">No Telp Supplier</label>
                        <input type="text" placeholder="Masukan No Telp Supplier" name="stok_supplier" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200" bind:value={noTelp}>
                      </div>
                      
                    
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                      
                    <div class="flex justify-between">
                      
                      <a class="btn btn-info  text-white bg-gray-500 mt-4" href="/dashboard">Kembali</a>
                      <button class="btn btn-info  text-white bg-sky-700 mt-4" on:click={add_supplier}>Tambah</button>
                    </div>
                    </form>  
  
                    </div>
               </div>
          </div>
      
          </div>
      
     
  </div>