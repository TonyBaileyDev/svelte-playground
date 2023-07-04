<script>
    //import "$lib/adventure/models/page.js"
    import { marked } from 'marked';
    export let title = "Page 1";
    let markdown = "**This is bold**.\nHere is some _text_";
    let parsed = marked.parse(markdown);
</script>

<h3>{title}</h3>

{@html parsed}

<style>

</style>
