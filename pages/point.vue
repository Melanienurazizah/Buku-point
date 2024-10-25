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
                    <select class="form-select form-select-lg mb-3 rounded-4" aria-label="Large select example"
                        style="background-color: #D9D9D9;">
                        <option disabled selected>NAMA</option>
                        <option v-for="siswa in siswa" :key="siswa.id" :value="siswa.id">{{ siswa.nama }}</option>
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
                    <select class="form-select form-select-lg mb-3 rounded-4" aria-label="Large select example"
                        style="background-color: #D9D9D9;">
                        <option selected>JENIS PELANGGARAN</option>
                        <option v-for="data in jenis" :key="data.id" :value="data.id">{{ data.nama }}</option>
                    </select>
                </div>
                <div class="my-2">
                    <select class="form-select form-select-lg mb-3 rounded-4" aria-label="Large select example"
                        style="background-color: #D9D9D9;">
                        <option selected>PELANGGARAN</option>
                        <option v-for="point in pelanggaran" :key="point.id" :value="point.id">{{ point.pelanggaran }}</option>
                    </select>
                </div>
                <div class="col-2 ms-auto mb-3">
                    <NuxtLink to="siswa">
                        <button type="submit" class=" btn btn-light btn-lg rounded-5 px-5"
                            style=" background-color: #167BF1;">KIRIM</button>
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

<script setup>
definePageMeta({
    middleware: 'auth'
})

const supabase = useSupabaseClient()

const siswa = ref([])
const jenis = ref([])
const pelanggaran = ref([])

async function getSiswa() {
    const { data, error } = await supabase.from('siswa').select('id, nama')
    if (error) throw error
    if (data) siswa.value = data
}

async function getJenis() {
    const { data, error } = await supabase.from('jenis_pelanggaran').select('id, nama')
    if (error) throw error
    if (data) jenis.value = data
}

async function getPelanggaran() {
    const { data, error } = await supabase.from('pelanggaran').select('id, pelanggaran')
    if (error) throw error
    if (data) pelanggaran.value = data
}

onMounted(() => {
    getSiswa()
    getJenis()
    getPelanggaran()
})
</script>