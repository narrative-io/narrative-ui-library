<template lang="pug">
  .test-icons
    .icons.display-icons
      NioIcon(name="display-new")
      NioIcon(name="display-list")
      NioIcon(name="display-reports")
      NioIcon(name="display-preferences")
      NioIcon(name="display-quick-start")
      NioIcon(name="display-listmanager")
      NioIcon(name="display-sources")
      NioIcon(name="display-destinations")
      NioIcon(name="display-payment")
      NioIcon(name="display-help")
      NioIcon(name="display-email")
      NioIcon(name="display-website")
      NioIcon(name="display-security")
      NioIcon(name="display-privacy")
      NioIcon(name="display-module")
      NioIcon(name="display-search")
      NioIcon(name="display-notification")
      NioIcon(name="display-subscriptions")
      NioIcon(name="display-hamburger")
      NioIcon(name="display-logout")
      NioIcon(name="display-close")
      NioIcon(name="display-file")
      NioIcon(name="display-cart")
      NioIcon(name="display-company")
      NioIcon(name="display-upload")
      NioIcon(name="display-download")
      NioIcon(name="display-yourprofile")
      NioIcon(name="display-warning")
      NioIcon(name="display-invoice")
      NioIcon(name="display-kb")
      NioIcon(name="display-budget")
      NioIcon(name="display-list-warning")
      NioIcon(name="display-curvy-arrow")
    br
    br
    .icons.utility-icons
      NioIcon(name="utility-code")
      NioIcon(name="utility-plus")
      NioIcon(name="utility-chevron-left")
      NioIcon(name="utility-times")
      NioIcon(name="utility-external-link")
      NioIcon(name="utility-more")
      NioIcon(name="utility-chevron-left")
      NioIcon(name="utility-arrow-left")
      NioIcon(name="utility-trash")
      NioIcon(name="utility-android")
      NioIcon(name="utility-apple" color="#415298")
      NioIcon(name="utility-lock")
      NioIcon(name="utility-search")
      NioIcon(name="utility-chevron-down")
      NioIcon(name="utility-envelope")
      NioIcon(name="utility-link")
      NioIcon(name="utility-linkedin")
      NioIcon(name="utility-twitter")
      NioIcon(name="utility-eye")
      NioIcon(name="utility-eye-slash")
      NioIcon(name="utility-exclamation")
</template>

<script>

import NioIcon from '../components/icon/Icon'

export default {
  components: {
    NioIcon
  },
  data: () => ({
   
  })
};
</script>

<style lang="sass" scoped>
.icons
  display: flex
  flex-wrap: wrap
  & > * + * 
    margin-left: 10px
    
  
</style>