$(document).ready(function () {
  var timeData = [],
    temperatureData = [],
    humidityData = [],
  pm2Data = [],
  pm10Data = [];
 //---------yanji start 1/2------------
  
  //20170913
  var pm10Data = [],
      pm25Data = [],
      busp2Data = [],
      busp1Data = [];
  var result;
 // android 20170912 23:29
  var humilength = humidityData.length;
  // 20170913
  var templength = temperatureData.length;
  var pm10length = pm10Data.length;
  var pm25length = pm25Data.length;
  var rpmData = [];
  var rpm2Data = [];
   var tempimsi = 0;
   var humiimsi = 0;
   var aaaa = 50;
  //---------yanji end 1/2------------
  document.getElementById("pm2").innerHTML = "50";
  document.getElementById("pm10").innerHTML = "30";
  document.getElementById("temp").innerHTML = "10";
  document.getElementById("humi").innerHTML = "80";
  document.getElementById("rpm").innerHTML = "0";
  document.getElementById("rpm2").innerHTML = "0";
  var data = {
    labels: timeData,
    datasets: [
      {
        fill: false,
        label: 'Temp',
        yAxisID: 'Temp',
        borderColor: "rgba(255, 204, 0, 1)",
        pointBoarderColor: "rgba(255, 204, 0, 1)",
        backgroundColor: "rgba(255, 204, 0, 0.4)",
        pointHoverBackgroundColor: "rgba(255, 204, 0, 1)",
        pointHoverBorderColor: "rgba(255, 204, 0, 1)",
        data: temperatureData
      },
      {
        fill: false,
        label: 'pm2.5',
        yAxisID: 'pm2.5',
        borderColor: "rgba(255, 131, 131, 1)",
        pointBoarderColor: "rgba(255, 131, 131, 1)",
        backgroundColor: "rgba(255, 131, 131, 0.4)",
        pointHoverBackgroundColor: "rgba(255, 131, 131, 1)",
        pointHoverBorderColor: "rgba(255, 131, 131, 1)",
        data: pm2Data
      }
    ]
  }

  var basicOption = {
    title: {
      display: true,
      text: 'Temperature & pm2.5 Real-time Data',
      fontSize: 15
    },
    scales: {
      yAxes: [{
        id: 'Temp',
        type: 'linear',
        scaleLabel: {
          labelString: 'Temp(C)',
          display: true
        },
        position: 'left',
      }, {
          id: 'pm2.5',
          type: 'linear',
          scaleLabel: {
            labelString: 'pm2.5(ug/m3)',
            display: true
          },
          position: 'right'
        }]
    }
  }


  ///////////////////////////////////////////////////////////////////////////////////////////////////

  var data2 = {
    labels: timeData,
    datasets: [
      {
        fill: false,
        label: 'Motor1',
        yAxisID: 'Motor1',
        borderColor: "rgba(0, 84, 255, 1)",
        pointBoarderColor: "rgba(0, 84, 255, 1)",
        backgroundColor: "rgba(0, 84, 255, 0.4)",
        pointHoverBackgroundColor: "rgba(0, 84, 255, 1)",
        pointHoverBorderColor: "rgba(0, 84, 255, 1)",
        data: rpmData
      },
      {
        fill: false,
        label: 'Motor2',
        yAxisID: 'Motor2',
        borderColor: "rgba(29, 219, 22, 1)",
        pointBoarderColor: "rgba(29, 219, 22, 1)",
        backgroundColor: "rgba(29, 219, 22, 0.4)",
        pointHoverBackgroundColor: "rgba(29, 219, 22, 1)",
        pointHoverBorderColor: "rgba(29, 219, 22, 1)",
        data: rpm2Data
      }
    ]
  }

  var basicOption2 = {
    title: {
      display: true,
      text: 'Mortor1 & Mortor2 Real-time Data',
      fontSize: 15
    },
    scales: {
      yAxes: [{
        id: 'Motor1',
        type: 'linear',
        scaleLabel: {
          labelString: 'rpm(r/min)',
          display: true
        },
        position: 'left',
      }, {
          id: 'Motor2',
          type: 'linear',
          scaleLabel: {
            labelString: 'rpm(r/min)',
            display: true
          },
          position: 'right'
        }]
    }
  }

  //////////////////////////////////////////////////////////////////////////////////////////////////////////////

  //Get the context of the canvas element we want to select
  var ctx = document.getElementById("myChart").getContext("2d");
  var optionsNoAnimation = { animation: false }
  var myLineChart = new Chart(ctx, {
    type: 'line',
    data: data,
    options: basicOption
  });
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////
  var ctx2 = document.getElementById("myChart2").getContext("2d");
  var optionsNoAnimation2 = { animation: false }
  var myLineChart2 = new Chart(ctx2, {
    type: 'line',
    data: data2,
    options: basicOption2
  });
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////
  var ws = new WebSocket('wss://' + location.host);
  ws.onopen = function () {
    console.log('Successfully connect WebSocket');
  }
  ws.onmessage = function (message) {
    console.log('receive message' + message.data);
    try {
      var obj = JSON.parse(message.data);
      if(!obj.time || !obj.params.pm10) {
        return;
      }
      document.getElementById("pm2").innerHTML = obj.params.pm2;
  	  document.getElementById("pm10").innerHTML = obj.params.pm10;
	  document.getElementById("temp").innerHTML = obj.params.Temperature;
	  document.getElementById("humi").innerHTML = obj.params.Humidity;
	  document.getElementById("rpm").innerHTML = obj.params.rpm;
	  document.getElementById("rpm2").innerHTML = obj.params.rpm2;
	  var time = obj.time;
	  var subS = time.substring(13,19);
	  var hourS = time.substring(11,13);
	  var vv = parseInt(hourS);
	  var timeS = "";
	  vv = vv - 3;
	  if(vv<0)
		{
		  vv = vv + 24;
		}

		if(vv<10)
		{
			timeS = "0" + vv.toString() + subS;
		}
		else
		{
			timeS = vv.toString() + subS;
		}
	if(obj.params.Temperature)
	{
	  timeData.push(timeS);
      temperatureData.push(obj.params.Temperature);
	  tempimsi = obj.params.Temperature;
	  humiimsi = obj.params.Humidity;
	}
	else
	{
		timeData.push(timeS);
		document.getElementById("humi").innerHTML = humiimsi;
		var xxx = Math.floor((Math.random() * 2));
		temperatureData.push(tempimsi+xxx);
		document.getElementById("temp").innerHTML = tempimsi+xxx;
		
	}

      
      // only keep no more than 50 points in the line chart
      const maxLen = 10;
      var len = timeData.length;
      if (len > maxLen) {
        timeData.shift();
        temperatureData.shift();
      }
	  
	  
      if (obj.params.Humidity) {
        humidityData.push(obj.params.Humidity);
      }
      if (humidityData.length > maxLen) {
        humidityData.shift();
      }
	  if (obj.params.pm2) {
		  pm2Data.push(obj.params.pm2);
		  rpmData.push(obj.params.rpm);
		  rpm2Data.push(obj.params.rpm2);
	  }
	  if (pm2Data.length > maxLen)
	  {
		  pm2Data.shift();
	  }
	    
	    
	  if (rpmData.length > maxLen)
	  {
		  rpmData.shift();
	  }
	  if (rpm2Data.length > maxLen)
	  {
		  rpm2Data.shift();
	  }

// yangji, update data Start-------------------------------------------------------

if(obj.params.pm2>100){
  document.getElementById("pm25dis").innerHTML = "아주나쁨";
}else if(obj.params.pm2>50){
  document.getElementById("pm25dis").innerHTML = "나쁨";
}else if(obj.params.pm2>15){
  document.getElementById("pm25dis").innerHTML = "보통";
}else if(obj.params.pm2>0){
  document.getElementById("pm25dis").innerHTML = "좋음";
}
if(obj.params.pm10>150){
  document.getElementById("pm10dis").innerHTML = "아주나쁨";
}else if(obj.params.pm2>80){
  document.getElementById("pm10dis").innerHTML = "나쁨";
}else if(obj.params.pm2>30){
  document.getElementById("pm10dis").innerHTML = "보통";
}else if(obj.params.pm2>0){
  document.getElementById("pm10dis").innerHTML = "좋음";
}

// yangji, update data End-------------------------------------------------------


//graph tag start------------------------------------------------------------------
// if(obj.params.pm2>80){
// 	document.getElementById("pm25dis").innerHTML = "아주나쁨";
// }else if(obj.params.pm2>60){
// 	document.getElementById("pm25dis").innerHTML = "나쁨";
// }else if(obj.params.pm2>40){
// 	document.getElementById("pm25dis").innerHTML = "보통";
// }else if(obj.params.pm2>20){
// 	document.getElementById("pm25dis").innerHTML = "좋음";
// }else if(obj.params.pm2>0){
// 	document.getElementById("pm25dis").innerHTML = "아주좋음";
// }
// 	    if(obj.params.pm10>80){
// 	document.getElementById("pm10dis").innerHTML = "아주나쁨";
// }else if(obj.params.pm2>60){
// 	document.getElementById("pm10dis").innerHTML = "나쁨";
// }else if(obj.params.pm2>40){
// 	document.getElementById("pm10dis").innerHTML = "보통";
// }else if(obj.params.pm2>20){
// 	document.getElementById("pm10dis").innerHTML = "좋음";
// }else if(obj.params.pm2>0){
// 	document.getElementById("pm10dis").innerHTML = "아주좋음";
// }
if(obj.params.Temperature>30){
	document.getElementById("tempdis").innerHTML = "높음";
}else if(obj.params.Temperature>20){
	document.getElementById("tempdis").innerHTML = "쾌적";
}else if(obj.params.Temperature>0){
	document.getElementById("tempdis").innerHTML = "낮음";
}
	    if(obj.params.humi>70){
	document.getElementById("humidis").innerHTML = "습함";
}else if(obj.params.pm2>50){
	document.getElementById("humidis").innerHTML = "쾌적";
}else if(obj.params.pm2>0){
	document.getElementById("humidis").innerHTML = "건조";
}
	    if(obj.params.rpm  >1300){
	document.getElementById("rpm1dis").innerHTML = "강하게";
}else if(obj.params.rpm>1100){
	document.getElementById("rpm1dis").innerHTML = "중간";
}else if(obj.params.rpm>900){
	document.getElementById("rpm1dis").innerHTML = "약하게";
}else if(obj.params.rpm>=0){
	document.getElementById("rpm1dis").innerHTML = "정지";
}
	    	    if(obj.params.rpm2>1300){
	document.getElementById("rpm2dis").innerHTML = "";
}else if(obj.params.rpm2>1100){
	document.getElementById("rpm2dis").innerHTML = "중간";
}else if(obj.params.rpm2>900){
	document.getElementById("rpm2dis").innerHTML = "약하게";
}else if(obj.params.rpm2>=0){
	document.getElementById("rpm2dis").innerHTML = "정지";
}
//graph tag end-------------------------------------------------------------------
 myLineChart2.update();

      myLineChart.update();

	 


      
 //---------yanji start 2/2------------
 //20170913 pm Data push    
      pm10Data.push(obj.params.pm10);
      pm25Data.push(obj.params.pm2);
    
      //android 20170912 23:29
//       if(humilength==0 || templength == 0 || pm10length ==0 || pm25length ==0){
           
//            }
//           }else{
//             humilength = humidityData.length;
//             templength = temperatureData.length;
//             pm10length = pm10Data.length;
//             pm25length = pm25Data.length;
//            insertDatas(pm25Data[pm25length],humidityData[humilength],temperatureData[templength],humidityData[humilength]);
//         }
      //20170913
     if((pm25length<pm25Data.length || pm25length == pm25Data.length)&&(pm10length<pm10Data.length || pm10length == pm10Data.length)){
          pm25length = pm25Data.length;
          pm10length = pm10Data.length;
          insertDatas(pm25Data[pm25length-1],pm10Data[pm10length-1]);
                          
          }
     
      
      //android 20170912 23:29
      function insertDatas(p2,p1){
         var p2State;
         if(p2<16){
           p2State = "좋음";
         }else if(p2<51){
           p2State = "보통";
         }else if(p2<101){
           p2State = "나쁨";
         }else{
           p2State = "매우나쁨";
         }
         A2.showResult2(p2,p1,p2State);
      }
      
     
     
//---------yanji end 2/2------------
      
    } catch (err) {
      console.error(err);
    }
  }
});
