<template>
<div  id="content-wrapper">
	<div class="so-con-right" >
		<div id="scroller" > <!-- style="min-height: 180%"  --><!--<div>-->
			<div class="tab_container">
				<!--以下为盘面不同样式，根据ID区分-->
				<!-- 两面 -->
	            <div id="so-item0" class="content-right active item_one" >
	                
	                <ul>
						<!-- 特码两面 -->
	                    <li class="select-li bet_lm" v-for="item in liangMianList">
                            <div class="bet_panel">
                                <h2>
                                    {{item.name}}
                                </h2>
                                <div class="bet_box">
                                    <p :data-id="itemChild.cid" :class="isBtnActived(itemChild)"  v-for="(itemChild,index) in item.childrens" @click="betSelect(itemChild)">
                                        <span>{{itemChild.name}}</span>
                                        <span class="bet-times">{{payoffFormat(itemChild.oddsData.payoff)}}</span>
                                    </p>
                                </div>
                            </div>
                        </li>
	                </ul>
	            </div>
	        </div><!-- tab_container -->
        </div><!-- scroller -->
    </div><!-- so-con-right -->
</div>
</template>

<script>
    import playTreeIndexByCid from '@/PlayTreeIndexByCid'
    import LhcMixin from '@/components/lhc/LhcMixin'

    export default {
        name: 'LiangMian',
        mixins: [LhcMixin],
        props: {
            playTreeList: {
                type: Array,
                default: [],
            },
            betSelectedList: {
                type: Array,
                default: [],
            }
        },
        data: function () {
            return {
                liangMianList: [],
                myScroll: null
            }
        },
        mounted(){
            if (playTreeIndexByCid.get('1021000')) {
                this.liangMianList = playTreeIndexByCid.get('1021000').childrens
            }
            this.myScroll = new iScroll("scroller",{  // 投注区域
                onScrollEnd() {
                    this.refresh() ;
                },
                vScroll:true,
                mouseWheel: false ,
                hScrollbar:false ,
                vScrollbar:false ,
                click: true ,
                useTransform: false ,
                useTransition: false ,
            });
            this.myScroll.refresh()
            this.myScroll.scrollTo(0, 100)
        },
        created() {
        },
        computed: {

        },
        updated() {
            this.setScrollHeight(false, 0)
        },
        watch: {
            playTreeList() {
                if (playTreeIndexByCid.get('1021000')) {
                    this.liangMianList = playTreeIndexByCid.get('1021000').childrens
                }
            },
        },
        methods: {

        }
    }
</script>
