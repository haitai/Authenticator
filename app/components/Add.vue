<script setup lang="ts">
import Form from "./Form.vue";
import Qrscan from "./Qrscan.vue";

const overlay = useOverlay();

const emit = defineEmits(["close"]);

const formModal = overlay.create(Form);
const qrModal = overlay.create(Qrscan);

const openForm = async () => {
  emit("close");
  setTimeout(() => formModal.open(), 300);
};

const openQrscan = async () => {
  emit("close");
  setTimeout(() => qrModal.open(), 300);
};
</script>

<template>
  <UDrawer side="bottom" :close="true" :ui="{ width: 'w-full', content: 'p-4 pb-8 rounded-t-3xl' }">
    <template #content>
      <div class="space-y-4">
        <div class="flex items-center justify-between gap-x-3">
          <UButton
            color="neutral"
            variant="soft"
            class="rounded-full text-base px-6 h-12"
            @click="openQrscan"
            >扫描二维码</UButton
          >
          <UButton
            color="primary"
            variant="solid"
            class="rounded-full h-14 w-14"
            @click="openQrscan"
          >
            <UIcon name="i-heroicons-camera-20-solid" class="h-6 w-6" />
          </UButton>
        </div>
        <div class="flex items-center justify-between gap-x-3">
          <UButton
            color="neutral"
            variant="soft"
            class="rounded-full text-base px-6 h-12"
            @click="openForm"
            >输入设置密钥</UButton
          >
          <UButton
            color="primary"
            variant="solid"
            class="rounded-full h-14 w-14"
            @click="openForm"
          >
            <UIcon name="i-heroicons-computer-desktop-16-solid" class="h-6 w-6" />
          </UButton>
        </div>
      </div>
    </template>
  </UDrawer>
</template>
