<template>
<transition name="slide-down">
  <section class="lx-common-view" v-for="(view,key) in commonViews"
  :key="key" v-if="commonView==key">
    <component :is="view"/>
    <a href="javascript:;" class="close el-icon-close" @click="onClose"></a>
  </section>
</transition>
</template>
<script>
import { SET_ATTR } from '@/store/types';
import ServiceList from '@/views/common/ServiceList.vue';
import MessageList from '@/views/common/MessageList.vue';
import Userinfo from '@/views/common/Userinfo.vue';
import Preference from '@/views/common/Preference.vue';

export default {
  name: 'LxCommonView',
  data() {
    return {
      commonViews: {
        ServiceList,
        MessageList,
        Userinfo,
        Preference,
      },
    };
  },
  computed: {
    commonView() {
      return this.$store.state.commonView;
    },
  },
  mounted() {
    window.addEventListener('keyup', (e) => {
      if (e.keyCode === 27) {
        if (this.$store.state.commonView) {
          this.$store.commit(SET_ATTR, {
            commonView: '',
          });
        }
      }
    });
  },
  methods: {
    onClose() {
      this.$store.commit(SET_ATTR, {
        commonView: '',
      });
    },
  }
};
</script>
<style lang="scss" scoped>
.close{
  position: absolute;
  top: 10px;
  right: 10px;
  width: 25px;
  height: 25px;
  background: #aaa;
  border-radius: 50%;
  line-height: 25px;
  text-align: center;
  color: #FFF;
  font-size: 12px;
  text-decoration: none;
}
</style>

