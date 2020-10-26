<template>
	<div id="app">
		<img :src="gif" :alt="gif">
		<button v-for="item in notes" :key="item.name" :id="item.name" @click="play(item.src)">
			{{ item.name }}
		</button>
	</div>
</template>
<script>
import { GiphyFetch } from '@giphy/js-fetch-api'
const gf = new GiphyFetch('hoc7Xw81iwUP2iewXhekupQznVmYDlHK')

export default {
	name: "App",
	data() {
		return {
			gif: "",
			notes: [
				{ name: "do", src: "/assets/sounds/C.mp3", shortcut: "q" },
				{ name: "do#", src: "/assets/sounds/C#.mp3", shortcut: "z" },
				{ name: "ré", src: "/assets/sounds/D.mp3", shortcut: "s" },
				{ name: "ré#", src: "/assets/sounds/D#.mp3", shortcut: "e" },
				{ name: "mi", src: "/assets/sounds/E.mp3", shortcut: "d" },
				{ name: "fa", src: "/assets/sounds/F.mp3", shortcut: "f" },
				{ name: "fa#", src: "/assets/sounds/F#.mp3", shortcut: "g" },
				{ name: "sol", src: "/assets/sounds/G.mp3", shortcut: "y" },
				{ name: "sol#", src: "/assets/sounds/G#.mp3", shortcut: "h"  },
				{ name: "la", src: "/assets/sounds/A.mp3", shortcut: "u" },
				{ name: "la#", src: "/assets/sounds/A#.mp3", shortcut: "j" },
				{ name: "si", src: "/assets/sounds/B.mp3", shortcut: "k" },
				{ name: "do", src: "/assets/sounds/C.mp3", shortcut: "l" }
			]
		}
	},
	mounted() {
		for (let i=0;i<this.notes.length;i++)
			this.shortcut(this.notes[i].shortcut,this.notes[i].src);
	},
	methods: {
		play(src) {
			this.audio=document.createElement("AUDIO");
			this.audio.setAttribute("src",encodeURIComponent(src));
			this.audio.autoplay=true;
			this.emoji();
		},
		shortcut(key,src) {
			window.addEventListener('keydown', (event) => {
				event.preventDefault();
				const keyName = event.key;
				if (keyName == key) {
					this.play(src);
				}
			});
		},
		async emoji() {
			const { data : gif } = await gf.random()
			this.gif=gif.images.fixed_width.webp;
		}
	}
}

</script>