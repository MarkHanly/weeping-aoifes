<script>
  let flipped = $state(false);
</script>

<div
  class="w-72 h-48 perspective cursor-pointer"
  role="button"
  tabindex="0"
  onclick={() => (flipped = !flipped)}
  onkeydown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      flipped = !flipped;
    }
  }}
>
  <div
    class="
      relative w-full h-full
      transform-gpu
      transform-style-preserve-3d
      transition-transform duration-700
    "
    style:transform={`rotateY(${flipped ? 180 : 0}deg)`}
  >
    <!-- Front -->
    <div
      class="
        absolute inset-0
        flex items-center justify-center
        bg-white border rounded-xl
        backface-hidden
      "
    >
      Front
    </div>

    <!-- Back -->
    <div
      class="
        absolute inset-0
        flex items-center justify-center
        bg-blue-600 text-white rounded-xl
        backface-hidden rotate-y-180
      "
    >
      Back
    </div>
  </div>
</div>