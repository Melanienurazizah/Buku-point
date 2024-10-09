<template>
    <div class="container-fluid">
       <div class="row justify-content-around align-items-center" style="height: 80vh;">
           <div class="col-sm-4">
            <NuxtLink to="point">
               <div class="card shadow bg1">
                   <div class="card-body">
                       <h5 class="card-title">MEMBERIKAN POINT </h5>
                   </div>
               </div>
            </NuxtLink>   
           </div>
           <div class="col-sm-4">
            <NuxtLink to="login">
               <div class="card bg2 shadow">
                   <div class="card-body">
                       <h5 class="card-title" style="opacity: none;">MELIHAT RIWAYAT POINT</h5>
                   </div>
               </div>
            </NuxtLink>
           </div>
           <div class="col-sm-4">
            <NuxtLink to="/pelanggaran">
               <div class="card bg2 shadow">
                   <div class="card-body">
                       <h5 class="card-title" style="opacity: none;">MELIHAT PELANGGARAN</h5>
                   </div>
               </div>
            </NuxtLink>
           </div>
       </div>
    </div>   
   </template>
   
   <style scoped>
   .card-body{
       height: 10rem;
   }
    .card{
    position: relative;
   }
    .card .card-title{
        position: relative;
        top: 10;
        left: 10px;
        font-size: 40px;
   }
   .bg1{
    background-image:url("/assets/img/guru.png") ;
    background-size: cover;
    
   }
   .bg2{
    background-image: url("/assets/img/siswa.png");
    background-size: cover;
    
   }
   </style>