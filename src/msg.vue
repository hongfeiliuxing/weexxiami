<template>
    <div>
    <list style="background-color: #F8F8F8;height: 1200" >
        <refresh class="refresh" @refresh="onrefresh" @pullingdown="onpullingdown" :display="refreshing ? 'show' : 'hide'">
            <loading-indicator class="indicator"></loading-indicator>
            <text class="refreshText">{{refreshText}}</text>
        </refresh>
        <cell style="background-color: white">
            <div style="height: 150;flex-direction:row;justify-content:center;align-items:center;border-bottom-color: #EEEEEE;border-bottom-width: 1;">
                <div style="flex: 0.3;margin-left: 20;">
                    <image style="width: 50;height: 50" :src="path+'/msg1.png'"/>
                </div>
                <text style="flex: 0.5">通知</text>
                <div style="flex:2;justify-content: flex-end;align-items: flex-end;right: 40">
                    <image style="width: 30;height: 30" :src="path+'/open_icon.png'"/>
                </div>
            </div>
            <div style="height: 150;flex-direction:row;justify-content:center;align-items:center;border-bottom-color: #EEEEEE;border-bottom-width: 1">
                <div style="flex: 0.3;margin-left: 20;">
                    <image style="width: 50;height: 50" :src="path+'/common.png'"/>
                </div>
                <text style="flex: 0.5">评论和赞</text>
                <div style="flex:2;justify-content: flex-end;align-items: flex-end;right: 40">
                    <image style="width: 30;height: 30" :src="path+'/open_icon.png'"/>
                </div>
            </div>
            <div style="height: 150;flex-direction:row;justify-content:center;align-items:center;border-bottom-color: #EEEEEE;border-bottom-width: 1">
                <div style="flex: 0.3;margin-left: 20;">
                    <image style="width: 50;height: 50" :src="path+'/new-msc.png'"/>
                </div>
                <text style="flex: 0.5">新歌新碟</text>
                <div style="flex:2;justify-content: flex-end;align-items: flex-end;right: 40">
                    <image style="width: 30;height: 30" :src="path+'/open_icon.png'"/>
                </div>
            </div>
            <div style="height: 150;flex-direction:row;justify-content:center;align-items:center;border-bottom-color: #EEEEEE;border-bottom-width: 1">
                <div style="flex: 0.3;margin-left: 20;">
                    <image style="width: 50;height: 50" :src="path+'/fdgrth.png'"/>
                </div>
                <text style="flex: 0.5">新粉丝</text>
                <div style="flex:2;justify-content: flex-end;align-items: flex-end;right: 40">
                    <image style="width: 30;height: 30" :src="path+'/open_icon.png'"/>
                </div>
            </div>
        </cell>
    </list>
    </div>
</template>

<script>
    var api = require('./api.js');
    export default {
        data: {
            refresh_display: 'hide',
            refreshText: '↓   pull to refresh...',
            path:api.apiurl.path,
        },
        methods: {
            onrefresh (event) {
                var thls=this;
                thls.refreshing = true;
                thls.refreshText = "正在刷新";
                setTimeout(() => {
                    thls.refreshing = false;
                    thls.refreshText = '↓ 下拉可以刷新...';
                }, 2000)
            },
            onpullingdown (event) {
                if (event.pullingDistance < -100) {
                    if(this.refreshText != '正在刷新') {

                        this.refreshText = '↑ 松开立即刷新';
                    }
                } else {
                    if(this.refreshText != '正在刷新') {
                        this.refreshText = '↓ 下拉可以刷新';
                    }

                }
            }
        }
    }
</script>

<style>
    .indicator {
        color: #888888;
        height: 40;
        width: 40;
        margin-right: 10;
        justify-content: center;
        align-items: center;
    }
    .refresh {
        height: 100;
        width: 750;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }
    .refreshText {
        color: #888888;
        font-weight: bold;
        font-size: 25;
    }
</style>