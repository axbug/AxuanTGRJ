<template>
	<view class="example-box">
		<uni-card :is-shadow="true" title="阿轩" mode="title" thumbnail="http://q2.qlogo.cn/headimg_dl?dst_uin=1024340498&spec=640" :extra="date" note="true" @click="clickCard">
			<view>
				<view class="content-box">
					<text class="content-box-text">{{ con }}</text>
				</view>
				<view class="image-box"><image class="image" mode="aspectFill" src="../../static/img.gif" /></view>
			</view>
			<template slot="footer">
				<view class="footer-box">
					<view @click.stop="footerClick('喜欢')"><text class="footer-box__item">喜欢</text></view>
					<view @click.stop="footerClick('评论')"><text class="footer-box__item">评论</text></view>
					<view @click.stop="footerClick('分享')"><text class="footer-box__item">收藏</text></view>
				</view>
			</template>
		</uni-card>
		<button type="primary" style="width: 92%;" @click="getwrite()">刷新日记</button>
	</view>
</template>

<script>
import uniSection from '@/components/uni-section/uni-section.vue';
import uniCard from '@/components/uni-card/uni-card.vue';
export default {
	components: {
		uniSection,
		uniCard
	},
	data() {
		return {
			date: '发表于 2020-03-23  多云',
			con: '请求数据中 长时间未载入数据可能是接口失效或者其他错误'
		};
	},
	onLoad() {
		this.getwrite();
	},
	methods: {
		clickCard() {},
		footerClick(types) {
			uni.showToast({
				title: types + '成功！',
				icon: 'none'
			});
		},
		getwrite() {
			uni.request({
				url: 'http://app.yxbug.cn/app/AxuanTGRJ/',
				success: res => {
					console.log(res.data);
					this.date = '发表于' + ' ' + res.data.data.date + ' ' + res.data.data.weather;
					this.con = res.data.data.content;
				}
			});
		}
	}
};
</script>

<style>
/* 头条小程序组件内不能引入字体 */
/* #ifdef MP-TOUTIAO */
@font-face {
	font-family: uniicons;
	font-weight: normal;
	font-style: normal;
	src: url('~@/static/uni.ttf') format('truetype');
}

/* #endif */

/* #ifndef APP-NVUE */
page {
	display: flex;
	flex-direction: column;
	box-sizing: border-box;
	background-color: #efeff4;
	min-height: 100%;
	height: auto;
}

view {
	font-size: 28rpx;
	line-height: inherit;
}

.example {
	padding: 0 30rpx 30rpx;
}

.example-info {
	padding: 30rpx;
	color: #3b4144;
	background: #ffffff;
}

.example-body {
	flex-direction: row;
	flex-wrap: wrap;
	justify-content: center;
	padding: 0;
	font-size: 14rpx;
	background-color: #ffffff;
}

/* #endif */
.example {
	padding: 0 30rpx;
}

.example-info {
	/* #ifndef APP-NVUE */
	display: block;
	/* #endif */
	padding: 30rpx;
	color: #3b4144;
	background-color: #ffffff;
	font-size: 30rpx;
}

.example-info-text {
	font-size: 28rpx;
	line-height: 36rpx;
}

.example-body {
	flex-direction: column;
	padding: 30rpx;
	background-color: #ffffff;
}

.word-btn-white {
	font-size: 18px;
	color: #ffffff;
}

.word-btn {
	/* #ifndef APP-NVUE */
	display: flex;
	/* #endif */
	flex-direction: row;
	align-items: center;
	justify-content: center;
	border-radius: 6px;
	height: 48px;
	margin: 15px;
	background-color: #007aff;
}

.word-btn--hover {
	background-color: #4ca2ff;
}

.example-body {
	padding: 20rpx 0;
	padding-bottom: 0;
}

.example-box {
	/* margin-bottom: 30rpx;
 */
}

.image-box {
	/* #ifndef APP-NVUE */
	display: flex;
	flex-direction: column;
	/* #endif */
	height: 440rpx;
	overflow: hidden;
	padding-bottom: 10rpx;
}

.image {
	/* #ifndef APP-NVUE */
	width: 100%;
	height: 100%;
	/* #endif */
	flex: 1;
}

.content-box {
	margin-top: -10rpx;
}

.content-box-text {
	font-size: 30rpx;
}

.footer-box {
	/* #ifndef APP-NVUE */
	display: flex;
	/* #endif */
	justify-content: space-between;
	flex-direction: row;
}

.footer-box__item {
	align-items: center;
	padding: 10rpx 0;
	font-size: 30rpx;
	color: #666;
}
</style>
