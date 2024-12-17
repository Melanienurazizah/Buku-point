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
                            <option disabled value="">NAMA</option>
                            <option v-for="siswa in siswa" :key="siswa.id" :value="siswa.id">{{ siswa.nama }}</option>
                        </select>
                    </div>

                    <div class="my-3">
                        <select v-model="selectedJenis" @change="getPelanggaran"  class="form-select form-select-lg mb-3 rounded-4"
                            aria-label="Large select example" style="background-color: #D9D9D9;">
                            <option disabled :value="null">JENIS PELANGGARAN</option>
                            <option v-for="data in jenis" :key="data.id" :value="data.id">{{ data.nama }}</option>
                        </select>
                    </div>
                    <div class="my-3">
                        <select v-model="form.id_pelanggaran" :disabled="!selectedJenis" class="form-select form-select-lg mb-3 rounded-4"
                            aria-label="Large select example" style="background-color: #D9D9D9;">
                            <option disabled value="">PELANGGARAN</option>
                            <option v-for="point in pelanggaran" :key="point.id" :value="point.id">{{ point.pelanggaran}}</option>
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
const selectedJenis = ref(null)
const pelanggaran = ref([])
const form = ref({
    id_siswa: "",
   
    id_pelanggaran: "",
});

const kirimData = async () => {
    console.log(form.value)
    const { error } = await supabase.from('point_siswa').insert([form.value])
    if (error) throw error
    navigateTo(`/siswa/${form.value.id_siswa}`)
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
    const { data, error } = await supabase.from('pelanggaran').select('id, pelanggaran').eq("jenis_pelanggaran", selectedJenis.value)
    if (error) throw error
    if (data) pelanggaran.value = data
}

// const getJenis = async () => {
//     const { data, error} = await supabase
//         .form("jenis_pelanggaran")
//         .select("*")
//         .order("id", { ascending: true});
//     if (data) jenis.value = data;
// };

// const getPelanggaran = async (event) => {
//     let id = event.target.value;
//     form.value.jenis_pelanggaran = parseInt(id);
//     conts {data, error} = await supabase
//         .from("pelanggaran")
//         .select('*, jenis_pelanggaran(id, nama)')
//         .eq("jenis_pelanggaran",id)
//         .order("id", {ascending: true});
//     if (data) pelanggaran.value = data;
// };
onMounted(() => {
    getSiswa();
    getJenis();
})
</script>