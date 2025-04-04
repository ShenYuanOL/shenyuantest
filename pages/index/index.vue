<template>
	<view class="main" :style="{height:btom}">
		<view class="chat">
			<scroll-view class="message-list" scroll-y :scroll-into-view="scrollIntoViewId" @scrolltoupper="handleRefresh"
				:refresher-enabled="true" :refresher-triggered="isRefreshing" @refresherrefresh="onPullDownRefresh">
				<!-- 下拉刷新提示 -->
				<view v-if="isRefreshing" class="refresh-tip">正在刷新...</view>
	
				<!-- 消息内容 -->
				<view v-for="(msg, index) in messages" :key="index" :id="'msg-' + index" class="message-item">
					<view :class="['message-bubble', msg.isUser ? 'user-message' : 'other-message']">
						{{ msg.content }}
					</view>
				</view>
				<view class="message-item">
					<view class="frist-message">
						<up-avatar class="avatar" src="../../static/1.jpg" size="54"></up-avatar>
						<view class="text">您好，智能客服助手为您服务</view>
					</view>
					<view class="tips-message">
						<view>正在转接中，人工客服马上为您服务</view>
						<view>您可以先描述问题哦~</view>
					</view>
				</view>
				<view class="message-item user-area">
					<view class="product-item-message">
						<view class="card-top">
							<up-avatar src="../../static/1.jpg" shape="square" size="70"></up-avatar>
							<view class="info">
								<view class="name">十月稻田 黄金玉米段 1.6斤（8段） 黄糯aaaa1111232132131232131211aa</view>
								<view class="pirce">￥200.00</view>
							</view>
						</view>
						<view class="card-bottom">
							<view class="text">7天无理由退款 30天只换不修</view>
							<up-icon name="arrow-right" size="12"></up-icon>
						</view>
					</view>
				</view>
				<view class="message-item">
					<view class="service-message">
						亲亲，您的眼光真的是太棒了<br>【飞利浦电视 焕新购】<br> 32时6590 下单到手不高于558元<br>【补】领取国补下单再打8.5折，到手474.3元
						<br>【赠】晒单赠20元京东E卡(2图+20文字) <br>【送】只换不修服务
					</view>
				</view>
				<view class="message-item user-area">
					<view class="user-message">
						您好，这东东质保期有多久呢?
					</view>
				</view>
				<view class="message-item">
					<view class="tips-message">
						<view>昨天 12:30</view>
					</view>
				</view>
				<view class="message-item">
					<view class="tips-message">
						<view>很久没有收到您的回复，如已解决问题，请为我评价</view>
					</view>
				</view>
				<view class="message-card">
					<view class="evaluate-card">
						<up-grid col="5">
							<view class="item" v-for="(item, index) in ratings" :key="index"
								@click="handleRatingClick(index)">
								<up-avatar :src="selectedRating === index ? ratingImages[index] : item.src"
									size="34"></up-avatar>
								<view class="text">{{ item.text }}</view>
							</view>
						</up-grid>
						<up-divider textColor="#333333" lineColor="#E4E4E4" text="问题是否解决"></up-divider>
						<view class="solve-btns">
							<view class="btn" :class="{ active: activeButton === '已解决' }" @click="handleButtonClick('已解决')">
								已解决
							</view>
							<view class="btn" :class="{ active: activeButton === '未解决' }" @click="handleButtonClick('未解决')">
								未解决
							</view>
						</view>
						<view class="opinion">
							<up-textarea v-model="value1" placeholder="您有任何想说的，都可以告诉我们" count maxlength="200" height="76px"
								placeholderStyle="color: #CACACA;font-size:12px;"></up-textarea>
						</view>
						<view class="submit-btn">提交评价</view>
					</view>
				</view>
			</scroll-view>
		</view>
		<view class="input">
			input
		</view>
	</view>
</template>

<script>
export default {
  data() {
    return {
      btom: "",//自动获取可视区域的高度
      messages: [
        { content: "你好！", isUser: false },
        { content: "有什么可以帮你的吗？", isUser: false },
      ], // 消息列表
      newMessage: "", // 当前输入的消息
      scrollIntoViewId: "", // 滚动到最新消息的 ID
      isRefreshing: false, // 是否正在刷新
      selectedRating: null, // 当前选中的评分项索引
      ratings: [
        { src: "../../static/icon/feichangbuman.png", text: "非常不满意" },
        { src: "../../static/icon/buman.png", text: "不满意" },
        { src: "../../static/icon/yiban.png", text: "一般" },
        { src: "../../static/icon/manyi.png", text: "满意" },
        { src: "../../static/icon/feichngmanyi.png", text: "非常满意" },
      ],
      ratingImages: [
        "../../static/icon/feichangbumandianji.png",
        "../../static/icon/bumandianji.png",
        "../../static/icon/yibandianji.png",
        "../../static/icon/manyidianji.png",
        "../../static/icon/feichngmanyidianji.png",
      ],
      activeButton: "已解决", // 当前激活的按钮
    }
  },
  mounted() {
    this.btom = uni.getWindowInfo().windowHeight + "px"
    console.log(this.btom);
  },
  methods: {
    handleRatingClick(index) {
      this.selectedRating = index;
    },
    handleButtonClick(buttonText) {
      this.activeButton = buttonText;
    },
  },
}

