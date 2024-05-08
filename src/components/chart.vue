<script>
import axios from "axios";

export default {
  name: "chart",
  props: ["valuta"],
  data() {
    return {
      series: [
        {
          name: "USD",
          data: []
        }
      ],
      chartOptions: {
        chart: {
          type: "area",
          stacked: false,
          height: 350,
          zoom: {
            type: "x",
            enabled: true,
            autoScaleYaxis: true
          },
          toolbar: {
            autoSelected: "zoom"
          }
        },
        dataLabels: {
          enabled: false
        },
        markers: {
          size: 0
        },
        title: {
          text: "Stock Price Movement",
          align: "left"
        },
        fill: {
          type: "gradient",
          gradient: {
            shadeIntensity: 1,
            inverseColors: false,
            opacityFrom: 0.5,
            opacityTo: 0,
            stops: [0, 90, 100]
          }
        },
        yaxis: {
          labels: {
            // formatter: function (val) {
            //   return (val / 1000000).toFixed(0);
            // },
          },
          title: {
            text: "Price"
          }
        },
        xaxis: {
          categories: []
        },
        tooltip: {
          shared: false,
          y: {
            formatter: function(val) {
              return (val / 1000000).toFixed(0);
            }
          }
        }
      }
    };
  },
  methods: {
    async GetHistoricValuta() {
      try {
        const oggi = new Date();
        oggi.setDate(1); // Imposta il giorno al primo del mese corrente

        // Formattazione della data come "YYYY-MM-DD"
        const dataInizioMese = oggi.toISOString().split("T")[0];
        console.log(dataInizioMese);

        const response = await axios.get(`https://api.frankfurter.app/${dataInizioMese}..?to=${this.valuta}`);
        console.log("Response data:", response.data);

        const ratesEntries = Object.entries(response.data.rates);
        for (const [date, rates] of ratesEntries) {
          console.log(rates.USD);
          this.series[0].data.push({
            x: date,
            y: rates.USD
          });
          this.chartOptions.xaxis.categories.push(date);
        }
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    }
  },
  mounted() {
    this.GetHistoricValuta();
  }
};
</script>

<template>
  <div id="chart" class="col-7 border-black">
    <apexchart
      type="area"
      height="350"
      :options="chartOptions"
      :series="series"
    ></apexchart>
  </div>
</template>

<style lang="scss" scoped></style>
