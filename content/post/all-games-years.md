+++
categories = ["statistics", "VideoGames"]
date = "2016-08-28T12:30:14+02:00"
description = ""
draft = false
image = "/img/about-bg.jpg"
tags = ["videogames", "PS4", "PC", "Xbox One", "Xbox 360","PS Vita", "Nintendo 3DS", "Wii U"]
title = "Statistics Videogames 2016"
+++

<div id="container" style="width: 100%;">
    <canvas id="canvas"></canvas>
    <canvas id="pieChart"></canvas>
    <table class="table table-hover">
        <thead>
            <tr>
                <th>#</th>
                <th>Month</th>
                <th>Total Games</th>
                <th>Percentage</th>
            </tr>
        </thead>
        <tbody id="totalMonth">
        </tbody>
    </table>
</div>
VIA [Wikipedia](https://en.wikipedia.org/wiki/2016_in_video_gaming#endnote_Published)



<script type="text/javascript">
  // Initialize Firebase
    var months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December",]
    var config = {
    apiKey: "AIzaSyC2m_Y0FIpXRm-3X0HVZL00iTnY1tc-1jI",
    authDomain: "games-d7880.firebaseapp.com",
    databaseURL: "https://games-d7880.firebaseio.com",
    storageBucket: "games-d7880.appspot.com",
    };
    firebase.initializeApp(config);
    var database = firebase.database();
    firebase.database().ref('count_mount').on('value', function(snapshot) {
        var key = Object.keys(snapshot.val())[0];
        var total = snapshot.val()[key].reduce(function(a, b) { return a + b; }, 0);
        var ctx = document.getElementById("canvas").getContext("2d");
        var data = {
            labels: months,
            datasets: [
                {
                    label: "Launched In The Month Game",
                    backgroundColor: [
                        '#80FF00',
                        '#0000FF',
                        '#FF8000',
                        '#FFFF00',
                        '#00FF00',
                        '#0080FF',
                        '#8000FF',
                        '#FF00FF',
                        '#FF0080',
                        '#00FF80',
                        '#C207A0',
                        '#2B2626',
                    ],
                    borderColor: [
                        '#80FF00',
                        '#0000FF',
                        '#FF8000',
                        '#FFFF00',
                        '#00FF00',
                        '#0080FF',
                        '#8000FF',
                        '#FF00FF',
                        '#FF0080',
                        '#00FF80',
                        '#C207A0',
                        '#2B2626',
                    ],
                    borderWidth: 1,
                    data: snapshot.val()[key],
                }
            ]
        };
        var options = {
            // Elements options apply to all of the options unless overridden in a dataset
            // In this case, we are setting the border of each bar to be 2px wide and green
            elements: {
                rectangle: {
                    borderWidth: 2,
                    borderColor: 'rgb(0, 255, 0)',
                    borderSkipped: 'bottom'
                }
            },
            responsive: true,
            title: {
                display: true,
                text: 'Total Games Released A Month'
            }
        }
        var myBarChart = new Chart(ctx, {
            type: 'bar',
            data: data,
            options: options
        });
        $.each(snapshot.val()[key], function(index, value) {
            var percentage = 0;
            var number = index + 1
            if (value != 0){
                percentage = Math.round((value / total) * 100)
            }
            $('#totalMonth').append('<tr><th scope="row">' + number+ '</th> <td>' + months[index]  + '</td> <td>' + value + '</td><td> ' + percentage + '%</td></tr>')
        })
        var options = {
            // Elements options apply to all of the options unless overridden in a dataset
            // In this case, we are setting the border of each bar to be 2px wide and green
            elements: {
                rectangle: {
                    borderWidth: 2,
                    borderColor: 'rgb(0, 255, 0)',
                    borderSkipped: 'bottom'
                }
            },
            responsive: true,
            title: {
                display: true,
                text: 'Total Games Released A Month'
            },
            tooltips: {
                callbacks: {
                    label: function(tooltipItem, data) {
                        var allData = data.datasets[tooltipItem.datasetIndex].data;
                        var tooltipLabel = data.labels[tooltipItem.index];
                        var tooltipData = allData[tooltipItem.index];
                        var total = 0;
                        for (var i in allData) {
                            total += allData[i];
                        }
                        var tooltipPercentage = Math.round((tooltipData / total) * 100);
                        return tooltipLabel + ': ' + tooltipData + ' (' + tooltipPercentage + '%)';
                    }
                }
            }
        }
        var PieChart = document.getElementById("pieChart").getContext("2d");
        var myPieChart = new Chart(PieChart, {
            type: 'pie',
            data: data,
            options: options
        });
    });
    firebase.database().ref('games_month').on('value', function(snapshot) {
        var result = snapshot.val();
        var key = Object.keys(result)[0];
        $.each(months, function(index, values) {
            $('#container').append('<canvas id="' + values + '"></canvas>');
            $('#container').append('<table class="table table-hover"><thead><tr><th>Day</th><th>Total</th><th>Game</th></tr></thead><tbody id="totalMonth' + values + '"></tbody></table>')
            var labels = [], dataChart = [];
            $.each(result[key][values.toUpperCase()], function(position, val){
                if (result[key][values.toUpperCase()][position] != undefined) {
                    labels.push(position)
                    dataChart.push(result[key][values.toUpperCase()][position].length)
                    $('#totalMonth' + values).append('<tr><td>' + position  + '</td><td> ' + result[key][values.toUpperCase()][position].length + '</td><td>' + result[key][values.toUpperCase()][position].join(', ') + '</td></tr>')

                }
            });
            var ctx = document.getElementById( values ).getContext("2d");
            var data = {
                labels: labels,
                datasets: [
                    {
                        label: "Launched In The Month " + values,
                        backgroundColor: [
                            "#3D3551", "#884EA2", "#EA648D", "#FFFC3A", "#03414D", "#72DFD0", "#A0F6D2", "#EF7079", "#BF382A", "#683531", "#6D0AD3", "#0098EF", "#00CF95", "#D1FFA2", "#2F3032", "#383A56", "#B0A565", "#EDE68A", "#01005E", "#22267B", "#28518A", "#17B794", "#B062EA", "#F392F2", "#FED08F", "#F6F39F", "#283739", "#2C5D63", "#A2C11C", "#E0E0E0", "#312F44",
                        ],
                        borderColor: [
                            "#3D3551", "#884EA2", "#EA648D", "#FFFC3A", "#03414D", "#72DFD0", "#A0F6D2", "#EF7079", "#BF382A", "#683531", "#6D0AD3", "#0098EF", "#00CF95", "#D1FFA2", "#2F3032", "#383A56", "#B0A565", "#EDE68A", "#01005E", "#22267B", "#28518A", "#17B794", "#B062EA", "#F392F2", "#FED08F", "#F6F39F", "#283739", "#2C5D63", "#A2C11C", "#E0E0E0", "#312F44",
                        ],
                        borderWidth: 1,
                        data: dataChart,
                    }
                ]
            };
            var options = {
                // Elements options apply to all of the options unless overridden in a dataset
                // In this case, we are setting the border of each bar to be 2px wide and green
                elements: {
                    rectangle: {
                        borderWidth: 2,
                        borderColor: 'rgb(0, 255, 0)',
                        borderSkipped: 'bottom'
                    }
                },
                responsive: true,
                title: {
                    display: true,
                    text: 'Total Games Released A ' +  values
                },
                scales: {
                    yAxes: [{
                        ticks: {
                            beginAtZero:true
                        }
                    }]
                }
            }
            var myBarChart = new Chart(ctx, {
                type: 'bar',
                data: data,
                options: options
            });
        })

    });
</script>
