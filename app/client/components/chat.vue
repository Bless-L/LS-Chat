<template>
	<div class="wrapper">
        <div class="msg_box">
            <p class="msg_box_p" v-for="msg in msgs">{{msg.user}} <span class="msg_box_date">({{msg.date}}):</span> {{msg.msg}}</p>
        </div>
        <div class="controls">
            <textarea id="messageInput" placeHolder="输入并发送" name="message" cols="30" rows="10" v-model="text"></textarea>
            <input type="button" value="SEND" class="send_btn" id="sBtn" @click="sendMsg">
        </div>
    </div>
</template>

<script>
	export default {
		data () {
			return {
				text: '',
				msgs: [],
			}
		},
		created() {
			socket.on('newMsg', (data) =>{
				this.disNewMsg(data.nickname, data.msg);
			})
		},
		methods: {
			sendMsg() {
				if (!this.text.trim()) {return};
				socket.emit('sendMsg', this.text);
				this.text = '';
			},
			disNewMsg(user, msg) {
				const date = new Date().toTimeString().substr(0,8);
				this.msgs.push({
					user,
					msg,
					date,
				});
			},
		}
	}
</script>

<style lang='scss'>
.wrapper {
	margin: 0 auto;
}
.msg_box {
	height: 300px;
	&_p {

	}
	&_date {
		color: #666;
	}
}
</style>