</script>
<style lang="scss" scoped>
.chat {
	height: 90%;

	.message-list {
		flex: 1;
		overflow-y: auto;
		padding: 12px;
		background-color: #f5f5f5;
		height: 100%;
		width: calc(100% - 24px);
		// 动态计算聊天区域的高度

		.message-item {
			margin: 10px 0;

			.message-bubble {
				max-width: 80%;
				padding: 11px;
				border-radius: 6px;
				font-size: 18px;
				line-height: 1.5;
			}

			.service-message {
				max-width: 80%;
				background-color: white;
				padding: 10px;
				border-radius: 8px;
				font-size: 14px;
				color: #333333;
			}

			.user-message {
				max-width: 80%;
				background-color: #FFEBEB;
				padding: 10px;
				border-radius: 8px;
				font-size: 14px;
				color: #333333;
			}

			.other-message {
				align-self: flex-start;
				background-color: #fff;
				color: #333;
				box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
			}

			.frist-message {
				height: 54px;
				position: relative;
				display: flex;
				flex-direction: column-reverse;

				.avatar {
					position: absolute;
					top: 0;
					left: 0;
					border-radius: 50%;
					background-color: #fff;
					box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
				}

				.text {
					margin-left: 20px;
					padding: 11px 11px 11px 50px;
					border-radius: 6px;
					font-size: 12px;
					line-height: 1.5;
					align-self: flex-start;
					background-color: #fff;
					color: #333333;
					box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
				}
			}

			.tips-message {
				margin: 18px 0;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: center;
				gap: 10px;
				font-size: 11px;
				color: #666666;
			}

			.product-item-message {
				width: 78%;
				background-color: white;
				padding: 10px;
				border-radius: 8px;

				.card-top {
					display: flex;
					flex-direction: row;
					align-items: start;

					.info {
						margin-left: 10px;
						display: flex;
						flex-direction: column;
						justify-content: space-between;
						width: 100%;

						.name {
							font-size: 14px;
							color: #333;
							overflow: hidden;
							text-overflow: ellipsis;
							display: -webkit-box;
							-webkit-line-clamp: 2;
							-webkit-box-orient: vertical;
						}

						.pirce {
							font-size: 13px;
							color: #C83F24;
						}
					}
				}

				.card-bottom {
					display: flex;
					flex-direction: row;
					align-items: center;
					justify-content: space-between;
					margin-top: 10px;
					font-size: 14px;
					color: #C87224;
				}
			}

		}

		.message-card {
			width: calc(100% - 22px);

			.evaluate-card {
				width: 100%;
				background-color: #FFFFFF;
				border-radius: 8px;
				padding: 16px 11px;

				.item {
					display: flex;
					flex-direction: column;
					align-items: center;
					justify-content: center;
					padding: 16px 11px;
					font-size: 10px;
					color: #999999;

					.text {
						margin-top: 12px;
					}
				}

				.solve-btns {
					display: flex;
					flex-direction: row;
					justify-content: center;
					margin-top: 20px;
					gap: 20px;

					view {
						padding: 6px 33px;
						border-radius: 8px;
						font-size: 14px;
						color: #FFFFFF;
						margin: 0;
						background-color: #F5F5F5;
						border: 1px solid #E0E0E0;
					}

					.active {
						background-color: #C83F24;
						border: 1px solid #C83F24;
					}
				}

				.opinion {
					margin-top: 16px;
				}

				.submit-btn {
					margin-top: 10px;
					padding: 7px 0;
					text-align: center;
					border-radius: 8px;
					font-size: 14px;
					color: #FFFFFF;
					background-color: #C83F24;
				}

				.submit-btn:active {
					background-color: #ad3017;
				}
			}
		}

		.user-area {
			display: flex;
			flex-direction: row-reverse;
		}
	}
}

.input {
	background-color: wheat;
}
</style>