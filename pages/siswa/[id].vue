<template>
    <div class="container-fluid">
        <div class="row mt-5 justify-content-center">
            <div class="col-1 ">
                <div class="card" style="width: 10rem; min-height:10rem ;">
                    <div class="card-body">
                        <img src="assets/img/fotoprofil.png" alt="" height="120rem">
                    </div>
                </div>
            </div>

            <div class="col-5">
                <div class="card" style="width: 18rem; min-height:10rem ;">
                    <div v-if="!siswa">loading..</div>
                    <div class="card-body">
                        <h5 class="card-title">{{ siswa.nama }}</h5>
                        <h6 class="card-subtitle mb-2 text-body-secondary">{{ siswa.tingkat }}</h6>
                        <h1 class="card-text">{{ siswa.poin }} POIN</h1>
                    </div>
                </div>
            </div>
        </div>
        <div class="row justify-content-center">
            <div class="col-11">
                <table class="table table-striped table-bordered">
                    <thead>
                        <tr>
                            <th>PELANGGARAN</th>
                            <th>POINT</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(p, i) in pelanggaran" :key="i">
                            <td>{{ p.id_pelanggaran.pelanggaran }}</td>
                            <td>{{ p.id_pelanggaran.point }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="col-2 ms-auto mb-3">
                <NuxtLink to="/">
                    <button type="submit" class=" btn btn-light btn-lg rounded-5 px-5"
                        style=" background-color: #167BF1;">KEMBALI</button>
                </NuxtLink>
            </div>
        </div>

    </div>
</template>

<script setup>
const client = useSupabaseClient()
const siswa = ref({})
const pelanggaran = ref([])
const route = useRoute()
const id_siswa = route.params.id

async function getSiswaById() {
    const { data, error } = await client
        .from('siswa')
        .select(`*`)
        .eq('id', id_siswa)
        .single()
    if (data) {
        siswa.value = data
        console.log(siswa.value)
    }
}

async function getBukuByIdSiswa() {
    const { data, error } = await client
        .from('point_siswa')
        .select(`id_siswa(id), id_pelanggaran(id, pelanggaran, point)`)
        .eq('id_siswa', id_siswa)
    if (data) {
        pelanggaran.value = data
    }
}

onMounted(() => {
    getSiswaById()
    getBukuByIdSiswa()
})
</script>
