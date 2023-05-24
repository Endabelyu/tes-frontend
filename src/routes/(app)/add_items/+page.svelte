<script>
import { goto } from '$app/navigation';
    let unRegister = false
</script>


<div class="flex h-[95vh] pt-[8rem] ">
 
        <div class="w-2/4  mx-auto px-2">
            <div class="w-4/5 mx-auto">
    
             <div class="bg-sky-200  w-full rounded-t-lg text-blue-400 py-3 px-3"><h5 class="text-xl">Tambah Barang</h5></div>
             <div class="border bg-white  rounded-b-lg p-4">
                <div class="form-control rounded">
                  <!-- <form action=""> -->
                    <div class="flex gap-x-[4rem] mb-2">
                      <label for="nama_barang">Nama Barang</label>
                      <input type="text" placeholder="Masukan Nama Barang" name="nama_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                    </div>
                    <div class="flex gap-x-[4rem] mb-2">
                      <label for="harga_barang">Harga Barang</label>
                      <input type="text" placeholder="Masukan Harga Barang" name="harga_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                    </div>
                    <div class="flex gap-x-[4.8rem] mb-2">
                      <label for="stok_barang">Stok Barang</label>
                      <input type="text" placeholder="Masukan Stok Barang" name="stok_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                    </div>
                    <div class="flex gap-x-[4.8rem] mb-2">
                      <label for="stok_barang">Stok Barang</label>
                      <input type="text" placeholder="Masukan Stok Barang" name="stok_barang" class="w-[65%] bg-white border-2 p-1 rounded border-gray-200">
                    </div>
                  
                  <!-- svelte-ignore a11y-label-has-associated-control -->
                    
                  <div class="flex justify-between">
                    
                    <button class="btn btn-info  text-white bg-gray-500 mt-4" on:click={() => goto('/dashboard')}>Kembali</button>
                    <button class="btn btn-info  text-white bg-sky-700 mt-4" on:click={() => goto('/dashboard')}>Tambah</button>
                  </div>
                  <!-- </form>   -->

                  </div>
             </div>
        </div>
    
        </div>
    
   
</div>