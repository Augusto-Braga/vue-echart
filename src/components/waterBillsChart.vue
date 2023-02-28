<template>
  <div ref="chart" style="height: 500px"></div>
</template>

<script>
import * as echarts from "echarts";

export default {
  name: "WaterBillsChart",
  props: {
    waterBills: {
      type: Array,
      required: true,
    },
  },
  mounted() {
    // Criar instância do gráfico
    let myChart = echarts.init(this.$refs.chart);

    // Formatar dados
    let data = this.waterBills;

    // Definir opções do gráfico
    let options = {
      xAxis: {
        type: "category",
        data: data.map((d) => d.month),
      },
      yAxis: {
        type: "value",
        min: 0,
        max: 300,
        interval: 20,
      },
      series: [
        {
          data: data.map((d) => d.value),
          type: "bar",
        },
      ],
      tooltip: {
        trigger: "axis",
        axisPointer: {
          type: "shadow",
        },
        formatter: function (params) {
          const data = params[0];
          const valueInReal = data.data.toLocaleString("pt-BR", {
            style: "currency",
            currency: "BRL",
          });
          return `Mês: ${data.axisValue}<br>Valor: ${valueInReal}`;
        },
      },
    };

    // Renderizar gráfico com as opções definidas
    myChart.setOption(options);
  },
};
</script>
