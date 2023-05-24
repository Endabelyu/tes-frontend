
<script>
// @ts-nocheck

  
  import { goto } from '$app/navigation';
	import { onMount } from 'svelte';
  import Swal from 'sweetalert2';


  let barang =true,
  currentdate = new Date(),
  dataBarang=[],
  dataSupplier=[],
  date= currentdate.getFullYear()+ "/" + (currentdate.getMonth()+1) + "/" +currentdate.getDate(),
  time = currentdate.getHours() + ":"  
                + currentdate.getMinutes() + ":" 
                + currentdate.getSeconds(),
   usersname= '';
                ;


onMount(async () => {
  await getData()  
  await getSupplier()
  usersname= localStorage.getItem('username');

})
let    url_api = import.meta.env.VITE_API_DIGITAL

// get all item data  
const getData = async () => {
		fetch(`${url_api}/barang/find-all?limit=10&offset=1`, {
			method: 'GET',
			headers: {
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
				console.log(response);
				if (response.status === 200) {
				const res = await response.json()
          dataBarang = res.data
          console.log(dataBarang)
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

  // get all data suppliers
const getSupplier = async () => {
		fetch(`${url_api}/supplier/find-all?limit=10&offset=1`, {
			method: 'GET',
			headers: {
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
				console.log(response);
				if (response.status === 200) {
				const res = await response.json()
          dataSupplier = res.data
          console.log(dataSupplier)
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

// delete Item

// let id_item = '';

const deleteItem = async (id) => {
		fetch(`${url_api}/barang/delete/${id}`, {
			method: 'DELETE',
			headers: {
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
				console.log(response);
				if (response.status === 200) {
				const res = await response.json()
        await Swal.fire({
						imageUrl: '/alertsucc.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Success!',
						text: 'Successfully deleted item',
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
          console.log(res)
          location.reload()
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
// delete supplier

// let id_item = '';

const deleteSupplier = async (id) => {
		fetch(`${url_api}/supplier/delete/${id}`, {
			method: 'DELETE',
			headers: {
				Authorization: `Bearer ${localStorage.getItem('token')}`
			}
		})
			.then(async (response) => {
				console.log(response);
				if (response.status === 200) {
				const res = await response.json()
        await Swal.fire({
						imageUrl: '/alertsucc.svg',
						imageHeight: 130,
						imageAlt: 'A tall image',
						title: 'Success!',
						text: 'Successfully deleted item',
						confirmButtonColor: '#596066',
						customClass: 'swal-height'
					});
          console.log(res)
          location.reload()
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

<div class="h-[85vh] flex gap-6  py-4 px-8">
    <div class="w-[15%]">
      <div class="mb-2 shadow-lg">
        <div class=" rounded-t-lg border-2 py-4 rounded border-gray-200 w-full ">
          <img src="/woman.png" alt="profile" class="w-2/4 mx-auto">
        </div>
        <div class="bg-blue-300  text-center rounded-b-md w-full px-3 py-3 text-blue-900">
          <h2>{usersname}</h2>
        </div>
      </div>
      <div class="shadow-lg">
        <div class="bg-blue-300  text-center rounded-t-lg w-full px-3 py-3 text-blue-900">
          <h2>Menu</h2>
        </div>
        <div class=" rounded-b-lg border-2 border-gray-200 w-full mb-2 ">
          <ul class=" list-container">
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li class="p-2" on:click={() => barang=true}>Barang</li>
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li class="p-2"  on:click={() => barang=false}>Supplier</li>
          </ul>
        </div>
      </div>
      <div class="shadow-lg">
        <div class="bg-blue-300  text-center rounded-t-lg w-full px-3 py-3 text-blue-900 flex justify-center">
          <h2>Online</h2>
          <span class="bg-green-500 w-2 h-2 rounded-full ml-2 mt-[10px] "></span>
        </div>
        <div class=" rounded-b-lg border-2  py-2 px-4 border-gray-200 w-full ">
          <div class="flex justify-between text-black">

            <p class="text-xs ">Hari Online</p>
            <span class="text-xs text-black">: {date}</span>
          </div>
          
          <div class=" flex  justify-between text-black">

            <p class="text-xs">Waktu Online</p>
            <span class="text-xs text-black mr-[10px]">: {time}</span>
          </div>

        </div>
        
      </div>
    
    </div>
    <div class="w-4/5">
        <div class="bg-blue-300 rounded-t-lg w-full p-3 text-blue-900">
            <h2>
                Dashboard
            </h2>
        </div>
{#if barang}
   <!-- content here -->
        <div class="border-2 rounded-b-lg px-2 py-4"> 
        <header class="flex justify-between gap-3 p-3  text-black mb-2">
                <h2 class="text-xl">Barang</h2>
                <button class=" w-[8rem] bg-blue-700 text-sm px-2 py-2 capitalize rounded text-white add" on:click={() => goto('/add_items')}>Tambah Barang</button>
        </header>
        <div class="overflow-x-auto">
            <table class="table w-full mb-4 shadow-md">
              <!-- head -->
              <thead class="">
                <tr>
                  <th>No</th>
                  <th>Nama Barang </th>
                  <th>Stok</th>
                  <th>Harga</th>
                  <th>Nama Supplier</th>
                  <th>Alamat Supplier</th>
                  <th>No Telp Supplier</th>
                  <th>Aksi</th>
                </tr>
              </thead>
              <tbody class="">
                <!-- row 1 -->

                {#each dataBarang as data,i}
                   <!-- content here -->
                <tr>
                  <td>{++i}</td>
                  <td>{data.namaBarang}</td>
                  <td>{data.stok}</td>
                  <td>{data.harga}</td>
                  <td>{data.supplier?.namaSupplier}</td>
                  <td>{data.supplier?.alamat}</td>
                  <td>{data.supplier?.noTelp}</td>
                  <td><button class="btn btn-error text-white" on:click={deleteItem(data.id)}>Hapus</button>
                    <button class="btn btn-warning " on:click={goto(`/dashboard/${data.id}`)}>Update</button></td>
                </tr>
                {/each}

            
              </tbody>
            </table>
            <div class="flex justify-end">

                <div class="btn-group ">
                    <button class="btn">1</button>
                    <button class="btn">2</button>
                    <button class="btn btn-disabled">...</button>
                    <button class="btn">99</button>
                    <button class="btn">100</button>
                </div>
            </div>
          </div>
        </div>

        {:else}

        <div class="border-2 rounded-b-lg px-2 py-4"> 
          <header class="flex justify-between gap-3 p-3  text-black mb-2">
                  <h2 class="text-xl">Supplier</h2>
                  <button class=" w-[8rem] bg-blue-700 text-sm px-2 py-2 capitalize rounded text-white add"  on:click={() => goto('/add_supplier')}>Tambah Supplier</button>
          </header>
        <div class="overflow-x-auto">
            <table class="table w-full mb-4 shadow-md">
              <!-- head -->
              <thead class="">
                <tr>
                  <th>No</th>
                  <th>Nama Supplier </th>
                  <th>Alamat</th>
                  <th>No Telp </th>
                  <th>Aksi</th>
                </tr>
              </thead>
              <tbody>
                <!-- row 1 -->
                {#each dataSupplier as data, i}
                   <!-- content here -->
                <tr>
                  <td>{++i}</td>
                  <td>{data.namaSupplier}</td>
                  <td>{data.alamat}</td>
                  <td>{data.noTelp}</td>
                  <td><button class="btn btn-error text-white" on:click={deleteSupplier(data.id)}>Hapus</button>
                    <button class="btn btn-warning " on:click={goto(`/dashboard/supplier/${data.id}`)}>Update</button></td>
                  
                </tr>
                {/each}
                
              
              </tbody>
            </table>
            <div class="flex justify-end">

                <div class="btn-group ">
                    <button class="btn">1</button>
                    <button class="btn">2</button>
                    <button class="btn btn-disabled">...</button>
                    <button class="btn">99</button>
                    <button class="btn">100</button>
                </div>
            </div>
          </div>
        </div>
        {/if}

    </div>
</div>
<style>
    .add{
        min-height: 2rem;
    }
    table th{
        background-color: #f2f2f2;
        border-radius: 0;
        color: black;
    }

    table td{
        background-color: #ffff;
        color: black;

    }

    .list-container li{
      color: black;
      cursor: pointer;
    }
    .list-container li:hover{
      background-color: rgb(74, 134, 224);
      color: #ffff;
    }
    
</style>