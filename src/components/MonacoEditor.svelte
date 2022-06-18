<script context="module">
    let monaco_promise;
    let _monaco;
    monaco_promise = import('./monaco.js');
    monaco_promise.then(mod => {
      _monaco = mod.default;
    })
</script>
  
<script>
    import { onMount } from "svelte";

    let Monaco;
    let editor;
    let container;

    onMount(() => {

        if (_monaco) {
            Monaco = _monaco;
            editor = Monaco.editor.create(container, {
                value: ['spring:'].join('\n'),
                language: 'yaml'
            });
        } else {
            monaco_promise.then(async mod => {
                Monaco = mod.default;
                editor = Monaco.editor.create(container, {
                    value: ['spring:', "\tcloud:", "\t\tgateway:", "\t\t\troutes:"].join('\n'),
                    language: 'yaml'
                });
            });
        }

        return () => {
            editor.dispose();
        }
    });

</script>

<div bind:this={container} style="height: 80vh;"></div>