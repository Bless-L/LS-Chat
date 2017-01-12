<template>
	<div class="history">
        <p class="num">{{num}} 人在线</p>
		<div class="msgs_wp">
			<p v-for="msg in msgs">{{ msg }}</p>
		</div>
    </div>
</template>

<script>
	export default {
		data () {
			return {
				num: 0,
				msgs: [],
			}
		},
		created() {
			socket.on('system', (data) =>{
				this.num = data.len;
				let msg = '';

				if (data.type === 'loginIn') {
					msg = `${data.nickname} 进入了聊天室`;
				}else if (data.type === 'loginOut') {
					msg = `${data.nickname} 离开了聊天室`;
				}
				msg && this.msgs.push(msg);
			})
		}
	}
</script>

<style lang='scss'>
.history {
	p {
		font-size: 14px;
	}
}
.msgs_wp {
	height: 200px;
	overflow: auto;
}
</style>