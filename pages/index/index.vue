<template>
	<view class="content">
		<view class="top">
			<up-row>
				<up-col span="8">
					<view class="user-card">
						<up-avatar src="../../static/1.jpg" size="60"></up-avatar>
						<view class="info">
							<view class="name">MR.懵</view>
							<up-tag type="warning" shape="circle" bgColor="#ef7d7f" icon="star" size="mini">中品维度会员</up-tag>
						</view>
					</view>
				</up-col>
				<up-col span="4">
					<view class="btns">
						<up-icon name="kefu-ermai" color="#fff" size="30"></up-icon>
						<up-icon name="photo" color="#fff" size="30"></up-icon>
						<up-icon name="setting" color="#fff" size="30"></up-icon>
					</view>
				</up-col>
			</up-row>
		</view>
		<view class="num-box">
			<up-row class="card">
				<up-col span="6" class="item box">
					<view class="num">750</view>
					<view class="title">余额</view>
				</up-col>
				<up-col span="6" class="item">
					<view class="num">0</view>
					<view class="title">积分</view>
				</up-col>
			</up-row>
			<view class="warning"><up-icon name="warning" color="#895331" size="20"></up-icon>{{warning}}</view>
		</view>
		<view class="shopping-cart">
			<view class="item">
				<up-icon name="bag" size="70"></up-icon>
				<view class="title">待付款</view>
			</view>
			<view class="item">
				<up-icon name="bag" size="70"></up-icon>
				<view class="title">待发货</view>
			</view>
			<view class="item">
				<up-icon name="bag" size="70"></up-icon>
				<view class="title">待结算</view>
			</view>
			<view class="item">
				<up-icon name="bag" size="70"></up-icon>
				<view class="title">待评价</view>
			</view>
			<view class="item">
				<up-icon name="bag" size="70"></up-icon>
				<view class="title">全部</view>
			</view>
		</view>
		<view class="anc">
			<view class="box">
				<up-icon name="volume" size="20"></up-icon>
				<up-icon name="volume" size="30" class="img"></up-icon>
				<up-notice-bar :icon="false" bgColor="#fff" :text="anc" direction="column"></up-notice-bar>
			</view>
		</view>
		<view class="function-group">
			<up-grid :border="false" :col="5">
				<up-grid-item v-for="i in 10" :key="i">
					<up-icon name="bag" size="70"></up-icon>
					<view class="title">全部</view>
				</up-grid-item>
			</up-grid>
		</view>
		<view class="other-function">
			<up-row>
				<up-col span="6">
					<view class="item">申请分平台服务商</view>
				</up-col>
				<up-col span="6">
					<view class="item">申请分平台服务商</view>
				</up-col>
			</up-row>
		</view>
	</view>
</template>

<script>
export default {
  data() {
    return {
      title: 'Hello',
      warning: '未绑定中品一号会员账号，同步积分可抵扣订单金额。',
      anc: [
        '中品一号会员，可享受会员折扣，积分抵扣，返现等优惠1。',
        '中品一号会员，可享受会员折扣，积分抵扣，返现等优惠2。',
        '中品一号会员，可享受会员折扣，积分抵扣，返现等优惠3。'
      ]
    }
  },
  onLoad() {

  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
body {
	background-color: #e4e4e4;
}

.content {
	padding: 15px;
	position: relative;
}

.content::before {
	content: '';
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 120px;
	background-color: #db2729;
	z-index: -1;
}

.top {
	background-color: #db2729;

	.user-card {
		display: flex;
		flex-direction: row;
		align-items: center;

		.info {
			margin-left: 10px;
			display: flex;
			flex-direction: column;
		}

		.name {
			font-size: 16px;
			margin: 3px 0;
		}


	}

	.btns {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-around;
	}
}

.num-box {
	margin-top: 10px;
	background-color: #fff;
	padding-top: 10px;
	border-radius: 15px;

	.card {
		margin-bottom: 10px;

		.item {
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			padding: 16px 0;

			.num {
				text-align: center;
				font-size: 34px;
				font-weight: bold;
				margin-bottom: 5px;
			}

			.title {
				margin-top: 8px;
				text-align: center;
				font-size: 16px;
				color: #999;
			}
		}

		.box {
			border-right: 1px solid #eee;
		}
	}

	.warning {
		display: flex;
		flex-direction: row;
		font-size: 13px;
		color: #999;
		align-items: center;
		margin-top: 10px;
		color: #895235;
		background-color: #ecc59b;
		padding: 4px 5px;
		border-radius: 0 0 15px 15px;
	}
}

.shopping-cart {
	margin-top: 10px;
	background-color: #fff;
	border-radius: 15px;
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content: space-around;

	.item {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 6px 0;

		.title {
			text-align: center;
			font-size: 14px;
			color: #999;
		}
	}
}

.anc {
	margin-top: 10px;
	background-color: #fff;
	border-radius: 15px;
	padding: 10px;

	.box {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
	}

	.img {
		margin: 0 3px;
	}
}

.function-group {
	margin-top: 10px;
	background-color: #fff;
	border-radius: 15px;
	padding: 10px;
}

.other-function {
	margin-top: 10px;

		.item {
			background-color: #fff;
			border: 1px solid #eee;
			text-align: center;
			padding: 70px 0;
			margin: 10px;
		}

}
</style>
