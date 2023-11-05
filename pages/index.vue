<script setup lang="ts">
const supabase = useSupabaseClient();
const config = useRuntimeConfig();

const user = (await supabase.auth.getSession()).data.session?.access_token;
console.log(user);

console.log(config.public.backendUrl);

const { data, error, pending, refresh } = useFetch(
  `${config.public.backendUrl}/auth`,
  {
    headers: {
      Authorization: `Bearer ${user}`,
    },
  }
);
</script>

<template>
  <div v-if="pending">Loading</div>
  <div v-else>not loading, i have some data</div>
</template>
