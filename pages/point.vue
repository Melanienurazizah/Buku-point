<template>
    <div class="container-fluid">
        <div class="row justify-content-center mt-5">
            <div class="col">
                <h1 class="text-center my-3"> BERI POINT KEPADA SISWA</h1> 
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-4">
                <div class="my-2">
                    <select class="form-select form-select-lg mb-3 rounded-4" aria-label="Large select example" style="background-color: #D9D9D9;">
                        <option selected>KELAS</option>
                        <option value="1">XII PPLG 1</option>
                        <option value="2">XII PPLG 2</option>
                        <option value="3">XII PPLG 3</option>
                        <option value="3">XII PPLG 4</option>
                    </select>
                </div>
                <div class="my-2">
                    <select class="form-select form-select-lg mb-3 rounded-4" aria-label="Large select example" style="background-color: #D9D9D9;">
                        <option selected>NAMA</option>
                        <option value="1">ALISHA RAHMAH FADILAH</option>
                        <option value="2">ANGGI</option>
                        <option value="3">AZRIL MAULANA</option>
                    </select>
                </div>
                <div class="my-2 d-flex justify-content-center">
                        <div class="card" style="width: 10rem; min-height:10rem ;">
                            <div class="card-body d-inline">
                                <img src="assets/img/fotoprofil.png" alt="" height="120rem">
                            </div>
                        </div>
                        <div class="card" style="width: 18rem; min-height:10rem ;">
                            <div class="card-body d-inline">
                                <h5 class="card-title">NAMA SISWA</h5>
                                <h6 class="card-subtitle mb-2 text-body-secondary">KELAS</h6>
                                <h1 class="card-text">15 POIN</h1>
                            </div>
                        </div>
                </div>
                <div class="my-2">
                    <select class="form-select form-select-lg mb-3 rounded-4" aria-label="Large select example" style="background-color: #D9D9D9;">
                        <option selected>PELANGGARAN</option>
                        <option value="1">Terlambat</option>
                        <option value="2">Kehadiran</option>
                        <option value="3">Pakaian</option>
                        <option value="3">Penampilan/Kepribadian</option>
                    </select>
                </div>
                <div class="col-2 ms-auto mb-3">
            <NuxtLink to="siswa">
            <button type="submit" class=" btn btn-light btn-lg rounded-5 px-5" style=" background-color: #167BF1;">KIRIM</button>
            </NuxtLink>
        </div> 
        </div>    
        <div class="row justify-content-center">
            <div class="col-11">
                <table class="table table-striped table-bordered">
                </table>
                </div>
            </div>
        </div>
    </div>
    </template>