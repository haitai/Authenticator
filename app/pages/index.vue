<script setup lang="ts">
definePageMeta({
  middleware: "auth",
});

const { data, status } = await useLazyFetch("/api/accounts", {
  key: "accounts",
  server: false,
});

const searchQuery = ref("");

const accounts = computed(() => {
  const q = searchQuery.value?.trim().toLowerCase();
  if (!q) return data.value;
  return data.value?.filter((item) => {
    const label = (item.label ?? "").toLowerCase();
    const issuer = (item.issuer ?? "").toLowerCase();
    return label.includes(q) || issuer.includes(q);
  });
});

// remove old overlay search state
</script>

<template>
  <TopBar v-model="searchQuery" placeholder="Search..." />
  <div
    v-if="!data?.length && status === 'success'"
    class="h-dvh overflow-hidden flex-center flex-col space-y-2 pt-12"
  >
    <UIcon name="i-heroicons-inbox-stack" class="h-8 w-8" />
    <span class="text-lg sm:text-xl font-semibold">Nothing here yet.</span>
    <span class="text-sm font-normal text-neutral-400"
      >Please use the button below to add something !</span
    >
  </div>
  <div
    v-else
    class="h-full scroll-smooth w-full grid place-items-center gap-y-2 gap-x-4 mt-16 grid-cols-1 sm:grid-cols-2 xl:grid-cols-3 pb-24 sm:pb-16"
  >
    <Tile v-for="account in accounts" :account="account" :key="account.id" />
  </div>
  <FabAdd />
</template>
