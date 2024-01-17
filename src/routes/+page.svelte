<script lang="ts">
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import axios from 'axios';
const API_KEY = "c611dcb7-e485-4572-a208-591a6c09e28b"; // API KEY HERE
    const sdxlURL = "https://urchin-app-ynpbq.ondigitalocean.app/api/text2image"
	let prompt = 'a usa girl'
	let image_url=''
	let costVnd = 0
    let jobId=''
    let verifyJobUrl=""
	async function GetImage(){
		image_url=''
		costVnd = 0
        const params={
  "model": "sd_xl_base_1.0.safetensors [be9edd61]",
  "prompt": prompt,
  "style": "3d-model",
  "width": 1024,
  "height": 1024
}
		axios.get(sdxlURL, {
            params: params})

  .then(function (response) {
    console.log(response.data);
    image_url=response.data
    // Remove "https://images.prodia.xyz/" and ".png"
    jobId = image_url.replace(/^https:\/\/images\.prodia\.xyz\//, '').replace(/\.png$/, '');
    verifyJobUrl = "https://api.prodia.com/v1/job/" + jobId
console.log(verifyJobUrl);
    axios.get(verifyJobUrl,{
    headers: {
        'X-Prodia-Key': API_KEY,
        'Accept': 'application/json',
        'Content-Type': 'application/json'
    }
})
.then((res) => console.log(res.data.status))
.catch((err) => console.error(err));


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
<h1>{image_url}</h1>
<img src={image_url} alt="theheai" />
{/if}

