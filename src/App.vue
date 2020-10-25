<template>
<div id="app">
<img :src="gif">
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
				{ name: "do", src: "/assets/sounds/C.mp3", shortcut: "q", code: "81" },
				{ name: "do#", src: "/assets/sounds/Cdiez.mp3", shortcut: "z", code: "90" },
				{ name: "ré", src: "/assets/sounds/D.mp3", shortcut: "s", code: "83" },
				{ name: "ré#", src: "/assets/sounds/Ddiez.mp3", shortcut: "e", code: "69" },
				{ name: "mi", src: "/assets/sounds/E.mp3", shortcut: "d", code: "68" },
				{ name: "fa", src: "/assets/sounds/F.mp3", shortcut: "f", code: "70" },
				{ name: "fa#", src: "/assets/sounds/Fdiez.mp3", shortcut: "g", code: "71" },
				{ name: "sol", src: "/assets/sounds/G.mp3", shortcut: "y", code: "89" },
				{ name: "sol#", src: "/assets/sounds/Gdiez.mp3", shortcut: "h", code: "72"  },
				{ name: "la", src: "/assets/sounds/A.mp3", shortcut: "u", code: "85" },
				{ name: "la#", src: "/assets/sounds/Adiez.mp3", shortcut: "j", code: "74" },
				{ name: "si", src: "/assets/sounds/B.mp3", shortcut: "k", code: "85" },
				{ name: "do", src: "/assets/sounds/C.mp3", shortcut: "l", code: "76" }
			]
		}
	},
	mounted() {
		for (let i=0;i<this.notes.length;i++)
			this.shortcut(this.notes[i].shortcut,this.notes[i].src);
	},
	methods: {
		play(src) {
			this.x=document.createElement("AUDIO");
			this.x.setAttribute("src",src);
			this.x.autoplay=true;
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