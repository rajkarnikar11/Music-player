<template>
	<div class="music" id="id">
		<header><h1>My Music</h1></header>
		<main>
			<section class="player">
				<div class="song-title__container">
					<h2 class="song-title">
						{{ current.title }}
					</h2>
					<img
						class="music-icon"
						height="180"
						width="180"
						:class="isPLaying && 'music-icon--active'"
						src="./assets/music.png"
					/>
				</div>

				<p class="song-artist">{{ current.artist }}</p>
				<div class="controls">
					<button @click="prev" class="prev">
						<img
							height="15"
							width="15"
							class="prev__icon"
							src="./assets/previous.svg"
						/>
					</button>

					<button v-if="!isPLaying" @click="playMusic" class="play">
						<img
							height="15"
							width="15"
							class="prev__icon"
							src="./assets/playIcon.svg"
						/>
					</button>
					<button v-else @click="pauseMusic" class="pause">
						<img
							height="15"
							width="15"
							class="prev__icon"
							src="./assets/pause.svg"
						/>
					</button>

					<button class="next" @click="next">
						<img
							height="15"
							width="15"
							class="prev__icon"
							src="./assets/next.svg"
						/>
					</button>
				</div>
			</section>
		</main>
	</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			current: {},
			index: 0,
			isPLaying: false,
			songs: [
				{
					title: "One",
					artist: "Metallica",
					src: require("./assets/1.mp3"),
				},
				{
					title: "Notthing Else Matters",
					artist: "Metallica",
					src: require("./assets/n1.mp3"),
				},
				{
					title: "Wind of Change",
					artist: "Scorpions",
					src: require("./assets/s1.mp3"),
				},
			],
			player: new Audio(),
		};
	},
	methods: {
		playMusic() {
			this.isPLaying = true;
			this.player.play();
			console.log(this.isPLaying);
		},
		pauseMusic() {
			this.isPLaying = false;
			this.player.pause();
			console.log(this.isPLaying);
		},
		next() {
			this.player.pause();

			if (this.index < this.songs.length - 1) {
				this.index++;
			} else {
				this.index = 0;
			}
			this.current = this.songs[this.index];
			this.player.src = this.current.src;
			this.player.play();
			this.isPLaying = true;

			console.log(this.index);
		},
		prev() {
			this.player.pause();

			if (this.index <= 0) {
				this.index = this.songs.length - 1;
			} else {
				this.index--;
			}
			this.current = this.songs[this.index];
			this.player.src = this.current.src;
			this.player.play();
			this.isPLaying = true;

			console.log(this.index);
		},
	},
	created() {
		this.current = this.songs[this.index];
		this.player.src = this.current.src;
		console.log(this.songs.length);
		console.log(this.index);
		// this.player.play();
	},
};
</script>

<style lang="scss">
* {
	margin: 0;
	padding: 0;
	font-family: sans-serif;
	box-sizing: border-box;
}
body {
}

.prev__icon {
	fill: white;
}
.music {
	max-width: 500px;
	margin: auto;
	background-color: #171717;

	color: white;
	text-align: center;
}
header {
	padding: 15px;
	background-color: black;
	box-shadow: 0 3px 15px silver;
}
.song-title__container {
	// outline: 1px solid red;
	height: 400px;
	position: relative;
}
.music-icon {
	position: absolute;
	bottom: 20px;
	left: 50%;
	transform: translateX(-50%);
	opacity: 0.7;

	&--active {
		opacity: 1;
		-webkit-filter: drop-shadow(0px 0px 10px rgb(255, 255, 255, 0.8));
		filter: drop-shadow(0px 0px 15px rgb(255, 255, 255, 0.8));
	}
}
.song-title {
	margin-top: 20px;

	font-weight: 900;
	font-size: 55px;
	text-shadow: 3px 3px silver;
	-webkit-text-stroke: 1px rgb(23, 23, 23, 0.5);
}
song-title--active .song-artist {
	font-weight: 200;
	font-style: italic;
	letter-spacing: 5px;
	margin-bottom: 20px;
}
.controls {
	display: flex;
	width: 50%;
	margin: auto;
	justify-content: space-between;
	padding: 20px;
	& button {
		background-color: black;
		color: white;
		padding: 10px;
		border-radius: 100%;
		cursor: pointer;
		transition-duration: 0.3s;
		position: relative;
		display: flex;
		justify-content: center;
		height: 50px;
		width: 50px;
		align-items: center;
		border-top: 3px solid grey;
		&:hover {
			box-shadow: 0px 0px 5px silver;
			border: 3px solid grey;
		}
		& img {
			opacity: 0.7;
			&:hover {
				opacity: 1;
			}
		}
	}
}
</style>
