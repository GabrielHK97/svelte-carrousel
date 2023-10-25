<script lang="ts">
  import cat1 from "../lib/assets/1.jpeg";
  import cat2 from "../lib/assets/2.jpeg";
  import cat3 from "../lib/assets/3.jpeg";
  import cat4 from "../lib/assets/4.jpeg";
  import cat5 from "../lib/assets/5.jpeg";

  export { cssClass as class };

  export let seconds: number = 0.2;
  let cssClass: string = "";
  const images = [cat1, cat2, cat3, cat4, cat5];
  let index: number = 0;
  let nextIndex: number = 0;
  let translate: string = "0%";
  let secs: number;

  function resetIndex(i: number): number {
    if (Math.abs(i) > images.length - 1) {
      return i % images.length;
    } else {
      return i;
    }
  }

  function goRight() {
    nextIndex = 1;
    translate = "-100%";
    secs = seconds;
    setTimeout(() => {
      index++;
      index = resetIndex(index);
      translate = "0%";
      secs = 0;
    }, seconds * 1000);
  }

  function goLeft() {
    nextIndex = -1;
    translate = "100%";
    secs = seconds;
    setTimeout(() => {
      index--;
      index = resetIndex(index);
      translate = "0%";
      secs = 0;
    }, seconds * 1000);
  }
</script>

<div class={cssClass}>
  <div class="w-full h-full overflow-hidden flex">
    <div
      class="w-full h-full flex {nextIndex > 0
        ? 'flex-row'
        : 'flex-row-reverse'}"
      style="transform: translateX({translate}); transition:{secs}s"
    >
      <img
        src={images[resetIndex(Math.abs(index))]}
        alt="current"
        class="w-full h-full"
      />
      <img
        src={images[resetIndex(Math.abs(index + nextIndex))]}
        alt="current"
        class="w-full h-full"
      />
    </div>
  </div>
  <div class="w-full h-12 space-x-2 p-2 flex flex-row bg-gray-700 rounded-b-lg">
    <button class="flex-grow rounded-lg bg-black text-white" on:click={goLeft}
      >{"<"}</button
    >
    <button class="flex-grow rounded-lg bg-black text-white" on:click={goRight}
      >{">"}</button
    >
  </div>
</div>
