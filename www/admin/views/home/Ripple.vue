<template>
    <bag-card class="profit">
        <template v-slot:title>盈利率/占比</template>
        <div id="dom1"></div>
    </bag-card>
</template>
<script lang="ts">
import {defineComponent, onMounted} from "vue";
import {Liquid, measureTextWidth} from '@antv/g2plot';

export default defineComponent({
    setup() {
        function container() {
            let dom1:HTMLElement = document.getElementById('dom1') as HTMLElement;
            const liquidPlot = new Liquid(dom1, {
                percent: 0.26,
                radius: 0.8,
                height:210,
                statistic: {
                    title: {
                        formatter: () => '盈利率',
                        style: ({percent}) => ({
                            fill: percent > 0.65 ? 'white' : 'rgba(44,53,66,0.85)',
                        }),
                    },
                    content: {
                        // @ts-ignore
                        style: ({percent}) => ({
                            fontSize: 60,
                            lineHeight: 1,
                            fill: percent > 0.65 ? 'white' : 'rgba(44,53,66,0.85)',
                        }),
                        customHtml: (container, view, res:any) => {
                            const {width, height} = container.getBoundingClientRect();
                            const d = Math.sqrt(Math.pow(width / 2, 2) + Math.pow(height / 2, 2));
                            const text = `占比 ${(res.percent * 100).toFixed(0)}%`;
                            const textWidth = measureTextWidth(text, {fontSize: 60});
                            const scale = Math.min(d / textWidth, 1);
                            return `<div style="width:${d}px;display:flex;align-items:center;justify-content:center;font-size:${scale}em;line-height:${
                                scale <= 1 ? 1 : 'inherit'
                            }">${text}</div>`;
                        },
                    },
                },
                liquidStyle: ({percent}) => {
                    return {
                        fill: percent > 0.45 ? '#5B8FF9' : '#FAAD14',
                        stroke: percent > 0.45 ? '#5B8FF9' : '#FAAD14',
                    };
                },
                color: () => '#5B8FF9',
            });
            liquidPlot.render();

            let data = 0.25;
            const interval = setInterval(() => {
                data += Math.min(Math.random() * 0.1, 0.1);
                if (data < 0.75) {
                    liquidPlot.changeData(data);
                } else {
                    clearInterval(interval);
                }
            }, 500);

        }

        onMounted(() => {
            container()
        })
    }
})
</script>
<style lang="less" scoped></style>
