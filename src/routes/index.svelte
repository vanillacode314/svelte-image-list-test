<script>
  import VirtualList from "svelte-tiny-virtual-list";

  const data = [...new Array(100).keys()].map((i) => {
    const url = `https://picsum.photos/seed/${i}/200/300`;
    return url;
  });

  let lst;
  let sizes = [...new Array(100).keys()].map((i) => 1);
  $: console.log(sizes);

  function getSize(index) {
    return sizes[index];
  }

  function onLoad(e, index) {
    console.log(e.target.naturalHeight);
    sizes[index] = e.target.naturalHeight;
    lst.recomputeSizes();
  }
</script>

<VirtualList
  width="100%"
  height={600}
  itemCount={data.length}
  itemSize={getSize}
  bind:this={lst}
>
  <div slot="item" let:index let:style {style}>
    <img src={data[index]} on:load={(e) => onLoad(e, index)} alt="test" />
  </div>
</VirtualList>
