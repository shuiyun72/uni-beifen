<template>
	<view class="xiaoxi">
		<uni-collapse :accordion="true" @change="changeItem">
			<sy-collapse-item v-for="item in accordion" :key="item.id" :title="item.title" :show-animation="item.animation"
			 :thumb="item.thumb" :number="item.number" :open='true' class="sy_collapse_item">
				<view class="xiaoxi_body">
					<!-- <view class="title">
						{{titleName}}
					</view> -->
					<view class="xiaoxi_list" v-if="titleName == '到货提醒'">
						<view class="item_daohuo" v-for="item in xiaoxiListCC">
							<view class="time">
								{{getDateL(item.time)}}
							</view>
							<view class="box">
								<view class="c_title">
									{{item.title}}
								</view>
								<view class="content_flex">
									<image src="../../static/img/img-sp19.png" class="c_img" mode=""></image>
									<view class="content">
										{{item.content}}
									</view>
								</view>
							</view>
						</view>
					</view>
					<view class="xiaoxi_list" v-if="titleName == '系统消息' || titleName == '订单消息'">
						<view class="item" v-for="item in xiaoxiListCC">
							<view class="time">
								{{getDateL(item.time)}}
							</view>
							<view class="box">
								<view class="c_title">
									{{item.title}}
								</view>
								<view class="content">
									{{item.content}}
								</view>
							</view>
						</view>
					</view>
				</view>
			</sy-collapse-item>
		</uni-collapse>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				xiaoxiListCC:[],  //展示消息
				
				xiaoxiListDD: [{  //订单消息
					time: "2020-05-17",
					title: "订单退款已受理 : 99854456564658474",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}, {
					time: "2020-05-17",
					title: "订单已受理 : 99854456564658474",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}, {
					time: "2020-05-17",
					title: "订单配送中 : 99854456564658474",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}],
				xiaoxiListDH: [{  //到货消息
					time: "2020-05-17",
					title: "商品已到货",
					content: "南非进口橙子17:50到货南非进口橙子17:50到货南非进口橙子17:50到货"
				}, {
					time: "2020-05-17",
					title: "商品已到货",
					content: "南非进口橙子17:50到货南非进口橙子17:50到货南非进口橙子17:50到货"
				}],
				xiaoxiListXT: [{  //系统消息
					time: "2020-05-17",
					title: "系统消息",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}, {
					time: "2020-05-17",
					title: "系统消息",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}, {
					time: "2020-05-17",
					title: "系统消息",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}, {
					time: "2020-05-17",
					title: "系统消息",
					content: "消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容消息内容"
				}],
				firstTitle: "系统消息",
				xiaoxiList: [{
					time: ""
				}],
				accordion: [{
						id: 1,
						title: '订单消息',
						content: '手风琴效果',
						animation: true,
						thumb: "../../static/img/mine/dingdxx.png",
						number: 1
					},
					{
						id: 2,
						title: '到货提醒',
						content: '手风琴效果',
						animation: true,
						thumb: "../../static/img/mine/daohtx.png",
						number: 2
					},
					{
						id: 3,
						title: '系统消息',
						content: '手风琴效果',
						animation: true,
						thumb: "../../static/img/mine/daohtx.png",
						number: 6
					}
				],
				titleName:""
			};
		},
		mounted() {
			this.changeItem([2]);
		},
		onPullDownRefresh() {
			//监听下拉刷新动作的执行方法，每次手动下拉刷新都会执行一次
			let this_ = this;
			setTimeout(function() {
				if(this_.titleName == "订单消息"){
					this_.changeItem([0]);
				}else
				if(this_.titleName == "到货提醒"){
					this_.changeItem([1]);
				}else
				if(this_.titleName == "系统消息"){
					this_.changeItem([2]);
				}
				uni.stopPullDownRefresh(); //停止下拉刷新动画
			}, 1000);
		},
		methods: {
			changeItem(el) {
				console.log(el)
				if(el[0] == 0){
					this.titleName = "订单消息"
					this.xiaoxiListCC = this.xiaoxiListDD
				}else
				if(el[0] == 1){
					this.titleName = "到货提醒"
					this.xiaoxiListCC = this.xiaoxiListDH
				}else
				if(el[0] == 2){
					this.titleName = "系统消息"
					this.xiaoxiListCC = this.xiaoxiListXT
				}
				
			},
			getDateL(date){
				return this.$getDate(date,'年-月-日')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.sy_collapse_item {
		background-color: #fff;

		.xiaoxi_body {
			background-color: #f0f0f0;

			.title {
				font-size: 36upx;
				text-align: center;
				padding: 40upx 0 20upx;
				font-size: bold;
				color: #333;
			}
			.xiaoxi_list {
				padding: 20upx 26upx;
				.item_daohuo{
					padding-bottom: 30upx;
					.time {
						color: #666;
						text-align: center;
						padding-bottom: 20upx;
					}
					
					.box {
						background-color: #fff;
						padding: 20upx 26upx 40upx;
						border-radius: 20upx;
						color: #666;
					
						.c_title {
							font-size: 36upx;
							text-align: center;
							padding-bottom: 20upx;
						}
						.content_flex{
							display: flex;
							align-items: center;
							.c_img{
								width: 90upx;
								height: 90upx;
								flex-shrink: 0;
							}
							.content{
								padding: 0 30upx;
							}
						}
						.content {
							font-size: 30upx;
						}
					}
				}
				.item {
					padding-bottom: 30upx;
					.time {
						color: #666;
						text-align: center;
						padding-bottom: 20upx;
					}

					.box {
						background-color: #fff;
						padding: 20upx 26upx 40upx;
						border-radius: 20upx;
						color: #666;

						.c_title {
							font-size: 36upx;
							text-align: center;
							padding-bottom: 20upx;
						}

						.content {
							font-size: 30upx;
						}
					}
				}
			}
		}
	}
</style>
