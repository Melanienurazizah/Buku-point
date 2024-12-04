<template>
    <div class="container-fluid">
        <div class="row justify-content-center mt-5">
            <div class="col">
                <h1 class="text-center my-3"> BERI POINT KEPADA SISWA</h1>
            </div>
        </div>
        <form @submit.prevent="kirimData">
            <div class="row justify-content-center">
                <div class="col-4">
                    <div class="my-3">
                        <select v-model="form.id_siswa" class="form-select form-select-lg mb-3 rounded-4"
                            aria-label="Large select example" style="background-color: #D9D9D9;">
                            <option disabled selected>NAMA</option>
                            <option v-for="siswa in siswa" :key="siswa.id" :value="siswa.id">{{ siswa.nama }}</option>
                        </select>
                    </div>

                    <div class="my-3">
                        <select v-model="form.id_jenis_pelanggaran" class="form-select form-select-lg mb-3 rounded-4"
                            aria-label="Large select example" style="background-color: #D9D9D9;">
                            <option selected>JENIS PELANGGARAN</option>
                            <option v-for="data in jenis" :key="data.id" :value="data.id">{{ data.nama }}</option>
                        </select>
                    </div>
                    <div class="my-3">
                        <select v-model="form.id_pelanggaran" class="form-select form-select-lg mb-3 rounded-4"
                            aria-label="Large select example" style="background-color: #D9D9D9;">
                            <option selected>PELANGGARAN</option>
                            <option v-for="point in pelanggaran" :key="point.id" :value="point.id">{{ point.pelanggaran
                                }}</option>
                        </select>
                    </div>


                    <button type="submit" class=" btn btn-light btn-lg rounded-5 px-5"
                        style=" background-color: #167BF1;">KIRIM</button>


                </div>
                <div class="row justify-content-center">
                    <div class="col-11">
                        <table class="table table-striped table-bordered">
                        </table>
                    </div>
                </div>
            </div>
        </form>
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
const form = ref({
    id_siswa: "",
    id_jenis_pelanggaran: "",
    id_pelanggaran: "",
});

const kirimData = async () => {
    // console.log(form.value)
    const { error } = await supabase.from('point_siswa').insert([form.value])
    if (!error) navigateTo(`/siswa/${form.value.id_siswa}`)
}

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
    getSiswa();
    getJenis();
    getPelanggaran();
})
</script>