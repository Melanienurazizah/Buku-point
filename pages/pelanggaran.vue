<template>
    <div class="container-fluid">
        <div class="row pt-5 justify-content-center">
            <div class="col">
                <h1 class="text-center my-3"> DAFTAR PELANGGARAN DAN POINNYA</h1>
            </div>
        </div>
    </div>
    <div class="row justify-content-center">
        <div class="col-11">
            <table class="table table-striped table-bordered">
                <thead>
                    <tr>
                        <th class="text-center">NO</th>
                        <th class="text-center">JENIS PELANGGARAN</th>
                        <th class="text-center">PELANGGARAN</th>
                        <th class="text-center">KONSEKUENSI</th>
                        <th class="text-center">JUMLAH POINT</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(pelanggaran, index) in pelanggaran" :key="pelanggaran.id">
                        <td class="text-center">{{ index + 1 }}</td>
                        <td class="text-center">{{ pelanggaran.jenis_pelanggaran?.nama }}</td>
                        <td class="text-center">{{ pelanggaran.pelanggaran }}</td>
                        <td class="text-center">{{ pelanggaran.konsekuensi }}</td>
                        <td class="text-center">{{ pelanggaran.point }}</td>
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
</template>

<script setup>
const supabase = useSupabaseClient()

const pelanggaran = ref([])

async function getPelanggaran() {
    const { data, error } = await supabase.from('pelanggaran').select(`
        *,
        jenis_pelanggaran (
            nama
        )
    `)
    if (error) throw error
    if (data) pelanggaran.value = data
}

onMounted(() => {
    getPelanggaran()
})
</script>

<style></style>