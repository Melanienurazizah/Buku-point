<template>
    <div class="container-fluid">
        <div class="mt-5 row justify-content-center">
            <div class="col-10">
                <!-- <form @submit.prevent="getSiswaById">
                    <input
                    v-model="keyword"
                    type="search"
                    class="form-control rounded-5"
                    placeholder="Cari siswa"
                    />
                </form> -->
                <select v-model="selectedKelas" @change="getSiswa" class="form-select mb-3">
                    <option :value="null">Pilih Kelas</option>
                    <option v-for="kelas in classes" :value="kelas.id">{{ kelas.nama }}</option>
                </select>
                <select v-model="selectedSiswa" :disabled="!selectedKelas" @change="getSiswaById" class="form-select">
                    <option :value="null">Pilih Siswa</option>
                    <option v-for="siswa in students" :value="siswa.id">{{ siswa.nama }}</option>
                </select>
            </div>
        </div>
        <div class="row my-3 justify-content-center">
                <div class="card" style="width: 16rem; min-height:14rem ;">
                    <div class="card-body">
                        <img src="assets/img/fotoprofil.png" alt="" height="200rem">
                    </div>
                </div>
                <div class="card" style="width: 30rem; min-height:15rem ;">
                    <div v-if="!siswa">loading..</div>
                    <div class="card-body">
                        <h5 class="card-title">{{ siswa.nama }}</h5>
                        <h6 class="card-subtitle mb-2 text-body-secondary">{{ siswa.tingkat }}</h6>
                        <h1 class="card-text">{{ siswa.poin }} POIN</h1>
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
                        <tr v-for="pelanggaran in siswa.point_siswa" :key="pelanggaran.id">
                            <td>{{ pelanggaran.pelanggaran.pelanggaran }}</td>
                            <td>{{ pelanggaran.pelanggaran.point }}</td>
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
const classes = ref([])
const selectedKelas = ref(null)
const siswa = ref({})
const students = ref([])
const selectedSiswa = ref(null)
const pelanggaran = ref([])

async function getSiswaById() {
    const { data, error } = await client
        .from('siswa')
        .select(`
            *,
            point_siswa (
                pelanggaran (
                    *,
                    jenis_pelanggaran (
                        nama
                    )
                )
            )
        `)
        .eq('id', selectedSiswa.value)
        .single()
    if (error) throw error
    if (data) {
        siswa.value = data
    }
}

async function getKelas() {
    const { data, error } = await client
        .from('kelas')
        .select()
    if (error) throw error
    if (data) classes.value = data
}

async function getSiswa() {
    const { data, error } = await client
        .from('siswa')
        .select()
        .eq('kelas', selectedKelas.value)
        .order("id", {ascending: true})
    if (error) throw error
    if (data) students.value = data
}

onMounted(() => {
    getKelas()
})
</script>
