<template>
	<div id="app">
		<Banner :xinfo=info></Banner>
		<List :xsongs=songs></List>
		<xplay></xplay>
	</div>
</template>

<script>
	import Banner from '../components/rangeDetails/banner.vue'
	import List from '../components/rangeDetails/list.vue'
	import xplay from "../components/xplay.vue"

	export default {
		data() {
			return {}
		},
		components: {
			Banner,
			List,
			xplay,
		},
		methods: {
			getDetails() {
				return this.$store.dispatch("rangeDetails");
			}
		},
		mounted() {
			this.$store.dispatch('setPage', 1);
			this.$store.dispatch('setDetails', this.$route.params.id)
			this.getDetails();
			this.$watch("songs", function() {})
		},
		computed: {
			info() {
				if(this.$store.getters.getDetails) {
					var str = this.$store.getters.getDetails.info;
					str.banner7url = str.banner7url.replace(/{size}/g, '400');
					str.bannerurl = str.bannerurl.replace(/{size}/g, '400');
					str.imgurl = str.imgurl.replace(/{size}/g, '400');
					for(var i = 0;i<str.length;i++){
						if(str[i].rankname.slice(0,2) == '酷狗' ){
							str[i].rankname = '爱乐'+str[i].rankname.slice(2,);
						}
					}
					return str;
				} else {
					return ' '
				}
			},
			songs() {
				if(this.$store.getters.getDetails) {
					return this.$store.getters.getDetails.songs.list
				}
			}
		}
	}
</script>
<style lang="less">
.tabLink {
    color: #fc378c;
    width: 100%;
    height: 100%;
    display: block;
}

@import '~vux/src/styles/reset.less';
.vux-tab {
    margin-top: 48px;
}

body {
    background-color: #fbf9fe;
}
</style>