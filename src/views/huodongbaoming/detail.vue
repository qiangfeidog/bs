<template>
    <div class="huodongbaoming-detail" v-loading="loading" ref="print">
        <el-page-header @back="goBack" content="详情页面"></el-page-header>
        <div class="admin-detail">
            <div class="detail detail-readmodule">
                <div class="detail-title">旅游活动id：</div>
                <div class="detail-content">{{ map.lvyouhuodongid }}</div>
            </div>
            <div class="detail detail-text">
                <div class="detail-title">编号：</div>
                <div class="detail-content">{{ map.bianhao }}</div>
            </div>
            <div class="detail detail-text">
                <div class="detail-title">报名编号：</div>
                <div class="detail-content">{{ map.baomingbianhao }}</div>
            </div>
            <div class="detail detail-text">
                <div class="detail-title">联系方式：</div>
                <div class="detail-content">{{ map.lianxifangshi }}</div>
            </div>
            <div class="detail detail-text">
                <div class="detail-title">昵称：</div>
                <div class="detail-content">{{ map.nicheng }}</div>
            </div>
            <div class="detail detail-longtext">
                <div class="detail-title">标题：</div>
                <div class="detail-content">{{ map.biaoti }}</div>
            </div>
            <div class="detail detail-select">
                <div class="detail-title">类型：</div>
                <div class="detail-content">{{ map.leixing }}</div>
            </div>
            <div class="detail detail-select">
                <div class="detail-title">报名状态：</div>
                <div class="detail-content">{{ map.baomingzhuangtai }}</div>
            </div>
            <div class="detail detail-image">
                <div class="detail-title">图片：</div>
                <div class="detail-content">
                    <e-img :src="map.tupian" style="max-width: 120px" />
                </div>
            </div>
            <div class="detail detail-money">
                <div class="detail-title">活动价格：</div>
                <div class="detail-content">{{ map.huodongjiage }}</div>
            </div>
            <div class="detail detail-money">
                <div class="detail-title">总费用：</div>
                <div class="detail-content">{{ map.zongfeiyong }}</div>
            </div>
            <div class="detail detail-datetime">
                <div class="detail-title">开始时间：</div>
                <div class="detail-content">{{ map.kaishishijian }}</div>
            </div>
            <div class="detail detail-datetime">
                <div class="detail-title">结束时间：</div>
                <div class="detail-content">{{ map.jieshushijian }}</div>
            </div>
            <div class="detail detail-number">
                <div class="detail-title">报名人数：</div>
                <div class="detail-content">{{ map.baomingrenshu }}</div>
            </div>
            <div class="detail detail-textuser">
                <div class="detail-title">报名用户：</div>
                <div class="detail-content">{{ map.baomingyonghu }}</div>
            </div>
        </div>
        <div class="mt10">
            <el-button type="default" class="hidePrint" @click="$router.go(-1)"> 返回 </el-button>
            <el-button type="success" class="hidePrint" @click="$print"> 打印本页 </el-button>
        </div>
    </div>
</template>
<style type="text/scss" scoped lang="scss">
    .huodongbaoming-detail {
        .admin-detail {
            display: flex;
            flex-wrap: wrap;
            margin-top: 30px;
            .detail {
                width: 50%;
                padding: 5px;
                display: flex;
                margin-bottom: 10px;
                border-bottom: 1px solid #DEDEDE;
                .detail-title {
                    width: 120px;
                    text-align: right;
                    flex-shrink: 0;
                }
                .detail-content {
                    flex-grow: 1;
                }
            }
            .detail.detail-images {
                width: 100%;
                flex-wrap: wrap;
                .detail-title {
                    display: none;
                }

                .detail-content {
                    width: 100%;
                    padding: 10px;
                }
            }
            .detail.detail-editor,
            .detail.detail-dataset {
                width: 100%;
                flex-wrap: wrap;
                .detail-title {
                    width: 100%;
                    padding: 10px;
                    margin-top: 10px;
                    background: #9a0606;
                    color: #ffffff;
                    text-align: left;
                }
                .detail-content {
                    padding: 10px;
                }
            }
        }
    }
</style>
<script>
    import api from "@/api";
    import { extend } from "@/utils/extend";

    export default {
        data() {
            return {
                loading: false,
                map: {},
            };
        },
        props: {
            id: {
                type: [String, Number],
                required: true,
            },
        },
        watch: {
            id: {
                handler() {
                    this.loadDetail();
                },
                immediate: true,
            },
        },
        computed: {},
        methods: {
            goBack() {
                this.$router.go(-1);
            },
            loadDetail() {
                if (this.loading) return;
                this.loading = true;
                this.$get(api.huodongbaoming.detail, {
                    id: this.id,
                })
                    .then((res) => {
                        this.loading = false;
                        if (res.code == api.code.OK) {
                            extend(this, res.data);
                        } else {
                            this.$message.error(res.msg);
                        }
                    })
                    .catch((err) => {
                        this.loading = false;
                        this.$message.error(err.message);
                    });
            },
        },
        created() {},
        mounted() {},
        destroyed() {},
    };
</script>
