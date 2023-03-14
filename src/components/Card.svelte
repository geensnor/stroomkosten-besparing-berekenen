<script lang="ts">
  export let title: string;
</script>

<div class="drop-shadow rounded-lg px-3 pb-5 pt-3 border bg-white">
  <div>
    <h2 class="text-lg underline-offset-2 text-orange-600 mb-3">
      {title}
    </h2>
  </div>
  <slot />
</div>
