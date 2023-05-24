


<div class="h-[85vh] flex gap-3  py-4 px-8">
    <div class="w-1/5">
        <div><span>a</span></div>
        <div><span>q</span></div>
        <div><span>qwe</span></div>
    </div>
    <div class="w-4/5">
        <div class="bg-blue-300 rounded-t-lg w-full p-3 text-blue-900">
            <h2>
                Dashboard
            </h2>
        </div>

        <div class="border-2 rounded-b-lg px-2 py-4"> 
          <header class="flex justify-between gap-3 p-3  text-black mb-2">
                  <h2 class="text-xl">Barang</h2>
                  <button class=" w-[8rem] bg-blue-700 text-sm px-2 py-2 capitalize rounded text-white add">Tambah Supplier</button>
          </header>
        <div class="overflow-x-auto">
            <table class="table w-full mb-4">
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
              <tbody>
                <!-- row 1 -->
                <tr>
                  <th>1</th>
                  <td>Cy Ganderton</td>
                  <td>Quality Control Specialist</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                </tr>
                <!-- row 2 -->
                <tr class="">
                  <th>2</th>
                  <td>Cy Ganderton</td>
                  <td>Quality Control Specialist</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                </tr>
                <!-- row 3 -->
                <tr>
                  <th>3</th>
                  <td>Cy Ganderton</td>
                  <td>Quality Control Specialist</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                  <td>Blue</td>
                </tr>
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
        background-color: white;
        color: black;

    }
    
</style>