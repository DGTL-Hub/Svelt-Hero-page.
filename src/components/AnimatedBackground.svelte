<script>
    import { onMount } from 'svelte';
  
    let boxes = [];
    const boxSize = 40; // Width and height of a box in pixels
    const gap = 30; // Gap between boxes in pixels
    const totalSize = boxSize + gap; // Total space taken by a box including the gap
  
    function calculateBoxes() {
      const screenWidth = window.innerWidth;
      const screenHeight = window.innerHeight;
      const columns = Math.floor(screenWidth / totalSize);
      const rows = Math.floor(screenHeight / totalSize);
      boxes = Array(columns * rows).fill(0);
    }
  
    onMount(() => {
      calculateBoxes(); // Initial calculation
      const interval = setInterval(() => {
        const num = Math.floor(Math.random() * boxes.length);
        boxes[num] = Math.random();
      }, 500);
  
      // Removed the resize event listener binding
  
      return () => {
        clearInterval(interval);
        // No need to remove the resize event listener since it's not added
      };
    });
  </script>
  <div class="sec">
    {#each boxes as box, index (index)}
      <div class="box animate" style:animation-delay="{Math.random()}s"></div>
    {/each}
  </div>
  
  
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    .sec {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(40px, 1fr));
    gap: 30px;
    z-index: -1; /* Ensure it stays behind other content */
    overflow: hidden;
  }
  
  .box {
    width: 100%;
    height: 0;
    padding-top: 100%; /* Maintain aspect ratio */
    background: #222;
    animation: animate 1s linear forwards;
  }
  
    @keyframes animate {
      0% {
        background: transparent;
      }
      50% {
        background: #33e48c;
      }
      100% {
        background: transparent;
      }
    }
  </style>