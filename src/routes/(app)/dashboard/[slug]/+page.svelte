<script>
// @ts-nocheck

 import { goto } from '$app/navigation';
import Swal from 'sweetalert2';
import { onMount } from 'svelte';
import { page } from '$app/stores';


let id_supplier= $page.params.slug,
// @ts-ignore
dataSupplier= [],
dataSuppliers= [],
url_api = import.meta.env.VITE_API_DIGITAL,
harga='',
nama_barang='',
nama_supplier='',
stok='',
supplierId='',
supplier='',
tokens= '';


onMount(async () => {
    // @ts-ignore
await getItems()
await getSupplier()
  });

// get data suppliers
const getItems = async () => {
		fetch(`${url_api}/barang/find-by-id/${id_supplier}`, {
			method: 'GET',
			headers: {
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
        if (response.status === 200) {
          const res = await response.json()
          dataSupplier= res.data;
          console.log(dataSupplier);
          nama_barang =  dataSupplier.namaBarang;
          harga =  dataSupplier.harga;
          stok =  dataSupplier.stok;
          supplierId =  dataSupplier.supplier.id;
          console.log(supplierId)
				} else {
          await Swal.fire({
						html: `
				<div class="flex flex-col justify-center  h-full">
					<img src="/alertfail.svg" width="150" height="150" class="mx-auto"/>
					<h4 class="mb-0 mt-3 fw-semibold text-black">Oops!</h4>
					<p class="mb-0 mt-2 fw-medium text-black">An error occurred while get data</p>
				</div>
			`,
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
				}
			})
			.catch(async (error) => {
				console.log(error);
        
			});
	};

  // get suppliers
  const getSupplier = async () => {
		fetch(`${url_api}/supplier/find-all?limit=10&offset=1`, {
			method: 'GET',
			headers: {
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
        if (response.status === 200) {
          const res = await response.json()
          dataSuppliers= res.data
          console.log(dataSuppliers);
          // nama_supplier=  dataSupplier.namaSupplier
          // alamat=  dataSupplier.alamat
          // noTelp=  dataSupplier.noTelp
          // console.log(dataSupplier)
				} else {
          await Swal.fire({
						html: `
				<div class="flex flex-col justify-center  h-full">
					<img src="/alertfail.svg" width="150" height="150" class="mx-auto"/>
					<h4 class="mb-0 mt-3 fw-semibold text-black">Oops!</h4>
					<p class="mb-0 mt-2 fw-medium text-black">An error occurred while get data</p>
				</div>
			`,
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
				}
			})
			.catch(async (error) => {
				console.log(error);
        
			});
	};
// update data suppliers
const UpdateBarang = async () => {
		fetch(`${url_api}/barang/update/${id_supplier}`, {
			method: 'PUT',
      body: JSON.stringify({
				harga: harga,
        id:0,
				namaBarang: nama_barang,
				stok: stok,
        supplier: supplier
			}),
			headers: {
				'Content-Type': 'application/json',
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
				if (response.status === 200) {
          console.log(response)
        await Swal.fire({
						imageUrl: '/alertsucc.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Success!',
						text: 'Successfully update supplier',
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
          goto('/dashboard')
				} else {
          await Swal.fire({
						html: `
				<div class="flex flex-col justify-center  h-full">
					<img src="/alertfail.svg" width="150" height="150" class="mx-auto"/>
					<h4 class="mb-0 mt-3 fw-semibold text-black">Oops!</h4>
					<p class="mb-0 mt-2 fw-medium text-black">An error occurred while get data</p>
				</div>
			`,
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
				}
			})
			.catch(async (error) => {
				console.log(error);
        
			});
	};


  </script>
  
  
  <div class="flex h-[95vh] pt-[8rem] ">
   
          <div class="w-2/4  mx-auto px-2">
              <div class="w-4/5 mx-auto ">
      
               <div class="bg-sky-200  w-full rounded-t-lg text-blue-400 py-3 px-3"><h5 class="text-xl">Update Barang</h5></div>
               <div class="border bg-white  rounded-b-lg p-4">
                  <div class="form-control rounded">
          <form on:submit|preventDefault={UpdateBarang}>

                      <div class="flex gap-x-[4rem] mb-2">
                        <label for="nama_barang">Nama Barang</label>
                        <input type="text" bind:value={nama_barang} name="nama_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                      </div>
                      <div class="flex gap-x-[4rem] mb-2">
                        <label for="harga_barang">Harga Barang</label>
                        <input type="text" bind:value={harga} name="harga_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                      </div>
                      <div class="flex gap-x-[4.8rem] mb-2">
                        <label for="stok_barang">Stok Barang</label>
                        <input type="text"  bind:value={stok} name="stok_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                      </div>
                      <div class="flex gap-x-[6.4rem] mb-2">
                        <label for="stok_barang">Supplier</label>
													<select
														class="w-[65%] bg-white border-2 p-1 rounded border-gray-200"
														placeholder="Select Letter type"
														on:change={getSupplier}
														bind:value={supplierId}
													>
														{#each dataSuppliers as supplierId}
															<option value={supplierId.id}>{supplierId.namaSupplier}</option>
														{/each}
													</select>
                      </div>
                      
                    
                    <!-- svelte-ignore a11y-label-has-associated-control -->
                      
                    <div class="flex justify-between">
                      
                      <a class="btn btn-info  text-white bg-gray-500 mt-4" href="/dashboard">Kembali</a>
                      <button class="btn btn-info  text-white bg-sky-700 mt-4" >Update</button>
                    </div>
                    </form>  
  
                    </div>
               </div>
          </div>
      
          </div>
      
     
  </div>