<template>
    <DetailViewBase>
        <AddRowForm
            :schema="schema"
            :tableName="tableName"
            v-if="schema"
        />
    </DetailViewBase>
</template>


<script lang="ts">
import Vue from "vue"
import { Location } from "vue-router"
import NavBar from "../components/NavBar.vue"
import AddRowForm from "../components/AddRowForm.vue"
import DetailViewBase from "../components/DetailViewBase.vue"

export default Vue.extend({
    props: ["tableName"],
    components: {
        AddRowForm,
        DetailViewBase
    },
    computed: {
        schema() {
            return this.$store.state.schema
        }
    },
    async mounted() {
        this.$store.commit("updateCurrentTablename", this.tableName)
        await this.$store.dispatch("fetchSchema", this.tableName)
    }
})
</script>


<style scoped lang="less">
</style>
