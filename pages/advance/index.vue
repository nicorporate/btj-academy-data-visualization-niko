<template>
    <!-- <AppContainer title="Manga List">
      <div>Content manga list</div>
    </AppContainer> -->
    <div>
      <highchart :options="chartOptions1" />
    </div>
    <div>
      <highchart :options="chartOptions" />

    </div>
    <div>
      <highchart :options="chartOptions2" />
    </div>
    <div>
      <highchart :options="chartOptions3" />
    </div>
</template>

<script>
  export default {
  data() {
    return {
      chartOptions1: {
        chart: {
          // type: 'column'
        },
        title: {
          text: 'Prakiraan Cuaca Bulanan',
          align: 'left'
        },
        subtitle: {
          text: 'Data penduduk Surabaya Tahun 2018-2022',
          align: 'left'
        },
        legend: {
          align: 'right',
          verticalAlign: 'top',
          layout: 'horizontal',
          reversed: true
        },
        series: [
          {
            name: 'Temperatur',
            type: 'column',
            tooltip: {
              valueSuffix: ' °C'
            },
            data: [23, 24, 27, 35, 31, 26, 29, 31, 23, 25, 28, 30]
          },
          {
            name: 'Kelembapan',
            type: 'spline',
            yAxis: 1,
            tooltip: {
              valueSuffix: ' %'
            },
            marker: {
              enabled: false
            },
            dashStyle: 'shortdot',
            data: [85, 89, 90, 82, 95, 91, 87, 84, 90, 88, 99, 91]
          },
          {
            name: 'Kecepatan Angin',
            type: 'spline',
            yAxis: 2,
            tooltip: {
              valueSuffix: ' km/jam'
            },
            data: [12, 12, 14, 15, 13, 11, 15, 16, 16, 14, 15, 16]
          }
        ],
        xAxis: {
          categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sept', 'Oct', 'Nov', 'Dec' ],
          title: {
            text: 'Bulan'
          }
        },
        yAxis: [
          {
            title: {
              text: 'Temperatur'
            },
            labels: {
              format: '{value}°C'
            }
          },
          {
            title: {
              text: 'Kelembapan'
            },
            labels: {
              format: '{value}%'
            }
          },
          {
            title: {
              text: 'Kecepatan Angin'
            },
            labels: {
              format: '{value} km/jam'
            },
            opposite: true
          },
        ],

        
        // tooltip: {
        //   shared: true,
        //             formatter: function(){
        //                 console.log(this.points)
        //                 return [`<b>Bulan ${this.x} </b> <br/>`].concat(
        //                     this.points ? this.points.map(point => {
        //                         return `  ${point.series.name}: ${point.y} <br />` 
        //                     }) : []
        //                 )
        //                 return 'something'
        //             }
        // }
      },
      chartOptions: {
        chart: {
          // type: 'column'
        },
        title: {
          text: 'Prakiraan Cuaca Bulanan',
          align: 'left'
        },
        subtitle: {
          text: 'Data penduduk Surabaya Tahun 2018-2022',
          align: 'left'
        },
        legend: {
          align: 'right',
          verticalAlign: 'top',
          layout: 'horizontal',
          reversed: true
        },
        series: [
          {
            name: 'Pria',
            type: 'column',
            data: [12341, 84982, 53783, 23234, 4435]
          },
          {
            name: 'Wanita',
            type: 'column',
            data: [43541, 34982, 53183, 63234, 15235]
          },
          {
            name: 'rata-rata',
            type: 'line',
            step: 'center',
            data: [64861, 54573, 23667, 72535, 86645]
          },
          {
            name: 'total',
            type: 'pie',
            size: '120',
            center: [50, -10],
            innerSize: '30%',
            dataLabels: {
              enabled: false
            },
            data: [
              {
                name: 'Pria',
                y: 517
              },
              {
                name: 'Wanita',
                y: 590
              }
            ]
          }
        ],
        xAxis: {
          categories: [2018, 2019, 2020, 2021, 2022],
          title: {
            text: 'Tahun'
          }
        },
        yAxis: {
          title: {
            text: 'Jumlah Penduduk'
          },
          labels: {
            format: '{value}M'
          }
        },
        tooltip: {
          shared: true,
                    formatter: function(){
                        console.log(this.points)
                        return [`<b>Tahun ${this.x} </b> <br/>`].concat(
                            this.points ? this.points.map(point => {
                                return ` Jumlah  ${point.series.name}: ${point.y} <br />` 
                            }) : []
                        )
                        return 'something'
                    }
        }
      },
      chartOptions2: {
        chart: {
          type: 'area'
        },
        title: {
          text: 'Statistik Penduduk Surabaya',
          align: 'left'
        },
        subtitle: {
          text: 'Data penduduk Surabaya Tahun 2018-2022',
          align: 'left'
        },
        legend: {
          align: 'right',
          verticalAlign: 'top',
          layout: 'horizontal',
          reversed: true
        },
        series: [
          {
            name: 'Pria',
            data: [12341, 84982, 53783, 23234, 4435]
          },
          {
            name: 'Wanita',
            data: [43541, 34982, 53183, 63234, 15235]
          }
        ],
        xAxis: {
          categories: [2018, 2019, 2020, 2021, 2022],
          title: {
            text: 'Tahun'
          }
        },
        yAxis: {
          title: {
            text: 'Jumlah Penduduk'
          },
          labels: {
            format: '{value}M'
          }
        },
      },
      chartOptions3: {
        chart: {
          type: 'bar'
        },
        title: {
          text: 'Statistik Penduduk Surabaya',
          align: 'left'
        },
        subtitle: {
          text: 'Data penduduk Surabaya Tahun 2018-2022',
          align: 'left'
        },
        legend: {
          align: 'right',
          verticalAlign: 'top',
          layout: 'horizontal',
          reversed: true
        },
        series: [
          {
            name: 'Pria',
            data: [12341, 84982, 53783, 23234, 4435]
          },
          {
            name: 'Wanita',
            data: [43541, 34982, 53183, 63234, 15235]
          }
        ],
        xAxis: {
          categories: [2018, 2019, 2020, 2021, 2022],
          title: {
            text: 'Tahun'
          }
        },
        yAxis: {
          title: {
            text: 'Jumlah Penduduk'
          },
          labels: {
            format: '{value}M'
          }
        },
      }
    }
  }
}
</script>