+++
categories = ["statistics", "VideoGames"]
date = "2016-08-28T16:36:36+02:00"
description = ""
draft = false
image = "/img/about-bg.jpg"
tags = ["videogames", "PS4", "PC", "Xbox One", "Xbox 360","PS Vita", "Nintendo 3DS", "Wii U"]
title = "Percentage Monthly Per Console"
+++

<div id="container" style="width: 100%;">
</div>



<script type="text/javascript">
    // Initialize Firebase
    var months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December",]
    var labels = ['Nintendo 3DS', 'PC', 'PS3', 'PS4', 'PSVITA', 'Wii U', 'Xbox 360', 'Xbox One']
    var config = {
    apiKey: "AIzaSyC2m_Y0FIpXRm-3X0HVZL00iTnY1tc-1jI",
    authDomain: "games-d7880.firebaseapp.com",
    databaseURL: "https://games-d7880.firebaseio.com",
    storageBucket: "games-d7880.appspot.com",
    };
    firebase.initializeApp(config);
    var database = firebase.database();
    firebase.database().ref('percent_mount').on('value', function(snapshot) {
        var result = snapshot.val();
        var key = Object.keys(snapshot.val())[0];
        $.each(result[key], function(index, values) {
            if (index != 0) {
                var dataChart = []
                var nameCanvas = "canvas" + index
                $('#container').append('<canvas id="' + nameCanvas + '"></canvas>');
                $('#container').append('<table class="table table-hover"><thead><tr><th>Console</th><th>Total</th><th>Percentage</th></tr></thead><tbody id="totalMonth' + nameCanvas + '"></tbody></table>')
                $.each(labels, function(position, val) {
                    dataChart.push(values[val])
                })
                firebase.database().ref('category_mount').on('value', function(value){
                    var keyMount = Object.keys(value.val())[0];
                    $.each(labels, function(position, val) {
                        $('#totalMonth' + nameCanvas).append('<tr><td>' + val  + '</td><td>' + value.val()[keyMount][index][val] + '</td><td> ' + values[val] + ' %</td></tr>')
                    })
                });
                firebase.database().ref('videogames_mount').on('value', function(value){
                    var keyMount = Object.keys(value.val())[0];
                    console.log(snapshot.val()[keyMount])
                });
                var title = 'Percentage Of Games Released For Console In The Month Of ' + months[index - 1];
                var ctx = document.getElementById( nameCanvas ).getContext("2d");
                var data = {
                    labels: labels,
                    datasets: [
                        {
                            label: "Launched In The Month Game",
                            backgroundColor: [
                                '#0000FF',
                                '#FF8000',
                                '#FFFF00',
                                '#80FF00',
                                '#00FF00',
                                '#00FF80',
                                '#0080FF',
                                '#8000FF',
                                '#FF00FF',
                                '#FF0080',
                                '#0000FF',
                                '#2B2626',
                            ],
                            borderColor: [
                                '#0000FF',
                                '#FF8000',
                                '#FFFF00',
                                '#80FF00',
                                '#00FF00',
                                '#00FF80',
                                '#0080FF',
                                '#8000FF',
                                '#FF00FF',
                                '#FF0080',
                                '#0000FF',
                                '#2B2626',
                            ],
                            borderWidth: 1,
                            data: dataChart,
                        }
                    ]
                };
                var options = {
                    // Elements options apply to all of the options unless overridden in a dataset
                    // In this case, we are setting the border of each bar to be 2px wide and green
                    responsive: true,
                    title: {
                        display: true,
                        text: title
                    },
                    legend: {
                        position: 'left'
                    }
                }
                var myPieChart = new Chart(ctx, {
                    type: 'pie',
                    data: data,
                    options: options
                });
                
            }
        })  
    });
    firebase.database().ref('games_month').on('value', function(snapshot) {
        var result = snapshot.val();
        var key = Object.keys(result)[0];
        console.log(result)
        console.log(key)

    });
</script>
