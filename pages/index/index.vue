<template>
	<view class="welife">
		<view class="close_voice" :class="audioStatu == '' ? '' : 'voiceclose'" @tap="onPauseVoice"></view>
		<view class="bg_img"></view>
		<view class="canvas">
			<text class="first">
				人这一生，会走过许多路。
			</text>
		</view>
	</view>
</template>

<script>
	var audio = null;
	export default {
		
		data() {
			return {
				audio: {
					src: 'http://isure.stream.qqmusic.qq.com/C400003yNMwO2lJpNX.m4a?guid=5892439010&vkey=718AAFBCBABA6F8D90C75DE721655E1B4C805BA0BB3E595686BF180CDFD47172E6EC4248402518EB85084DD2DC5B874A26B93106A1F40826&uin=3606&fromtag=66'
				},
				audioStatu: ''
			}
		},
		onLoad() {
			var _self = this;
			audio = uni.createInnerAudioContext()
			audio.autoplay = true;
			audio.src = this.audio.src;
			audio.onPlay(function(){
				_self.audioStatu = ''
			})
			audio.onPause(function(){
				_self.audioStatu = 'voiceclose'
			})
			audio.onError((res) => {
				uni.showToast({
					icon: 'none',
					title: '声音播放失败',
					duration: 1500
				})
			  console.error(res.errMsg + '声音播放失败！');
			  console.log(res.errCode);
			});
			
		},
		methods: {
			onPauseVoice(res){
				if(this.audioStatu == ''){
					audio.pause()
				}
				if(this.audioStatu == 'voiceclose'){
					audio.play()
				}
				
			}
		}
		
	}
</script>

<style lang="less">
	.welife{
		position: fixed;
		width: 100%;
		height: 100%;
		background: #000;
		>view{
			background-size: 100% 100% !important;
		}
		.close_voice{
			width: 60upx;
			height: 60upx;
			max-width: 60px;
			max-height: 60px;
			position: absolute;
			top: 50upx;
			right: 50upx;
			//border-radius: 50%;
			font-size: 0;
			background: url(~@/static/shengyin.png) center no-repeat;
			animation: roll linear 5s infinite;
			z-index: 999;
		}
		.voiceclose{
			background: url(~@/static/novoice.png) center no-repeat;
		}
		.bg_img{
			position: fixed;
			width: 100%;
			height: 100%;
			top: 0;
			left: 0;
			background: url(~@/static/img/timg.jpg) center no-repeat;
			background-size: 100%;
			z-index: 1;
			animation: buling 10s ease-in-out infinite;
		}
		.canvas{
			position: fixed;
			width: 100%;
			height: 100%;
			top: 0;
			left: 0;
			z-index: 99;
			.first{
				opacity: 0;
				font-size: 36upx;
				display: block;
				padding-left: 100upx;
				margin-top: 120upx;
				color: cornsilk;
				animation:  hideshow 20s linear;
			}
		}
			
	}
	//全部动画
	@keyframes roll{
		from{
			transform: rotate(0deg)
		}
		to{
			transform: rotate(360deg)
		}
	}
	@keyframes buling{
		0%{
			opacity: 1;
		}
		50%{
			opacity: .2
		}
		100%{
			opacity: 1;
		}
	}
	@keyframes hideshow{
		0%{
			opacity: 0
		}
		25%{
			opacity: .75
		}
		50%{
			opacity: 1
		}
		100%{
			opacity: .2
		}
	}
</style>
