<template>
	<div class="login_wp" v-show="unLogin">
		<div class="login">
			<p>你的名字是：</p>
			<div class="login_input">
				<input type="text" v-model="name" id="name">
				<button @click="save">确定</button>
			</div>
            <p>{{msg}}</p>
		</div>
        <div class="login_shade"></div>
    </div>
</template>

<script>
	export default {
		data() {
			return {
				name: '',
                unLogin: true,
                msg: '',
			}
		},
        created() {
            socket.on('login_cb',(type) =>{
                if (type === 'success') {
                    this.unLogin = false;
                }else if (type === 'fail') {
                    this.msg = `这个昵称已经有人使用过了，请换一个`;
                    this.name = '';
                    document.getElementById('name').focus();
                }
            })
        },
		methods: {
			save() {
                if (!this.name.trim()) {return};
				socket.emit('login', this.name);
			}
		}
	}
</script>

<style lang='scss'>
.login_shade {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-color: rgba(0,0,0,.4);
    z-index: 0;
}
.login {
	position: absolute;
	top: 20%;
	left: 50%;
	transform: translate3d(-50%,0,0);
    z-index: 1;
	p {
		color: #fff;
	}
}
</style>