<template>
  <HomeCard v-bind="cardConfig" :table-config="tableConfig" />
</template>

<script>
import HomeCard from './HomeCard'

export default {
  name: 'Log',
  components: {
    HomeCard
  },
  props: {
    headerActions: {
      type: Object,
      default: () => {
        return {
          hasLeftActions: false,
          hasRightActions: false,
          hasSearch: false
        }
      }
    }
  },
  data() {
    return {
      cardConfig: {
        title: this.$t('common.RecentLogin')
      },
      tableConfig: {
        url: '/api/v1/audits/my-login-logs/?limit=5',
        columns: [
          'city', 'datetime'
        ],
        columnsMeta: {
          city: {
            showOverflowTooltip: true,
            formatter: (row) => {
              return <span>{ row.city }({ row.ip })</span>
            }
          },
          datetime: {
            showOverflowTooltip: true
          }
        },
        hasSelection: false,
        paginationSize: 5
      }
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
