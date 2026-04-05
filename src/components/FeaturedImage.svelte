<script>
  let { img = "" } = $props();
</script>

<div class="img-wrapper">
  <img src="./img/{img}" alt="a rectangle" />
</div>

<!-- 

the featured image component is a single image. it may need
to be wrapped in additional component that can handle a hover
state and be aware of other images 

-->
