+++ 
categories = ["ChartsJS", "Javascript"] 
date = "2015-05-24T18:53:17+02:00" 
tags = ["Charts", "Olympics", "100 meters", "rio 2016",] 
title = "100 metres at the Olympics" 
description = "" 
+++


<div style="width:100%;"id="">
    <canvas id="canvasMan"></canvas>
</div>

<div style="width:100%;"id="">
    <canvas id="canvasWomen"></canvas>
</div>

<div style="width:100%;"id="">
    <canvas id="canvasVS"></canvas>
</div>

<script type="text/javascript">
    $( document ).ready(function() {
        var city_all = ['Athens', 'Paris', 'St. Louis', 'London', 'Stockholm', 'Antwerp', 'Paris', 'Amsterdam', 'Los Angeles', 'Berlin', 'London', 'Helsinki', 'Melbourne', 'Rome', 'Tokyo', 'Mexico City', 'Munich', 'Montreal', 'Moscow', 'Los Angeles', 'Seoul', 'Barcelona', 'Atlanta', 'Sydney', 'Athens', 'Beijing', 'London', 'Rio de Janeiro']

        var run_man = ['Thomas Burke', 'Frank Jarvis', 'Archie Hahn', 'Reggie Walker', 'Ralph Craig', 'Charley Paddock ', 'Harold Abrahams', 'Percy Williams', 'Eddie Tolan', 'Jesse Owens', 'Harrison Dillard', 'Lindy Remigino', 'Bobby Morrow', 'Armin Hary', 'Bob Hayes', 'Jim Hines', 'Valeriy Borzov', 'Hasely Crawford', 'Allan Wells', 'Carl Lewis', 'Carl Lewis', 'Linford Christie', 'Donovan Bailey', 'Maurice Greene', 'Justin Gatlin', 'Usain Bolt', 'Usain Bolt', 'Usain Bolt']

        var manNationality = ['United States', 'United States', 'United States', 'South Africa', 'United States', 'United States', 'Great Britain', 'Canada', 'United States', 'United States', 'United States', 'United States', 'United States', 'Germany', 'United States', 'United States', 'Soviet Union', 'Trinidad and Tobago', 'Great Britain', 'United States', 'United States', 'GBR', 'Canada', 'United States', 'United States', 'Jamaica', 'Jamaica', 'Jamaica']

        var extasMan = ['Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Equal Olympic Record', 'Equal Olympic Record', 'Nothing', 'Equal World Record', 'Nothing', 'Equal Olympic Record', 'Nothing', 'Nothing', 'Equal Olympic Record', 'Equal Olympic Record', 'Equal World Record', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'World Record', 'Nothing', 'World Record', 'Nothing', 'Nothing', 'World Record', 'Olympic Record', "Season's Best"]

        var city_women = ['Amsterdam', 'Los Angeles', 'Berlin', 'London', 'Helsinki', 'Melbourne', 'Rome', 'Tokyo', 'Mexico City', 'Munich', 'Montreal', 'Moscow', 'Los Angeles', 'Seoul', 'Barcelona', 'Atlanta', 'Sydney', 'Athens', 'Beijing', 'London', 'Rio de Janeiro']

        var run_woman = ['Betty Robinson', 'Stanisława Walasiewicz', 'Helen Stephens', 'Fanny Blankers-Koen', 'Marjorie Jackson', 'Betty Cuthbert', 'Wilma Rudolph', 'Wyomia Tyus', 'Wyomia Tyus', 'Renate Stecher', 'Annegret Richter', 'Lyudmila Kondratyeva', 'Evelyn Ashford', 'Florence Griffith-Joyner', 'Gail Devers', 'Gail Devers', 'None', 'Yulia Nestsiarenka', 'Shelly-Ann Fraser', 'Shelly-Ann Fraser-Pryce', 'Elaine Thompson']

        var womenNationality = ['United States', 'Poland', 'United States', 'Netherlands', 'Australia', 'Australia', 'United States', 'United States', 'United States', 'East Germany', 'West Germany', 'URS', 'United States', 'United States', 'United States', 'United States', 'None', 'Belarus', 'Jamaica', 'Jamaica', 'Jamaica']

        var extrasWomen = ['Equal World Record', 'Equal World Record', 'Nothing', 'Equal Olympic Record', 'Equal World Record', 'Nothing', 'Nothing', 'Nothing', 'World Record', 'World Record', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing', 'Nothing']

        var configMan = {
            type: 'line',
            data: {
                labels: ['1896', '1900', '1904', '1908', '1912', '1920', '1924', '1928', '1932', '1936', '1948', '1952', '1956', '1960', '1964', '1968', '1972', '1976', '1980', '1984', '1988', '1992', '1996', '2000', '2004', '2008', '2012', '2016'],
                datasets: [{
                    label: "Time",
                    data: [12.0, 11.0, 11.0, 10.8, 10.8, 10.6, 10.6, 10.8, 10.38, 10.3, 10.3, 10.79, 10.5, 10.2, 10.0, 9.9, 10.14, 10.06, 10.25, 9.99, 9.92, 9.96, 9.84, 9.87, 9.85, 9.69, 9.63, 9.81],
                    lineTension: 0,
                    fill: false,
                    backgroundColor: "#3333ff",
                    borderColor: "#3333ff"
                }]
            },
            options: {
                responsive: true,
                tooltips: {
                    mode: 'label',
                    callbacks: {
                        beforeTitle: function(tooltipItems, data) {
                            return 'City: ' + city_all[tooltipItems[0].index];
                        },
                        beforeBody: function(data) {
                            var multistringText = ['Runner: ' + run_man[data[0].index]];
                            multistringText.push('Nationality: '+ manNationality[data[0].index]);
                            multistringText.push('Extra: '+ extasMan[data[0].index]);
                            return multistringText
                        }
                    }
                },
                scales: {
                    xAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Year'
                        }
                    }],
                    yAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Time Seconds'
                        }
                    }]
                },
                title: {
                    display: true,
                    text: '100 metres at the Olympics'
                },
            }
        };
         var configWoman = {
            type: 'line',
            data: {
                labels: ['1928', '1932', '1936', '1948', '1952', '1956', '1960', '1964', '1968', '1972', '1976', '1980', '1984', '1988', '1992', '1996', '2000', '2004', '2008', '2012', '2016'],
                datasets: [{
                    label: "Time",
                    data: [12.2, 11.9, 11.5, 11.9, 11.5, 11.5, 11.18, 11.4, 11.0, 11.07, 11.08, 11.06, 10.97, 10.54, 10.82, 10.94, null, 10.93, 10.7, 10.75, 10.71],
                    lineTension: 0,
                    fill: false,
                    backgroundColor: "#8a00e6",
                    borderColor: "#8a00e6"
                }
                ]
            },
            options: {
                responsive: true,
                tooltips: {
                    mode: 'label',
                    callbacks: {
                        beforeTitle: function(tooltipItems, data) {
                            return 'City: ' + city_women[tooltipItems[0].index];
                        },
                        beforeBody: function(data) {
                            var multistringText = ['Runner: ' + run_woman[data[0].index]];
                            multistringText.push('Nationality: '+ womenNationality[data[0].index]);
                            multistringText.push('Extra: '+ extrasWomen[data[0].index]);
                            return multistringText
                        }
                    }
                },
                scales: {
                    xAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Year'
                        }
                    }],
                    yAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Time'
                        }
                    }]
                },
                title: {
                    display: true,
                    text: '100 metres at the Olympics'
                }
            }
        };

        var configVS = {
            type: 'line',
            data: {
                labels: ['1896', '1900', '1904', '1908', '1912', '1920', '1924', '1928', '1932', '1936', '1948', '1952', '1956', '1960', '1964', '1968', '1972', '1976', '1980', '1984', '1988', '1992', '1996', '2000', '2004', '2008', '2012', '2016'],
                datasets: [{
                    label: "Men",
                    data: [12.0, 11.0, 11.0, 10.8, 10.8, 10.6, 10.6, 10.8, 10.38, 10.3, 10.3, 10.79, 10.5, 10.2, 10.0, 9.9, 10.14, 10.06, 10.25, 9.99, 9.92, 9.96, 9.84, 9.87, 9.85, 9.69, 9.63, 9.81],
                    lineTension: 0,
                    fill: false,
                    backgroundColor: "#3333ff",
                    borderColor: "#3333ff"
                },{
                    label: "Woman",
                    data: [null, null, null, null, null, null, null, 12.2, 11.9, 11.5, 11.9, 11.5, 11.5, 11.18, 11.4, 11.0, 11.07, 11.08, 11.06, 10.97, 10.54, 10.82, 10.94, null, 10.93, 10.7, 10.75, 10.71],
                    lineTension: 0,
                    fill: false,
                    backgroundColor: "#8a00e6",
                    borderColor: "#8a00e6"
                }
                ]
            },
            options: {
                responsive: true,
                hover: {
                    mode: 'label'
                },
                scales: {
                    xAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Year'
                        }
                    }],
                    yAxes: [{
                        display: true,
                        scaleLabel: {
                            display: true,
                            labelString: 'Time'
                        }
                    }]
                },
                title: {
                    display: true,
                    text: '100 metres at the Olympics'
                }
            }
        };

        window.onload = function() {
            var man = document.getElementById("canvasMan").getContext("2d");
            window.myLine = new Chart(man, configMan);

            var woman = document.getElementById("canvasWomen").getContext("2d");
            window.myLine = new Chart(woman, configWoman);

            var VS = document.getElementById("canvasVS").getContext("2d");
            window.myLine = new Chart(VS, configVS);
        };
    });
</script>