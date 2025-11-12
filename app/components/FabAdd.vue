<script setup lang="ts">
import Form from "./Form.vue";
import Qrscan from "./Qrscan.vue";

const overlay = useOverlay();
const formModal = overlay.create(Form);
const qrModal = overlay.create(Qrscan);

const isOpen = ref(false);

const openForm = () => {
	isOpen.value = false;
	setTimeout(() => formModal.open(), 150);
};
const openQrscan = () => {
	isOpen.value = false;
	setTimeout(() => qrModal.open(), 150);
};
</script>

<template>
	<div class="fixed right-4 bottom-5 sm:right-6 sm:bottom-6 z-20 flex flex-col items-end">
		<Transition name="fade" appear>
			<div v-if="isOpen" class="mb-4 flex flex-col items-end gap-3">
				<div class="flex items-center gap-3">
					<UButton
						color="neutral"
						variant="soft"
						class="rounded-full text-base px-5 h-11"
						@click="openQrscan"
					>扫描二维码</UButton>
					<UButton
						color="primary"
						variant="solid"
						class="rounded-full h-12 w-12"
						@click="openQrscan"
					>
						<UIcon name="i-heroicons-camera-20-solid" class="h-6 w-6" />
					</UButton>
				</div>
				<div class="flex items-center gap-3">
					<UButton
						color="neutral"
						variant="soft"
						class="rounded-full text-base px-5 h-11"
						@click="openForm"
					>输入设置密钥</UButton>
					<UButton
						color="primary"
						variant="solid"
						class="rounded-full h-12 w-12"
						@click="openForm"
					>
						<UIcon name="i-heroicons-key-solid" class="h-6 w-6" />
					</UButton>
				</div>
			</div>
		</Transition>

		<UButton
			class="rounded-full h-14 w-14 shadow-lg active:translate-y-0.5 flex-center"
			color="primary"
			variant="solid"
			@click="isOpen = !isOpen"
			:aria-expanded="isOpen"
		>
			<UIcon name="i-heroicons-plus-16-solid" class="h-7 w-7 transition-transform" :class="isOpen ? 'rotate-45' : ''" />
		</UButton>
	</div>
</template>

