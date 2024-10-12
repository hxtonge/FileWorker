<script setup lang="ts">
import { ref } from 'vue';
import Cookies from 'js-cookie';
import { toast } from '@/utils/toast';
import { useRouter } from 'vue-router';
import { useI18n } from 'vue-i18n';

const router = useRouter();
const { t: $t } = useI18n();

const password = ref('');

const onSubmitBtnClick = () => {
  Cookies.set('PASSWORD', password.value);
  toast($t("login.setting_success"), 'success');
  setTimeout(() => {
    if (window.history.state.back) {
      router.back();
    } else {
      router.replace({ path: '/' })
    }
  }, 1000);
}
</script>

<template>
  <div class="min-h-screen bg-gray-100 dark:bg-gray-900 flex flex-col">
    <div class="container mx-auto px-4 py-50 flex-1">
      <div class="max-w-md mx-auto bg-white dark:bg-gray-800 rounded-lg shadow-lg overflow-hidden transform transition-all duration-300 ease-in-out hover:shadow-2xl animate-fade-in-up">
        <div class="px-6 py-8">
          <h2 class="text-2xl font-bold text-center text-gray-800 dark:text-white">{{ $t("login.login_title") }}</h2>
          <div class="mt-6">
            <input class="w-full px-4 py-2 text-gray-700 bg-gray-200 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 dark:bg-gray-700 dark:text-white dark:border-gray-600 transform transition-transform duration-200 hover:-translate-y-1 hover:shadow-md"
                   type="password" v-model="password" :placeholder="$t('login.password_placeholder')">
          </div>
          <button id="submit-button"
                  class="w-full mt-6 px-4 py-2 text-white bg-blue-600 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 transform transition-transform duration-200 hover:-translate-y-1 hover:shadow-md"
                  @click="onSubmitBtnClick">
            {{ $t("login.login_button") }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translate3d(0, 50%, 0);
  }
  to {
    opacity: 1;
    transform: translateZ(0);
  }
}

.animate-fade-in-up {
  animation: fadeInUp 0.6s ease-out;
}

@media (min-width: 640px) {
  .container {
    max-width: 640px;
  }
}
@media (min-width: 768px) {
  .container {
    max-width: 768px;
  }
}
@media (min-width: 1024px) {
  .container {
    max-width: 1024px;
  }
}
</style>
