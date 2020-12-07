<template>
	<div class="wrapper-popup" :class="getClassPopup">
		<div class="rule">
			<h3>Luật chơi</h3>
			<p>Đôi khi, trong cuộc sống, có những thời điểm mà tất cả mọi thứ đều dường như chống lại bạn, đến nỗi bạn có cảm tưởng mình ko thể chịu đựng thêm một phút nào nữa. Nhưng hãy cố đừng buông xuôi và bỏ cuộc, vì sớm muộn gì mọi thứ rồi cũng sẽ thay đổi.</p>
			<button @click="confirm()" class="confirm">Đã hiểu</button>
		</div>
	</div>
</template>
<script type="text/javascript">
	export default{
		name : 'popup-rule',
		props:{
			isOpenPopup:{}
		},
		methods:{
			confirm(){
				this.$emit('handleConfirm');
			}
		},
		computed:{
			getClassPopup:function(){
				return {
					'open-popup' : this.isOpenPopup
				}
			}
		}
	}
</script>
<style type="text/css">
	.wrapper-popup{
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: rgba(0,0,0,0.4);
		opacity: 0;
		visibility: hidden;
	}
	.wrapper-popup.open-popup{
		opacity: 1;
		visibility: visible;
	}
	.rule{
		position: absolute;
		background: #fff;
		width: 350px;
		top: 50%;
		left: 50%;
		transform: translate(-50%,-50%) scale(1.2);
		padding: 20px;
		transition: all .3s ease;
	}
	.rule h3{
		margin-bottom: 10px;
	}
	.rule .confirm{
		border: 2px solid #333;
		background-color: #fff;
		margin-top: 20px;
		cursor: pointer;
		padding: 8px 15px;
		transition: all .3s ease;
	}
	.rule .confirm:hover{
		color: #fff;
		background-color: #333;
	}
	.open-popup .rule{
		transform: translate(-50%,-50%) scale(1);
	}
	/* Kết hợp css3 với vuejs để xây dựng hiệu ứng zôm in - zoom out*/
</style>