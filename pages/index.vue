<template>
    <div class="container-fluid">
       <div class="row justify-content-around align-items-center" style="height: 80vh;">
           <div class="col-sm-4">
               <div class="card bg1">
                   <div class="card-body">
                       <h5 class="card-title">MEMBERIKAN POINT </h5>
                   </div>
               </div>
           </div>
           <div class="col-sm-4">
               <div class="card bg2">
                   <div class="card-body">
                       <h5 class="card-title" style="opacity: none;">MELIHAT RIWAYAT POINT</h5>
                   </div>
               </div>
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