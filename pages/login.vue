<script setup lang="ts">
const supabase = useSupabaseClient();
const signInWithGoogle = async () => {
  const { error } = await supabase.auth.signInWithOAuth({
    provider: "google",
    options: {
      queryParams: {
        access_type: "offline",
        prompt: "consent",
      },
      redirectTo: "http://localhost:3000/confirm",
    },
  });

  if (error) {
    console.log(error);
  }
};
</script>

<template>
  <div>
    <button @click="signInWithGoogle">Sign In With Google</button>
  </div>
</template>
