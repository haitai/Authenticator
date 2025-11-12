<script setup lang="ts">
const overlay = useOverlay();

// lazy import Menu to keep the same content but show in a drawer
const Menu = defineAsyncComponent(() => import("./Menu.vue"));
const menuDrawer = overlay.create(Menu);

const props = defineProps<{
	modelValue?: string;
	placeholder?: string;
}>();
const emit = defineEmits<{
	(e: "update:modelValue", value: string): void;
}>();

const inputValue = computed({
	get: () => props.modelValue ?? "",
	set: (v: string) => emit("update:modelValue", v),
});
</script>

<template>
	<div
		class="fixed top-0 z-10 flex items-center gap-x-2 px-3 inset-x-0 h-14 bg-white ring-1 ring-neutral-200 dark:ring-neutral-800 dark:bg-neutral-900 w-full"
	>
		<div class="w-full max-w-sm xl:max-w-md mx-auto flex items-center gap-x-2">
			<div class="flex-1">
				<div
					class="flex items-center gap-x-2 h-10 rounded-full pl-1 pr-3 bg-neutral-100/80 dark:bg-neutral-800/80 ring-1 ring-neutral-200/60 dark:ring-neutral-800/60"
				>
					<UButton
						icon="i-lucide-menu"
						size="xl"
						color="neutral"
						class="rounded-full h-8 w-8 hover:bg-neutral-200/50 dark:hover:bg-neutral-700/60"
						variant="ghost"
						@click="menuDrawer.open()"
					/>
					<UInput
						v-model="inputValue"
						:placeholder="placeholder ?? 'Search...'"
						type="text"
						autocomplete="off"
						color="neutral"
						variant="ghost"
						:ui="{ base: 'flex-1', input: 'bg-transparent focus:ring-0 placeholder:text-neutral-400' }"
					/>
				</div>
			</div>
		</div>
	</div>
</template>


