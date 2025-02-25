<template>
	<view class="content">
		<view class="header">
			<view class="title">{{ title }}</view>
			<view class="state-badge" :class="{'state-connected': state === '已连接'}">
				<text class="state-text">服务状态： {{ state }}</text>
			</view>
		</view>
		
		<view class="button-container">
			<view class="button-group">
				<view class="group-title">卡片操作</view>
				<button class="button" @click="openCpuCard">激活非接CPU卡</button>
				<button class="button" @click="openMemoryCard">激活非接存储卡</button>
				<button class="button" @click="closeCard">关闭卡片</button>
			</view>
			
			<view class="button-group">
				<view class="group-title">存储卡功能</view>
				<button class="button" @click="memoryCardAuthEntication">验证非接存储卡</button>
				<button class="button" @click="memoryCardReadData">非接存储卡读数据</button>
				<button class="button" @click="memoryCardReadDataVal">非接存储卡读值</button>
			</view>
			
			<view class="button-group">
				<view class="group-title">其他功能</view>
				<button class="button" @click="sendCommand">发送交互命令</button>
				<button class="button" @click="beep">BEEP</button>
				<button class="button" @click="getEMID">获取EMID</button>
				<button class="button" @click="getJRICCardInfo">获取金融IC卡信息</button>
				<button class="button" @click="getSiCardBaseInfo">获取社保卡信息</button>
			</view>
		</view>
		
		<view class="footer">
			<text>Copyright © BSF 2025</text>
			<text class="link" @click="openUrl">https://byteee.fund</text>
		</view>
	</view>
</template>

<script>
	import * as IdcardManager from "../../uni_modules/bsf-sunmi-idcard";
	
	export default {
		data() {
			return {
				title: "bsf-sunmi-idcard演示工程",
				state: '未连接'
			}
		},
		onLoad() {
			// 绑定服务
			IdcardManager.bindIDCardService({
				onConnected() {
					this.state = "已连接"
				},
				onDisConnected() {
					this.state  = "已断开"
				}
			});
		},
		onUnload() {
			// 卸载服务
			IdcardManager.unbindIDCardService();
		},
		methods: {
			sendCommand () {
				IdcardManager.sendCommand({
					command: "01020304",
					success:(res)=> {
						console.log("获取到EMID", res);
					},
					fail:(res)=> {
						console.log("获取到EMID失败",res)
					}});
			},
			closeCard () {
				IdcardManager.closeCard({
					success:(res)=> {
						console.log("关闭成功");
					},
					fail:(res)=> {
						console.log("关闭失败",res)
					}});
			},
			openMemoryCard () {
				IdcardManager.openMemoryCard({
					success:(res)=> {
						console.log("激活成功", res);
					},
					fail:(res)=> {
						console.log("激活失败",res)
					}});
			},
			openCpuCard () {
				IdcardManager.openCpuCard({
					success:(res)=> {
						console.log("激活成功",res);
					},
					fail:(res)=> {
						console.log("激活失败",res)
					}});
			},
			memoryCardAuthEntication() {
				// mode 0-KEYA模式;1-KEYB模式
				IdcardManager.memoryCardAuthEntication({
					mode: 0,
					addr: 4,
					key: "FFFFFFFFFFFF",
					success:(res)=> {
						console.log("验证结果",res);
					},
					fail:(res)=> {
						console.log("验证失败",res)
					}});
			},
			memoryCardReadData () {
				IdcardManager.memoryCardReadData({
					addr: 0,
					success:(res)=> {
						console.log("读取结果",res);
					},
					fail:(res)=> {
						console.log("读取失败",res)
					}});
			},
			memoryCardReadDataVal () {
				IdcardManager.memoryCardReadDataVal({
					addr: 0,
					success:(res)=> {
						console.log("读取结果",res);
					},
					fail:(res)=> {
						console.log("读取失败",res)
					}});
			},
			getJRICCardInfo () {
				IdcardManager.getJRICCardInfo({
					success:(cardno, name)=> {
						console.log(cardno, name);
					},
					fail:(res)=> {
						console.log("获取失败", res)
					}})
			},
			getSiCardBaseInfo () {
				IdcardManager.getSiCardBaseInfo({
					success:(res)=> {
						console.log(cardno, name);
					},
					fail:(res)=> {
						console.log("获取失败", res)
					}})
			},
			getEMID() {
				IdcardManager.getEMID({
					success:(res)=> {
						console.log("获取到EMID", res);
					},
					fail:(res)=> {
						console.log("获取到EMID失败",res)
					}});	
			},
			beep () {
				IdcardManager.beep(5);
			},
			openUrl() {
				// #ifdef APP-PLUS
				plus.runtime.openURL('https://byteee.fund', (err) => {
					if (err) {
						uni.showToast({
							title: '打开链接失败',
							icon: 'none'
						});
					}
				});
				// #endif
				
				// #ifdef H5
				window.open('https://byteee.fund', '_blank');
				// #endif
			},
		}
	}
</script>

<style scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: flex-start;
		padding: 30rpx;
		min-height: 100vh;
		background-color: #f5f6fa;
	}

	.header {
		width: 100%;
		text-align: center;
		margin-bottom: 40rpx;
	}

	.title {
		font-size: 40rpx;
		color: #2c3e50;
		font-weight: bold;
		margin-bottom: 20rpx;
	}

	.state-badge {
		display: inline-block;
		padding: 10rpx 30rpx;
		border-radius: 30rpx;
		background-color: #ff4757;
		transition: all 0.3s ease;
	}

	.state-connected {
		background-color: #2ed573;
	}

	.state-text {
		color: white;
		font-size: 28rpx;
	}

	.button-container {
		width: 100%;
		max-width: 750rpx;
		padding: 0 20rpx;
	}

	.button-group {
		background-color: white;
		border-radius: 20rpx;
		padding: 30rpx;
		margin-bottom: 30rpx;
		box-shadow: 0 4rpx 12rpx rgba(0,0,0,0.05);
	}

	.group-title {
		font-size: 32rpx;
		color: #2c3e50;
		font-weight: bold;
		margin-bottom: 20rpx;
		padding-left: 10rpx;
		border-left: 8rpx solid #3498db;
	}

	.button {
		width: 100%;
		padding: 25rpx;
		margin: 15rpx 0;
		background-color: #3498db;
		color: white;
		font-size: 28rpx;
		border-radius: 10rpx;
		border: none;
		cursor: pointer;
		transition: all 0.3s ease;
	}

	.button:active {
		transform: scale(0.98);
		background-color: #2980b9;
	}

	.footer {
		margin-top: auto;
		padding: 30rpx;
		text-align: center;
		font-size: 24rpx;
		color: #7f8c8d;
	}

	.link {
		color: #3498db;
		margin-top: 10rpx;
		text-decoration: underline;
	}
</style>
