<script>
    import { Highlight } from "svelte-highlight";
  import cpp from "svelte-highlight/languages/cpp";
  import "svelte-highlight/styles/github.css";

  const code = `
    void main(){
        printf("Hello world")
    }
  `;
</script>

<main>
    <Highlight language={cpp} {code} />
</main>

<style>
</style>