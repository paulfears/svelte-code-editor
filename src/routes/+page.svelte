<script>
    import {JSEditor} from "$lib/index.js";
    import {Editor} from "$lib/index.js";

    let code = `alert("hello world");`;
    let logExample = `console.log("hello world");`;
    let logs = [];

    function logFunction(logValue){
        logs = [...logs, logValue];
    };



</script>

<div class="container">
    <h1>the Editor Component</h1>
</div>

<div class="container">
<h1>the JSEditor Component</h1>
<Editor width="100%" value={`
import {JSEditor} from "svelte-code-editor";
<JSEditor title="Code Editor JS" bind:code={code} width="100%" height="30rem"/>`}
/>
<br/>
        <div style="display:flex; gap: 1em;">
            <div style="display:flex; flex-direction: column; width: 50%;">
                <JSEditor title="Code Editor JS" bind:code={code} width="100%" height="10rem"/>
            </div>
            <div style="display:flex; flex-direction: column; width: 50%;">
                <h2>2 Way Binding out of the box</h2>
                <textarea bind:value={code}/>
            </div>
        </div>
</div>


<div class="container">

<Editor value={`
<script>
    let logs = [];
    const logFunction = (logValue)=>logs = [...logs, logValue];;
</script>
import {JSEditor} from "svelte-code-editor";
<JSEditor title="Code Editor JS" bind:code={code} logCallBack={logFunction}  width="100%"/>
{#each logs as log}
    <p>{log}</p>
{/each}
`
}/>

    <JSEditor title="Code Editor JS" bind:code={logExample} logCallBack={logFunction} width="100%"/>
    {#each logs as log}
        <p>{log}</p>
    {/each}
</div>


<style>
    .container{
        width: 80vw;
        margin: auto;
        display: flex;
        justify-content: center;
        flex-direction: column;
        padding-top: 5rem;
    }
    textarea{
        width: 100%;
        height: fit-content;
    }
</style>