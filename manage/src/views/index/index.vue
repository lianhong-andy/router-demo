<template>
  <div>欢迎来到人员管理系统
    <footer-nav :class="{'isIndex':isNowPage}"></footer-nav>
  </div>
</template>

<script>
    import FooterNav from '../../components/footer'
    export default {
        components: {
          FooterNav
        },
        data(){
          return {
            isNowPage: true
          }
        }
    }
</script>

<style scoped>

</style>
