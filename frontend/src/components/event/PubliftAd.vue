

<script>
import { mapActions } from "vuex"
import { upgradeDialogTypes } from "@/constants"

export default {
  name: "PubliftAd",

  props: {
    showAd: { type: Boolean, default: false },
    fuseId: { type: String, default: "" },
  },

  mounted() {
    if (this.showAd && this.fuseId) this.$nextTick(() => this.registerZone())
  },

  watch: {
    showAd: {
      handler(val) {
        if (val && this.fuseId) this.$nextTick(() => this.registerZone())
      },
    },
  },

  methods: {
    ...mapActions(["showUpgradeDialog"]),
    removeAds() {
      this.showUpgradeDialog({ type: upgradeDialogTypes.REMOVE_ADS })
    },
    registerZone() {
      const fuseId = this.fuseId
      const fusetag = window.fusetag || (window.fusetag = { que: [] })
      fusetag.que.push(function () {
        fusetag.registerZone(fuseId)
      })
    },
  },
}
</script>
