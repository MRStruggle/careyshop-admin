<template>
  <cs-container>
    <page-header
      slot="header"
      ref="header"
      :loading="loading"
      @submit="handleSubmit"/>

    <page-main
      :loading="loading"
      :table-data="table"/>
  </cs-container>
</template>

<script>
import { getAppList } from '@/api/aided/app'

export default {
  name: 'setting-app-app',
  components: {
    PageHeader: () => import('./components/PageHeader'),
    PageMain: () => import('./components/PageMain')
  },
  data() {
    return {
      loading: false,
      table: []
    }
  },
  mounted() {
    this.handleSubmit()
  },
  methods: {
    // 提交查询
    handleSubmit(form) {
      this.loading = true
      getAppList(form)
        .then(res => {
          this.table = res.data || []
        })
        .finally(() => {
          this.loading = false
        })
    }
  }
}
</script>
