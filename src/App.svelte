<script>
  import Navbar from "./lib/Navbar.svelte";
  import Opertion from "./lib/Opertion.svelte";
</script>

<body>
  <!-- navbar -->
  <Navbar />

  <!-- visual linked list -->
  <div class="visual-list">
    s
  </div>
  <!-- code editor and list operation -->
  <div class="code-operation">
    <!-- operation -->
    <div class="operation">
      <Opertion />
    </div>
    <!-- code -->
    <div class="code">

    </div>
  </div>
</body>

<style>

  .visual-list{
    height: 50vh;
    width: 100%;
    background-color: red;
  }

  .code-operation{
    background-color: green;
    width: 100%;
    height: 40vh;
    display: flex;
  }

  .operation{
    background-color: brown;
    width: 30%;
    height: 100%;
  }
</style>

