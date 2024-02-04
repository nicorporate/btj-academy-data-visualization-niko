<template>
    <div class="pt-5">
      <highchart :options="chartOptions"
      :modules="['exporting', 'export-data']" />

    </div>

</template>
  
<script>

  export default {
    data() {
      return {
        items: [],
        chartOptions: {
          chart: {
            height: 1000, 
            width: 1280, 
            backgroundColor: 'transparent',
          },
          title: {
            text: "Statistik Penduduk Indonesia Tahun 2023",
            align: 'center',
          },
          subtitle: {
            text: "Data Penduduk Indonesia Berdasarkan Provinsi Tahun 2023",
            align: 'center',
          },
          legend: {
            align: 'right',
            verticalAlign: 'top',
            layout: 'horizontal', 
          },
          xAxis: {
              title: {
                  text: 'PROVINSI',
              },
              categories: [],
          },
          yAxis: [
            { 
              title: {
                text: 'JUMLAH PENDUDUK (Jiwa)',
              },
              opposite: true
            },
            { 
              title: {
                text: "JUMLAH PENDUDUK PER KM2"
              },
              labels: {
                format: '{value}'
              }
            },
          ],
          series: [
            {
              name: 'Jumlah Penduduk per Provinsi',
              type: 'bar',
              data: [],
              tooltip: {
                headerFormat: '<b>Provinsi: {point.x}</b><br/>',
                pointFormat: 'Jumlah penduduk: <b>{point.y} jiwa</b><br/>',
              },
            },
            { 
              name: 'Total',
              type: 'pie',
              size: '200',
              center: [900, 90],
              innerSize: '20%',
              data: [],
              tooltip: {
                pointFormat: '<b><point.name></b>Jumlah penduduk: <b>{point.y} </b> jiwa',
              },
            },
            { 
              name: 'Jumlah Penduduk per km2',
              type: 'bar',
              data: [],
              tooltip: {
                headerFormat: '<b>Provinsi: {point.x}</b><br/>',
                pointFormat: 'Jumlah penduduk per km2: <b>{point.y} jiwa/km2</b><br/>',
              },
              yAxis: 1,
            },
          ],
          tooltip: { 
            enabled: true, 
            shared: true, 
          }, 
           plotOptions: {
            pie: {
              allowPointSelect: true,
              cursor: 'pointer',
              dataLabels: {
                enabled: true,
                distance: -50,
                format: '{point.name}',
              },
            },
          },
        },
      };
    },
    mounted() {
      this.fetchPeopleDataList();
    },
    methods: {
      hurufKapital(provinsi) {
        return provinsi.split(' ').map(huruf => {
            return huruf.charAt(0).toUpperCase() + huruf.slice(1).toLowerCase();
        }).join(' ');
      },
      async fetchPeopleDataList() {
        const resp = await fetch('https://api-e-database.kemendagri.go.id/api/dukcapil_jumlah_penduduk_prov/51F890E2DF?tahun=2023');
        const body = await resp.json();
        this.items = body.data;
        console.log(body);
        
        // XAxis Data
        this.chartOptions.xAxis.categories = this.items.map(entry => this.hurufKapital(entry.prov));
        console.log("ini xAxis", this.chartOptions.xAxis.categories);
  
        // Bar Chart
        this.chartOptions.series[0].data = this.items.map(entry => parseFloat(entry.jumlah_penduduk)); // ubahtz string ke angka
        console.log("ini series untuk bar", this.chartOptions.series[0].data);
        
        // Bar Chart
        this.chartOptions.series[2].data = this.items.map(entry => parseFloat(entry.jumlah_penduduk_km2));
         console.log("ini series untuk line", this.chartOptions.series[2].data);

        // Pie Chart
        this.chartOptions.series[1].data = this.items.map(entry => ({
          name: entry.prov,
          y: parseFloat(entry.jumlah_penduduk),
        }));
  
      },
   
    },
  };
</script>