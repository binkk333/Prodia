<script lang="ts">
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import axios from 'axios';
const API_KEY = "c611dcb7-e485-4572-a208-591a6c09e28b"; // API KEY HERE
    const sdxlURL = "https://api.prodia.com/v1/sdxl/generate"
	let prompt = 'a usa girl'
	let image_url=''
	let costVnd = 0
	async function GetImage(){
		image_url=''
		costVnd = 0
        const body={
  "model": "dreamshaperXL10_alpha2.safetensors [c8afe2ef]",
  "prompt": "a muscle mouse",
  "style_preset": "3d-model",
  "steps": 20,
  "width": 1024,
  "height": 1024
}
		axios.post(sdxlURL,body, {
  headers: {
    'Accept':'application/json',
    'content-type': 'application/json',
    'X-Prodia-Key': API_KEY
  }})

  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
}

</script>
<h1>sdxl</h1>
{#if costVnd != 0}
<h1>Cost VND = {costVnd}</h1>
{/if}
<LightSwitch/>
<h1>stable-diffusion</h1>
<input type="text" bind:value={prompt}>
<button on:click={GetImage}>Send to get Image</button>

{#if image_url != ''}
<img src="data:image/png;base64,{image_url}" alt="theheai" />
{/if}

