<script lang='ts'>
	import { sdkString } from '$lib/JSEditor/jsStringEsc.js';
	import { Card } from '@metastellar/ui-library';
	import Editor from '../Editor/Editor.svelte';
    import {Button} from 'flowbite-svelte';
    
    export let code = ``;
    export let prependCode = ``;
    export let width = '100%';
    export let height = '100%';
    export let logCallBack = (args)=>args;
    
    {
        const log = console.log.bind(console)
        console.log = (...args) => {
            log(...args);
            logCallBack(args);
        }
    }
    function exec(){
        window.onerror = (e) => {alert(e)}
        let ToBeRun = prependCode+code
        try{
            eval(ToBeRun);
        }
        catch(e){
            alert(e);
            console.error(e);
        }
        
        
    }

    
    $:code
</script>


<div class="uk-container justify-center">
    <Card  shadow>
        <slot></slot>
        <Editor width={width} height={height} bind:value={code}>
        </Editor>
        <br/>
        <Button on:click={exec} color="light">Run</Button>
    </Card>
    
</div>
