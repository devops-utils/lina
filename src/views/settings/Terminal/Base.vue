<template>
  <IBox>
    <GenericCreateUpdateForm v-bind="$data" />
  </IBox>
</template>
<script>
import IBox from '@/components/IBox'
import { GenericCreateUpdateForm } from '@/layout/components'

export default {
  name: 'Terminal',
  components: {
    IBox,
    GenericCreateUpdateForm
  },
  data() {
    const comp = this.$t('common.Component')
    return {
      fields: [
        [
          `SSH ${comp}(KoKo)`,
          [
            'TERMINAL_PASSWORD_AUTH', 'TERMINAL_PUBLIC_KEY_AUTH',
            'TERMINAL_ASSET_LIST_SORT_BY', 'TERMINAL_KOKO_HOST', 'TERMINAL_KOKO_SSH_PORT',
            'TERMINAL_ASSET_LIST_PAGE_SIZE', 'TERMINAL_TELNET_REGEX'
          ]
        ],
        [
          `RDP ${comp}(XRDP)`,
          [
            'XRDP_ENABLED', 'TERMINAL_RDP_ADDR'
          ]
        ],
        [
          `DB ${comp}(Magnus)`,
          [
            'TERMINAL_MAGNUS_ENABLED', 'TERMINAL_MAGNUS_HOST', 'TERMINAL_MAGNUS_MYSQL_PORT',
            'TERMINAL_MAGNUS_POSTGRE_PORT', 'TERMINAL_MAGNUS_MARIADB_PORT'
          ]
        ]
      ],
      fieldsMeta: {
        TERMINAL_TELNET_REGEX: {
          type: 'input'
        },
        TERMINAL_RDP_ADDR: {
          hidden: () => {
            return !this.$store.getters.hasValidLicense
          }
        },
        XRDP_ENABLED: {
          hidden: () => {
            return !this.$store.getters.hasValidLicense
          },
          el: {
            hiddenGroup: true
          }
        }
      },
      getUrl: () => '/api/v1/settings/setting/?category=terminal',
      hasDetailInMsg: false,
      submitMethod() {
        return 'put'
      },
      cleanFormValue(data) {
        Object.keys(data).forEach(
          function(key) {
            if (data[key] === null) {
              delete data[key]
            }
          }
        )
        return data
      }
    }
  },
  methods: {
  }
}
</script>

<style scoped>

</style>
