<script>
  export let step = 1;
  export let label = "";
  export let error = "";
  export let maxlength = 10;
  export let value;
  export let inputClass;

  let type = "number";

  const handleInput = ({ target: t }) => {
    value = t.value === "" ? null : t.valueAsNumber;
    value =
      t.value.length > maxlength
        ? (value = t.value.slice(0, maxlength))
        : t.value;

    if (inputClass == "hours" && (value > 24 || value < 0)) {
      error = "tussen 0 en 24 uren";
    } else {
      error = "";
    }
  };
</script>

<label class="block text-gray-700 text-sm font-bold m-2">
  {#if label}
    <span class="block">{label}</span>
  {/if}
  <input
    class="appearance-none border border-gray-400 rounded w-full py-2 px-3 text-gray-700 focus:outline-none focus:shadow-outline"
    {type}
    {step}
    {value}
    class:error
    on:input={handleInput}
    on:input
  />
  {#if error}
    <span class="block text-red-600">{error}</span>
  {/if}
</label>
