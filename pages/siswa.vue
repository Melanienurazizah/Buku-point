<template>
    <div class="container-fluid">
        <div class="row pt-5 justify-content-center">
            <div class="col-1 ">
                <div class="card" style="width: 10rem; min-height:10rem ;">
                    <div class="card-body">
                        <img src="assets/img/fotoprofil.png" alt="" height="120rem">
                    </div>
                </div>
            </div>
            <div class="col-5">
                <div class="card" style="width: 18rem; min-height:10rem ;">
                    <div class="card-body">
                        <h5 class="card-title">NAMA SISWA</h5>
                        <h6 class="card-subtitle mb-2 text-body-secondary">KELAS</h6>
                        <h1 class="card-text">15 POIN</h1>
                    </div>
                </div>
            </div>
        </div>
    <div class="row justify-content-center">
        <div class="col-11">
            <table class="table table-striped table-bordered">
                <thead>
                    <tr>
                        <th class="text-center">NAMA POINT YANG DILANGGAR</th>
                        <th class="text-center">JUMLAH POINT</th>
                    </tr>
                    <tr>
                        <td>tidak memakai dasi</td>
                        <td>5</td>
                    </tr> 
                </thead>
            </table>
        </div>
        <div class="col-2 ms-auto mb-3">
            <NuxtLink to="//">
            <button type="submit" class=" btn btn-light btn-lg rounded-5 px-5" style=" background-color: #167BF1;">KEMBALI</button>
            </NuxtLink>
        </div> 
    </div>

    </div>
</template>
<style></style>