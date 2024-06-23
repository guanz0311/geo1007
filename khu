<html lang="ko">
<head>
    <meta charset="utf-8">
    <title>카카오맵 api를 이용한 &lt;서울특별시 대통령 선거 결과&gt; 지도</title>
    <style>
        .map_wrap {
            position: relative;
            overflow: hidden;
            width: 100%;
            height: 900px;
        }
        .radius_border {
            border: 3px solid #e9e9e9;
            border-radius: 10px;
        }
        .custom_typecontrol {
            position: absolute;
            top: 8px;
            left: 10px;
            overflow: hidden;
            width: 180px;
            height: 200px; /* Adjusted height to accommodate multiple buttons */
            margin: 0;
            padding: 0;
            z-index: 1;
            font-size: 12px;
            font-family: 'Malgun Gothic', '맑은 고딕', sans-serif;
            box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
        }
        .custom_typecontrol span {
            display: block;
            width: 100%;
            height: 40px;
            text-align: center;
            line-height: 40px;
            cursor: pointer;
            background: #fff;
            background: linear-gradient(#fff, #e6e6e6);
            border-radius: 5px;
            transition: background-color 0.3s ease, box-shadow 0.3s ease;
            margin-bottom: 1px; /* Space between buttons */
        }
        .custom_typecontrol span:hover {
            background: #f5f5f5;
            background: linear-gradient(#f5f5f5, #e3e3e3);
        }
        .custom_typecontrol span:active {
            background: #e6e6e6;
            background: linear-gradient(#e6e6e6, #fff);
        }
        .custom_zoomcontrol {
            position: absolute;
            top: 10px;
            right: 10px;
            width: 36px;
            height: 80px;
            overflow: hidden;
            z-index: 1;
            background-color: #f5f5f5;
            z-index: 10; /* 지도 위로 나타나도록 설정 */
        }
        .custom_zoomcontrol span {
            display: block;
            width: 36px;
            height: 40px;
            text-align: center;
            cursor: pointer;
        }
        .custom_zoomcontrol span img {
            width: 15px;
            height: 15px;
            padding: 12px 0;
            border: none;
        }
        .custom_zoomcontrol span:first-child {
            border-bottom: 1px solid #bfbfbf;
        }
        /* Style for the color legend */
        .legend {
            position: absolute;
            bottom: 10px;
            right: 10px;
            background: white;
            padding: 10px;
            box-shadow: 0 0 5px rgba(0,0,0,0.5);
            display: none; /* Initially hidden */
            flex-wrap: wrap; /* Ensure items wrap properly */
            z-index: 10; /* 지도 위로 나타나도록 설정 */
        }
        .legend-column {
            display: flex;
            flex-direction: column;
            margin-right: 10px;
        }
        .legend-item {
            display: flex;
            align-items: center;
            margin-bottom: 5px;
            flex-basis: 50%; /* Two items per column */
        }
        .legend-title {
            font-size: 15px; /* Increase the font size */
            font-family: Arial, sans-serif; /* Change the font to a more prominent style */
            text-align: left;
            color: #4646469d
            
        }
        .color-box {
            width: 20px;
            height: 20px;
            margin-right: 10px;
        }
        #출처 {
            position: absolute;
            bottom: 10px; /* 지도와 출처 박스의 하단 간격 */
            left: 10px;  /* 지도와 출처 박스의 좌측 간격 */
            padding: 5px 10px; /* 박스 내부의 여백 */
            background-color: white;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.253);
            border-radius: 5px;
            font-size: 15px;
            color: #333333;
            z-index: 10; /* 지도 위로 나타나도록 설정 */
        }

        /* 바범례 스타일*/
        .barlegend {
            position: absolute;
            bottom: 10px;
            right: 10px;
            background: white;
            padding: 15px;
            box-shadow: 0 0 5px rgba(0,0,0,0.5);
            display: none; /* Initially hidden */
            flex-wrap: wrap; /* Ensure items wrap properly */
            z-index: 10; /* 지도 위로 나타나도록 설정 */
            font-size: 12px;
            border-radius: 5px;
            font-family: 'Malgun Gothic', '맑은 고딕', sans-serif;
        }
        .barlegend-title {
            width: 100%;
            text-align: center;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .legend-bar {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 10px;
}
.bar-vertical {
    width: 10px; /* Adjust width as needed */
    height: 50px;
    background-color: rgb(255, 208, 21);
    margin-right: 5px;
}
        .legend-description {
            font-size: 11px;
            text-align: center;
            width: 100%;
            margin-top: 10px;
            border-top: 1px solid #ccc;
            padding-top: 5px;
        }
              
    .single-bar-container {
    position: absolute;
    bottom: 10px; /* Adjust as needed */
    right: 10px; /* Adjust as needed */
    width: 70%; /* 막대 전체 너비, 필요에 따라 조정 가능 */
    max-width: 600px; /* 최대 너비 */
    background: rgba(255, 255, 255, 0.8);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
    border-radius: 10px;
    padding: 10px;
    z-index: 10; /* 지도 위로 나타나도록 설정 */
    display: none; /* Initially hidden */
}

.candidate-info {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px; /* 막대와 후보자 정보 사이 간격 */
}

.candidate {
    display: flex;
    align-items: center;
}

.candidate.left {
    flex-direction: row; /* 사진이 왼쪽, 텍스트가 오른쪽 */
}

.candidate.right {
    flex-direction: row-reverse; /* 사진이 오른쪽, 텍스트가 왼쪽 */
}

.candidate img {
    width: 50px; /* 이미지 너비 조정 */
    height: auto;
    border-radius: 0%; /* 원형 이미지 */
    margin: 0 10px;
}

.candidate-text {
    text-align: center;
}

.single-bar {
    width: 100%;
    height: 30px; /* 막대 높이 */
    display: flex;
    border-radius: 10px;
    overflow: hidden;
}

.bar {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white; /* 텍스트 색상 */
    font-weight: bold;
}

.blue {
    background-color: #0B68B3;}

.red {
    background-color: #E61E2B;}

.gray {
    background-color: rgb(149, 149, 149);}
    
.green {background-color: rgb(86, 197, 46);}

.bar span {
    width: 100%; /* 텍스트가 막대 너비에 맞게 중앙 정렬 */
    text-align: center;
}

.single-bar-container.b {
    position: absolute;
    bottom: 10px; /* Adjust as needed */
    right: 10px; /* Adjust as needed */
    width: 70%; /* 막대 전체 너비, 필요에 따라 조정 가능 */
    max-width: 600px; /* 최대 너비 */
    background: rgba(255, 255, 255, 0.8);
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
    border-radius: 10px;
    padding: 10px;
    z-index: 10; /* 지도 위로 나타나도록 설정 */
    display: none; /* Initially hidden */
    
}

        /* 막대그래프 */
        .bar-chart {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .bar-chart {
            width: 10px; /* 막대 너비 */
            background-color: rgb(255, 208, 21); /* 막대 색상 */
            margin-bottom: 5px; /* 구 이름과의 간격 */
        }
        .bar-label {
            font-size: 10px;
            text-align: center;
        }


    </style>

    </style>
</head>

<body>
    <div id="출처">선거 자료출처: 중앙선거관리위원회<br>통계 자료출처: 서울시 열린데이터 광장</div>
      <div class="map_wrap">
        <div id="map-container" style="width: 100%; height: 80%;"></div>
        <div class="custom_typecontrol radius_border">
            <span id="togglePolygonA">[2017년] 제19대 대통령 선거</span>
            <span id="togglePolygonB">[2022년] 제20대 대통령 선거</span>
            <span id="togglePolygonC">제20대 대선[서울시 개표결과]</span>
            <span id="togglePolygonD">제20대 대선[서울시 인구통계]</span>
            <span id="togglePolygonE">제20대 대선[서울시 수준지수]</span>
        </div>
        
        <div class="custom_zoomcontrol radius_border">
            <span id="zoomIn"><img src="https://t1.daumcdn.net/localimg/localimages/07/mapapidoc/ico_plus.png" alt="확대"></span>
            <span id="zoomOut"><img src="https://t1.daumcdn.net/localimg/localimages/07/mapapidoc/ico_minus.png" alt="축소"></span>
        </div>
    </div>

    <div class="single-bar-container" id="single-bar-container">
        <div class="candidate-info">
            <div class="candidate left">
                <img src="https://cdn.news.unn.net/news/photo/201901/205439_86851_2512.png" alt="문재인">
                <div class="candidate-text">
                    기호1번<br>문재인<br>42.3%
                </div>
            </div>
            <div class="candidate right">
                <div class="candidate-text">
                    기호2번<br>홍준표<br>20.8% 
                </div>
                <img src="https://i.namu.wiki/i/ATBAE7rDuK28IG0cgmH8yKJJSp5b5dZW_nmB02q2JGHE09DiDnP43q02lK6J7lf0Adp2cMbtScXJ_oC-Gpcihw.webp" alt="홍준표">
            </div>
            <div class="candidate right">
                <div class="candidate-text">
                    기호3번<br>안철수<br>22.7% 
                </div>
                <img src="https://i.namu.wiki/i/Y58d47jXMn--NHvY-r-vnbF4an1R7vaawR6R6t1wM9Dz6aEmd8tTYwXpyyMqXSs3gOefdw1RKoR4Zk0ZLRpnsg.webp" alt="안철수">
            </div>
        </div>
        <div class="single-bar">
            <div class="bar blue" id="bar-blue" style="width: 42.3%;">
                <span>42.3%%</span>
            </div>
            <div class="bar red" id="bar-red" style="width: 20.8%;">
                <span>20.8%</span>
            </div>
            <div class="bar green" id="bar-green" style="width: 22.7%;">
                <span>22.7%</span>
            </div>
            <div class="bar gray" id="bar-gray" style="width: 14.2%;">
                <span>14.2%</span>
            </div>
        </div>
    </div>
    
    <div class="single-bar-container b" id="single-bar-container-b">
    <div class="candidate-info">
        <div class="candidate left">
            <img src="https://i.namu.wiki/i/veNzLdSHNcFF-aBqtUfD_Uk1OUUXnjwD_ISGP3GuEzx4EOINUWJ9_L1Jk__zprV8Ps-z7cmeOd2iGgHW5qL9oA.webp" alt="이재명">
            <div class="candidate-text">
                기호1번<br>이재명<br>45.8% 
            </div>
        </div>
        <div class="candidate right">
            <div class="candidate-text">
                기호2번<br>윤석열<br>50.5% 
            </div>
            <img src="https://img.asiatoday.co.kr/file/2023y/11m/10d/2023110901001067100058501.jpg" alt="윤석열">
        </div>
    </div>
    <div class="single-bar">
        <div class="bar blue" id="bar-blue-b" style="width: 45.8%;">
            <span>45.8%</span>
        </div>
        <div class="bar red" id="bar-red-b" style="width: 50.5%;">
            <span>50.5%</span>
        </div>
        <div class="bar gray" id="bar-gary-b" style="width: 4%;">
            <span>4%</span>
        </div>
    </div>
</div>

    <div class="legend" id="legend">
        <div class="legend-column">
            <div class="legend-column">
                          <div class="legend-column">
                <div class="legend-header" style="font-weight: bold;">더불어민주당 (후보 이재명)</div>
                <div class="legend-item">
                    <div class="color-box" style="background-color: #0074BD;"></div> 50% ~ 55%
                </div>
                <div class="legend-item">
                    <div class="color-box" style="background-color: #009EDF;"></div> 45% ~ 49.9%
                </div>
            </div>
            <div class="legend-header" style="font-weight: bold;">국민의힘 (후보 윤석열)</div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #7D160F;"></div> 65% ~ 70% 
            </div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #A61914;"></div> 60% ~ 64.9%
            </div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #D20D14;"></div> 55% ~ 59.9%
            </div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #E85239;"></div> 50% ~ 54.9%
            </div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #F18077;"></div> 45% ~ 49.9%
            </div>
        </div>
          <div class="legend-title" style="font-weight: bold;">마우스를 올리면 득표율이 보입니다.</div>
            </div>
    </div>

    <!-- 인구통계 범례 -->
    <div class="legend" id="demographic-legend" style="display:none;">
        <div class="legend-column">
            <div class="legend-item">
                <div class="color-box" style="background-color: #fffccd;"></div> 20~30대
            </div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #fff460;"></div> 40~60대
            </div>
            <div class="legend-item">
                <div class="color-box" style="background-color: #e8d800;"></div> 70대이상
            </div>
        </div>
    </div>
    
    <!-- 바범례 -->
    <div class="legend barlegend" id="barlegend">
        <div class="barlegend-title">자치구별 1인당 지역내총생산 및 수준지수(2015년 기준)</div>
        <div class="legend-bar">
            <div class="bar-vertical"></div>
            100%
        </div>
        <div class="legend-description">서울시 전체 1인당 지역내총생산 대비 자치구 1인당 지역내총생산의 수준</div>

    </div>

    <script src="//dapi.kakao.com/v2/maps/sdk.js?appkey=ea5c4da1be0c4db650f766d2185effb6"></script>
    <script>
        var mapContainer = document.getElementById('map-container');
        var mapOption = {
            center: new kakao.maps.LatLng(37.5665851, 126.9782038), // 용산구 중심 좌표
            level: 9, // 지도 레벨
            mapTypeId : kakao.maps.MapTypeId.ROADMAP // 지도 유형
        }; 

        var map = new kakao.maps.Map(mapContainer, mapOption); // 지도 생성 및 객체 리턴

        var districtCenters = {
            "강남구": { lat: 37.489167, lng: 127.066502 },
            "강동구": { lat: 37.551359, lng: 127.144802 },
            "강북구": { lat: 37.6391706, lng: 127.0106175 },
            "강서구": { lat: 37.5509507, lng: 126.8495322 },
            "관악구": { lat: 37.468935, lng: 126.945149 },
            "광진구": { lat: 37.5384843, lng: 127.0822939 },
            "구로구": { lat: 37.4954856, lng: 126.8874589 },
            "금천구": { lat: 37.4568209, lng: 126.8955617 },
            "노원구": { lat: 37.6449003, lng: 127.0758322 },
            "도봉구": { lat: 37.665577, lng: 127.0313997 },
            "동대문구": { lat: 37.580023, lng: 127.046576 },
            "동작구": { lat: 37.503653, lng: 126.946509 },
            "마포구": { lat: 37.5560685, lng: 126.910091 },
            "서대문구": { lat: 37.5792607, lng: 126.9364946 },
            "서초구": { lat: 37.4792903, lng: 127.0128613 },
            "성동구": { lat: 37.5504328, lng: 127.0348241 },
            "성북구": { lat: 37.5975051, lng: 127.0199016 },
            "송파구": { lat: 37.515455, lng: 127.110139 },
            "양천구": { lat: 37.5162019, lng: 126.8663496 },
            "영등포구": { lat: 37.521638, lng: 126.9049865 },
            "용산구": { lat: 37.5311008, lng: 126.9810742 },
            "은평구": { lat: 37.6028188, lng: 126.9291173 },
            "종로구": { lat:37.5953731, lng:126.9654376 },
            "중구": { lat: 37.561098, lng: 126.995229 },
            "중랑구": { lat: 37.598603, lng: 127.092882 }
        };

        var districtData = {
            "강남구": [32.3, 55.1, 12.4],
            "강동구": [31.9, 54.9, 13.1],
            "강북구": [28.2, 53.6, 17.6],
            "강서구": [35.8, 51.1, 13.4],
            "관악구": [44.5, 42.6, 12.9],
            "광진구": [38.3, 49.3, 12.1],
            "구로구": [32.5, 52.5, 15],
            "금천구": [35.6, 50.2, 14],
            "노원구": [29.9, 54.3, 15.7],
            "도봉구": [27.5, 55.2, 16.4],
            "동대문구": [35.3, 49.8, 14.7],
            "동작구": [37.2, 48.8, 13.7],
            "마포구": [38.7, 49.2, 12.1],
            "서대문구": [34.9, 50.5, 14.5],
            "서초구": [31.8, 55.5, 12.6],
            "성동구": [35.7, 51, 13.3],
            "성북구": [32.9, 52.4, 14.6],
            "송파구": [34.2, 53.7, 12],
            "양천구": [28.9, 57.9, 13.1],
            "영등포구": [38.8, 48, 13.1],
            "용산구": [35.7, 50.3, 13.9],
            "은평구": [31.3, 53.2, 15.4],
            "종로구": [33, 51.5, 15.1],
            "중구": [34 , 52,  13.9],
            "중랑구": [31.6, 53.3, 15]
        };

        var colors = ['#fffccd', '#fff460', '#e8d800'];


        function drawPieChart(center, data) {
            var total = data.reduce(function (a, b) {
                return a + b;
            }, 0);

            var currentAngle = -0.5 * Math.PI;
            var canvas = document.createElement('canvas');
            canvas.width = 60;
            canvas.height = 60;
            var ctx = canvas.getContext('2d');

            data.forEach(function (value, index) {
                var sliceAngle = (value / total) * 2 * Math.PI;
                var color = colors[index];

                ctx.beginPath();
                ctx.moveTo(30, 30);
                ctx.arc(30, 30, 30, currentAngle, currentAngle + sliceAngle);
                ctx.closePath();

                ctx.fillStyle = color;
                ctx.fill();

                // 비율 텍스트 표시
                var textAngle = currentAngle + sliceAngle / 2;
                var textX = 30 + 20 * Math.cos(textAngle);
                var textY = 30 + 20 * Math.sin(textAngle);
                ctx.fillStyle = '#000';
                ctx.font = '10px Arial';
                ctx.fillText(value + '%', textX - 10, textY + 3);

                currentAngle += sliceAngle;
            });

            var markerImage = new kakao.maps.MarkerImage(canvas.toDataURL(), new kakao.maps.Size(60, 60));
            var marker = new kakao.maps.Marker({
                position: new kakao.maps.LatLng(center.lat, center.lng),
                image: markerImage
            });
            return marker;
        }

        var markers = [];
        Object.keys(districtCenters).forEach(function(district) {
            var center = districtCenters[district];
            var data = districtData[district];
            markers.push(drawPieChart(center, data));
        });


                // 서울시 25개 구의 위치 및 막대그래프 값
                var seoulDistricts = {
            "강남구": { lat: 37.489167, lng: 127.066502, value: 312.72 },
            "강동구": { lat: 37.551359, lng: 127.144802, value: 41.70 },
            "강북구": { lat: 37.6391706, lng: 127.0106175, value: 23.66 },
            "강서구": { lat: 37.5509507, lng: 126.8495322, value: 65.84 },
            "관악구": { lat: 37.468935, lng: 126.945149, value: 25.75 },
            "광진구": { lat: 37.5384843, lng: 127.0822939, value: 37.71 },
            "구로구": { lat: 37.4954856, lng: 126.8874589, value: 68.73 },
            "금천구": { lat: 37.4568209, lng: 126.8955617, value: 144.46 },
            "노원구": { lat: 37.6449003, lng: 127.0758322, value: 26.83 },
            "도봉구": { lat: 37.665577, lng: 127.0313997, value: 22.61 },
            "동대문구": { lat: 37.580023, lng: 127.046576, value: 44.61 },
            "동작구": { lat: 37.503653, lng: 126.946509, value: 34.72 },
            "마포구": { lat: 37.5560685, lng: 126.910091, value: 117.97 },
            "서대문구": { lat: 37.5792607, lng: 126.9364946, value: 57.96 },
            "서초구": { lat: 37.4792903, lng: 127.0128613, value: 194.81 },
            "성동구": { lat: 37.5504328, lng: 127.0348241, value: 97.99 },
            "성북구": { lat: 37.5975051, lng: 127.0199016, value: 29.40 },
            "송파구": { lat: 37.515455, lng: 127.110139, value: 101.23 },
            "양천구": { lat: 37.5162019, lng: 126.8663496, value: 34.01 },
            "영등포구": { lat: 37.521638, lng: 126.9049865, value: 219.60 },
            "용산구": { lat: 37.5311008, lng: 126.9810742, value: 118.59 },
            "은평구": { lat: 37.6028188, lng: 126.9291173, value: 22.42 },
            "종로구": { lat: 37.5953731, lng: 126.9654376, value: 480.27 },
            "중구": { lat: 37.561098, lng: 126.995229, value: 968.98 },
            "중랑구": { lat: 37.598603, lng: 127.092882, value: 25.65 }
        };

        // 기준값 400
        var baseline = 400;

        // 막대그래프 추가 함수
        function addBarCharts(map) {
            for (var district in seoulDistricts) {
                var location = seoulDistricts[district];
                var height = (location.value / baseline) * 100; // 100을 기준으로 높이 비율 조정
                var content = '<div class="bar-chart">' +
                              '<div class="bar" style="height:' + height + 'px;"></div>' +
                              '<div class="bar-label">' + district + '<br>' + location.value + '</div>' +
                              '</div>';

                var position = new kakao.maps.LatLng(location.lat, location.lng);
                var customOverlay = new kakao.maps.CustomOverlay({
                    position: position,
                    content: content,
                    xAnchor: 0.5,
                    yAnchor: 1.0
                });
                customOverlay.setMap(map);
            }
        }

        // 용산구 다각형 생성 (19대선)
        var yongsanPolygonAPath = [
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.54413326436179, 127.00898460651953),
            new kakao.maps.LatLng(37.539639030116945, 127.00959054834321),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.52290225898471, 127.00614038053493),
            new kakao.maps.LatLng(37.51309192794448, 126.99070240960813),
            new kakao.maps.LatLng(37.50654651085339, 126.98553683648308),
            new kakao.maps.LatLng(37.50702053393398, 126.97524914998174),
            new kakao.maps.LatLng(37.51751820477105, 126.94988506562748),
            new kakao.maps.LatLng(37.52702918583156, 126.94987870367682),
            new kakao.maps.LatLng(37.534519656862926, 126.94481851935942),
            new kakao.maps.LatLng(37.537500243531994, 126.95335659960566),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.5541513366375, 126.9657135934734),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994)
        ];

        var yongsanPolygonA = new kakao.maps.Polygon({
            path: yongsanPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 동대문구 다각형 생성 (19대선)
        var dongdaemunPolygonAPath = [
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496),
            new kakao.maps.LatLng(37.60107201319839, 127.07287376670605),
            new kakao.maps.LatLng(37.59724304056685, 127.06949105186925),
            new kakao.maps.LatLng(37.58953367466315, 127.07030363208528),
            new kakao.maps.LatLng(37.58651213184981, 127.07264218709383),
            new kakao.maps.LatLng(37.5849555116177, 127.07216063016078),
            new kakao.maps.LatLng(37.58026781100598, 127.07619547037923),
            new kakao.maps.LatLng(37.571869232268774, 127.0782018408153),
            new kakao.maps.LatLng(37.559961773835425, 127.07239004251258),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.572878529071055, 127.04263554582458),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.57838361223621, 127.0232348231103),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5956815721534, 127.04062845365279),
            new kakao.maps.LatLng(37.5969637344377, 127.04302522879048),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496)
        ];

        var dongdaemunPolygonA = new kakao.maps.Polygon({
            path: dongdaemunPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성동구 다각형 생성(19대선)
        var seungdongPolygonAPath = [
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.5594131360664, 127.07373408220053),
            new kakao.maps.LatLng(37.52832388381049, 127.05621773388143),
            new kakao.maps.LatLng(37.53423885672233, 127.04604398310076),
            new kakao.maps.LatLng(37.53582328355087, 127.03979942567628),
            new kakao.maps.LatLng(37.53581367627865, 127.0211714455564),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53938672166098, 127.00993448922989),
            new kakao.maps.LatLng(37.54157804358092, 127.00879872996808),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706)
        ];

        var seungdongPolygonA = new kakao.maps.Polygon({
            path: seungdongPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 서대문구 다각형 생성(19대선)
        var seodaemunPolygonAPath = [
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003),
            new kakao.maps.LatLng(37.5992407011344, 126.95499403097206),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.5575156365052, 126.95991288916548),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.57599550420081, 126.902091747923),
            new kakao.maps.LatLng(37.587223103650295, 126.91284666446226),
            new kakao.maps.LatLng(37.58541570520177, 126.91531241017965),
            new kakao.maps.LatLng(37.585870567159255, 126.91638068573187),
            new kakao.maps.LatLng(37.583095195853055, 126.9159399866114),
            new kakao.maps.LatLng(37.583459593417196, 126.92175886498167),
            new kakao.maps.LatLng(37.587104600730505, 126.92388813813815),
            new kakao.maps.LatLng(37.588386594820484, 126.92800815682232),
            new kakao.maps.LatLng(37.59157595859555, 126.92776504133688),
            new kakao.maps.LatLng(37.59455434247408, 126.93027139545339),
            new kakao.maps.LatLng(37.59869748704149, 126.94088480070904),
            new kakao.maps.LatLng(37.60065830191363, 126.9414041615336),
            new kakao.maps.LatLng(37.60305781086164, 126.93995273804141),
            new kakao.maps.LatLng(37.610598531321436, 126.95037536795142),
            new kakao.maps.LatLng(37.6083605525023, 126.95056259057313),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003)
        ];

        var seodaemunPolygonA = new kakao.maps.Polygon({
            path: seodaemunPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 종로구 다각형 생성(19대선)
        var jongnoPolygonAPath = [
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046),
            new kakao.maps.LatLng(37.632194205253654, 126.97609588529602),
            new kakao.maps.LatLng(37.629026103322374, 126.97496405167149),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.60401657024552, 126.98665951539246),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.5788668917658, 127.02140099081309),
            new kakao.maps.LatLng(37.578034045208426, 127.02313962015988),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.5681357695346, 126.99014772014593),
            new kakao.maps.LatLng(37.569315246023024, 126.9732046364419),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.59875701675023, 126.95306020161668),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.60912809443569, 126.95032198271032),
            new kakao.maps.LatLng(37.615539700280216, 126.95072546923387),
            new kakao.maps.LatLng(37.62433621196653, 126.94900237336302),
            new kakao.maps.LatLng(37.62642708817027, 126.95037844036497),
            new kakao.maps.LatLng(37.629590994617104, 126.95881385457929),
            new kakao.maps.LatLng(37.629794440379136, 126.96376660599225),
            new kakao.maps.LatLng(37.632373740990175, 126.97302793692637),
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046)
        ];

        var jongnoPolygonA = new kakao.maps.Polygon({
            path: jongnoPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중구 다각형 생성(19대선)
        var jungPolygonAPath = [
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55487749311664, 126.97240854546743),
            new kakao.maps.LatLng(37.5548766923893, 126.9691718124876),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.55498984534305, 126.96173858545431),
            new kakao.maps.LatLng(37.55695455613004, 126.96343068837372),
            new kakao.maps.LatLng(37.5590262922649, 126.9616731414449),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.569485309984174, 126.97637402412326),
            new kakao.maps.LatLng(37.56810323716611, 126.98905202099309),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.572022763755164, 127.0223363152772),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56973041414113, 127.0234585247501),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894)
        ];

        var jungPolygonA = new kakao.maps.Polygon({
            path: jungPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 광진구 다각형 생성(19대선)
        var gwangjinPolygonAPath = [
    new kakao.maps.LatLng(37.5568724, 127.1153231),
    new kakao.maps.LatLng(37.5585233, 127.113965),
    new kakao.maps.LatLng(37.5590006, 127.112297),
    new kakao.maps.LatLng(37.5585538, 127.1095286),
    new kakao.maps.LatLng(37.5564601, 127.1063932),
    new kakao.maps.LatLng(37.5595269, 127.1019134),
    new kakao.maps.LatLng(37.5616054, 127.1012509),
    new kakao.maps.LatLng(37.5643129, 127.1023143),
    new kakao.maps.LatLng(37.5701103, 127.1035059),
    new kakao.maps.LatLng(37.5714514, 127.104295),
    new kakao.maps.LatLng(37.5724694, 127.1017021),
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.5679178, 127.0768757),
    new kakao.maps.LatLng(37.5645904, 127.0740989),
    new kakao.maps.LatLng(37.5599603, 127.0723852),
    new kakao.maps.LatLng(37.559414, 127.0737358),
    new kakao.maps.LatLng(37.5393084, 127.0623676),
    new kakao.maps.LatLng(37.539291, 127.0623585),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5268818, 127.0607945),
    new kakao.maps.LatLng(37.523872, 127.0686631),
    new kakao.maps.LatLng(37.522514, 127.0769544),
    new kakao.maps.LatLng(37.5229485, 127.0799746),
    new kakao.maps.LatLng(37.524759, 127.0856328),
    new kakao.maps.LatLng(37.5270069, 127.090161),
    new kakao.maps.LatLng(37.5414079, 127.1082818),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5469267, 127.1114708),
    new kakao.maps.LatLng(37.5504987, 127.1115571),
    new kakao.maps.LatLng(37.5543662, 127.1143095),
    new kakao.maps.LatLng(37.5568724, 127.1153231)
];  
        var gwangjinPolygonA = new kakao.maps.Polygon({
            path: gwangjinPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중량구 다각형 생성(19대선)
        var jungnangPolygonAPath = [
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.5760708, 127.1011435),
    new kakao.maps.LatLng(37.578907, 127.1030254),
    new kakao.maps.LatLng(37.5805343, 127.103429),
    new kakao.maps.LatLng(37.5833044, 127.109002),
    new kakao.maps.LatLng(37.5891647, 127.1106433),
    new kakao.maps.LatLng(37.5932091, 127.1131972),
    new kakao.maps.LatLng(37.5940164, 127.1166645),
    new kakao.maps.LatLng(37.5954971, 127.1168775),
    new kakao.maps.LatLng(37.599521, 127.1140639),
    new kakao.maps.LatLng(37.6021085, 127.1157227),
    new kakao.maps.LatLng(37.6046024, 127.118047),
    new kakao.maps.LatLng(37.607613, 127.1184769),
    new kakao.maps.LatLng(37.6088335, 127.1166833),
    new kakao.maps.LatLng(37.6118276, 127.1174901),
    new kakao.maps.LatLng(37.6160155, 127.1166717),
    new kakao.maps.LatLng(37.6178884, 127.1171467),
    new kakao.maps.LatLng(37.6195377, 127.115021),
    new kakao.maps.LatLng(37.6210546, 127.110519),
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6153366, 127.0701774),
    new kakao.maps.LatLng(37.6153196, 127.0702079),
    new kakao.maps.LatLng(37.6135142, 127.0717529),
    new kakao.maps.LatLng(37.6070224, 127.0711169),
    new kakao.maps.LatLng(37.6046424, 127.0715334),
    new kakao.maps.LatLng(37.6013304, 127.0728729),
    new kakao.maps.LatLng(37.600246, 127.0724977),
    new kakao.maps.LatLng(37.5972431, 127.069494),
    new kakao.maps.LatLng(37.5951242, 127.0694344),
    new kakao.maps.LatLng(37.5919078, 127.0707184),
    new kakao.maps.LatLng(37.5899586, 127.070228),
    new kakao.maps.LatLng(37.5865116, 127.0726438),
    new kakao.maps.LatLng(37.5849569, 127.0721613),
    new kakao.maps.LatLng(37.5793357, 127.076458),
    new kakao.maps.LatLng(37.5729206, 127.0772314),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5737318, 127.1008637)
];

        var jungnangPolygonA = new kakao.maps.Polygon({
            path: jungnangPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성북구 다각형 생성(19대선)
        var seongbukPolygonAPath = [
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235),
            new kakao.maps.LatLng(37.631446839436855, 126.99372381657889),
            new kakao.maps.LatLng(37.626192451322005, 126.99927047335905),
            new kakao.maps.LatLng(37.62382095469671, 127.00488450145781),
            new kakao.maps.LatLng(37.624026217174986, 127.00788862747375),
            new kakao.maps.LatLng(37.6205124078061, 127.00724034082933),
            new kakao.maps.LatLng(37.61679651952433, 127.01014412786792),
            new kakao.maps.LatLng(37.61472018601129, 127.01451127202589),
            new kakao.maps.LatLng(37.614629670135216, 127.01757841621624),
            new kakao.maps.LatLng(37.61137091590441, 127.02219857751122),
            new kakao.maps.LatLng(37.612692696824915, 127.02642583551054),
            new kakao.maps.LatLng(37.612367438936786, 127.03018593770908),
            new kakao.maps.LatLng(37.60896889076571, 127.0302525167858),
            new kakao.maps.LatLng(37.61279787695882, 127.03730791358603),
            new kakao.maps.LatLng(37.62426467261789, 127.04973339977498),
            new kakao.maps.LatLng(37.61449950127667, 127.06174181124696),
            new kakao.maps.LatLng(37.61561580859776, 127.06985247014711),
            new kakao.maps.LatLng(37.61351359068103, 127.07170798866412),
            new kakao.maps.LatLng(37.60762512162974, 127.07105453180604),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.59644879095525, 127.04184728392097),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.57782865303167, 127.02296295333255),
            new kakao.maps.LatLng(37.57889204835333, 127.02179043639809),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.60451393107786, 126.98678626394351),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.62980449548538, 126.97468284124939),
            new kakao.maps.LatLng(37.633657663246694, 126.97740053878216),
            new kakao.maps.LatLng(37.63476479485093, 126.98154674721893),
            new kakao.maps.LatLng(37.63780700422825, 126.9849494717052),
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235)
        ];

        var seongbukPolygonA = new kakao.maps.Polygon({
            path: seongbukPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강북구 다각형 생성(19대선)
        var gangbukPolygonAPath = [
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6850889, 127.0045265),
    new kakao.maps.LatLng(37.6834224, 126.9973582),
    new kakao.maps.LatLng(37.678828, 126.9929755),
    new kakao.maps.LatLng(37.6757199, 126.9931995),
    new kakao.maps.LatLng(37.672422, 126.9942076),
    new kakao.maps.LatLng(37.6678322, 126.993576),
    new kakao.maps.LatLng(37.6670301, 126.9941291),
    new kakao.maps.LatLng(37.6652317, 126.9922245),
    new kakao.maps.LatLng(37.6643912, 126.9882682),
    new kakao.maps.LatLng(37.6606003, 126.9872768),
    new kakao.maps.LatLng(37.6589432, 126.9860205),
    new kakao.maps.LatLng(37.6570035, 126.9830101),
    new kakao.maps.LatLng(37.6560387, 126.9796581),
    new kakao.maps.LatLng(37.6548152, 126.9799441),
    new kakao.maps.LatLng(37.6505404, 126.9824953),
    new kakao.maps.LatLng(37.64961, 126.9839369),
    new kakao.maps.LatLng(37.6457101, 126.9850955),
    new kakao.maps.LatLng(37.6436716, 126.9832554),
    new kakao.maps.LatLng(37.6400446, 126.9856762),
    new kakao.maps.LatLng(37.6363484, 126.9841726),
    new kakao.maps.LatLng(37.6340757, 126.9894095),
    new kakao.maps.LatLng(37.6302496, 126.9953935),
    new kakao.maps.LatLng(37.6262023, 126.999273),
    new kakao.maps.LatLng(37.625951, 127.0000402),
    new kakao.maps.LatLng(37.6259335, 127.0000628),
    new kakao.maps.LatLng(37.6242258, 127.0038971),
    new kakao.maps.LatLng(37.6240272, 127.0078883),
    new kakao.maps.LatLng(37.6208272, 127.0072158),
    new kakao.maps.LatLng(37.618622, 127.0085),
    new kakao.maps.LatLng(37.6162859, 127.0109519),
    new kakao.maps.LatLng(37.6146854, 127.0144744),
    new kakao.maps.LatLng(37.6146161, 127.0175368),
    new kakao.maps.LatLng(37.6113717, 127.0221965),
    new kakao.maps.LatLng(37.6126938, 127.0264334),
    new kakao.maps.LatLng(37.6123662, 127.0301844),
    new kakao.maps.LatLng(37.6089762, 127.0302524),
    new kakao.maps.LatLng(37.6129618, 127.0375131),
    new kakao.maps.LatLng(37.6157606, 127.0399847),
    new kakao.maps.LatLng(37.6186436, 127.0439485),
    new kakao.maps.LatLng(37.6226012, 127.0468685),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6843696, 127.0086619)
];

        var gangbukPolygonA = new kakao.maps.Polygon({
            path: gangbukPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 도봉구 다각형 생성(19대선)
        var dobongPolygonAPath = [
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6879759, 127.0498208),
    new kakao.maps.LatLng(37.6908702, 127.0499658),
    new kakao.maps.LatLng(37.6940664, 127.0486327),
    new kakao.maps.LatLng(37.6923802, 127.0456492),
    new kakao.maps.LatLng(37.693687, 127.043083),
    new kakao.maps.LatLng(37.6952354, 127.0430909),
    new kakao.maps.LatLng(37.6952919, 127.0411383),
    new kakao.maps.LatLng(37.6926381, 127.0368093),
    new kakao.maps.LatLng(37.6918448, 127.0324625),
    new kakao.maps.LatLng(37.6930733, 127.0310969),
    new kakao.maps.LatLng(37.6962653, 127.0297701),
    new kakao.maps.LatLng(37.6992843, 127.0293125),
    new kakao.maps.LatLng(37.7009462, 127.02771),
    new kakao.maps.LatLng(37.6995947, 127.0253836),
    new kakao.maps.LatLng(37.6997207, 127.0221482),
    new kakao.maps.LatLng(37.7010174, 127.0198271),
    new kakao.maps.LatLng(37.7014553, 127.0154151),
    new kakao.maps.LatLng(37.6988007, 127.0138784),
    new kakao.maps.LatLng(37.6973775, 127.0121243),
    new kakao.maps.LatLng(37.6966991, 127.0096662),
    new kakao.maps.LatLng(37.6933154, 127.0097568),
    new kakao.maps.LatLng(37.6915772, 127.007678),
    new kakao.maps.LatLng(37.6900533, 127.0083369),
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6858137, 127.0518033)
];

        var dobongPolygonA = new kakao.maps.Polygon({
            path: dobongPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 노원구 다각형 생성(19대선)
        var nowonPolygonAPath = [
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6216472, 127.1040704),
    new kakao.maps.LatLng(37.6275838, 127.1059087),
    new kakao.maps.LatLng(37.6293016, 127.1088847),
    new kakao.maps.LatLng(37.6315033, 127.1116324),
    new kakao.maps.LatLng(37.6326429, 127.1122035),
    new kakao.maps.LatLng(37.6364891, 127.1124833),
    new kakao.maps.LatLng(37.6391262, 127.1105493),
    new kakao.maps.LatLng(37.6398412, 127.1120504),
    new kakao.maps.LatLng(37.6425246, 127.1108099),
    new kakao.maps.LatLng(37.6426948, 127.1093228),
    new kakao.maps.LatLng(37.6451721, 127.1067673),
    new kakao.maps.LatLng(37.6452258, 127.1028086),
    new kakao.maps.LatLng(37.6439649, 127.0975589),
    new kakao.maps.LatLng(37.6445705, 127.09457),
    new kakao.maps.LatLng(37.6496973, 127.0924745),
    new kakao.maps.LatLng(37.6524386, 127.0940495),
    new kakao.maps.LatLng(37.6537758, 127.0930673),
    new kakao.maps.LatLng(37.6593346, 127.0912069),
    new kakao.maps.LatLng(37.6632988, 127.0941422),
    new kakao.maps.LatLng(37.6675788, 127.095017),
    new kakao.maps.LatLng(37.6687685, 127.0962455),
    new kakao.maps.LatLng(37.6727011, 127.0957715),
    new kakao.maps.LatLng(37.673564, 127.0946559),
    new kakao.maps.LatLng(37.6767064, 127.0938558),
    new kakao.maps.LatLng(37.6786397, 127.0919859),
    new kakao.maps.LatLng(37.6814411, 127.0929524),
    new kakao.maps.LatLng(37.6855375, 127.0964162),
    new kakao.maps.LatLng(37.689071, 127.095996),
    new kakao.maps.LatLng(37.6899664, 127.0930367),
    new kakao.maps.LatLng(37.6895704, 127.0905519),
    new kakao.maps.LatLng(37.6899122, 127.0865306),
    new kakao.maps.LatLng(37.6917823, 127.083905),
    new kakao.maps.LatLng(37.694269, 127.0838433),
    new kakao.maps.LatLng(37.6961376, 127.0811047),
    new kakao.maps.LatLng(37.6959864, 127.0781963),
    new kakao.maps.LatLng(37.6951465, 127.0748951),
    new kakao.maps.LatLng(37.6937786, 127.0727908),
    new kakao.maps.LatLng(37.6939832, 127.0686396),
    new kakao.maps.LatLng(37.6949371, 127.0634232),
    new kakao.maps.LatLng(37.6930035, 127.0624128),
    new kakao.maps.LatLng(37.6902838, 127.0597139),
    new kakao.maps.LatLng(37.6892048, 127.0551791),
    new kakao.maps.LatLng(37.6870667, 127.0518042),
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6197959, 127.0544081),
    new kakao.maps.LatLng(37.6174813, 127.0574206),
    new kakao.maps.LatLng(37.6142587, 127.0632852),
    new kakao.maps.LatLng(37.6157243, 127.0697122),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.6203794, 127.105654)
];

        var nowonPolygonA = new kakao.maps.Polygon({
            path: nowonPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 은평구 다각형 생성(19대선)
        var eunpyeongPolygonAPath = [
    new kakao.maps.LatLng(37.6295893, 126.9588137),
    new kakao.maps.LatLng(37.62973, 126.9597977),
    new kakao.maps.LatLng(37.6332338, 126.9634013),
    new kakao.maps.LatLng(37.6357828, 126.9626334),
    new kakao.maps.LatLng(37.6421387, 126.9593275),
    new kakao.maps.LatLng(37.6467834, 126.959027),
    new kakao.maps.LatLng(37.6480477, 126.9578392),
    new kakao.maps.LatLng(37.6528372, 126.9571078),
    new kakao.maps.LatLng(37.6546009, 126.9543453),
    new kakao.maps.LatLng(37.6549496, 126.9513757),
    new kakao.maps.LatLng(37.6571298, 126.9478961),
    new kakao.maps.LatLng(37.6592154, 126.9475649),
    new kakao.maps.LatLng(37.6577222, 126.9421),
    new kakao.maps.LatLng(37.6566359, 126.9401282),
    new kakao.maps.LatLng(37.6523011, 126.9371587),
    new kakao.maps.LatLng(37.6511999, 126.9357024),
    new kakao.maps.LatLng(37.6500481, 126.9296991),
    new kakao.maps.LatLng(37.6461063, 126.9241229),
    new kakao.maps.LatLng(37.6447557, 126.9137208),
    new kakao.maps.LatLng(37.6476455, 126.9095352),
    new kakao.maps.LatLng(37.6486884, 126.905964),
    new kakao.maps.LatLng(37.6462898, 126.9077049),
    new kakao.maps.LatLng(37.6442586, 126.9122604),
    new kakao.maps.LatLng(37.6385095, 126.9100918),
    new kakao.maps.LatLng(37.6353165, 126.9108542),
    new kakao.maps.LatLng(37.633398, 126.9070962),
    new kakao.maps.LatLng(37.6308672, 126.9072938),
    new kakao.maps.LatLng(37.6293276, 126.9087697),
    new kakao.maps.LatLng(37.6262657, 126.9086108),
    new kakao.maps.LatLng(37.6244956, 126.9066268),
    new kakao.maps.LatLng(37.6219415, 126.9071175),
    new kakao.maps.LatLng(37.6207039, 126.9056125),
    new kakao.maps.LatLng(37.6190745, 126.9052311),
    new kakao.maps.LatLng(37.6188394, 126.903361),
    new kakao.maps.LatLng(37.6157535, 126.9018223),
    new kakao.maps.LatLng(37.6140692, 126.9017342),
    new kakao.maps.LatLng(37.6111913, 126.9003043),
    new kakao.maps.LatLng(37.6037417, 126.9021083),
    new kakao.maps.LatLng(37.6020402, 126.8999819),
    new kakao.maps.LatLng(37.5993665, 126.9013224),
    new kakao.maps.LatLng(37.5973371, 126.9010115),
    new kakao.maps.LatLng(37.5951135, 126.9018381),
    new kakao.maps.LatLng(37.5926784, 126.8989613),
    new kakao.maps.LatLng(37.589938, 126.8997501),
    new kakao.maps.LatLng(37.5885666, 126.896859),
    new kakao.maps.LatLng(37.5890755, 126.8932905),
    new kakao.maps.LatLng(37.5885221, 126.8922355),
    new kakao.maps.LatLng(37.5885328, 126.8871589),
    new kakao.maps.LatLng(37.5895376, 126.8858088),
    new kakao.maps.LatLng(37.593639, 126.885004),
    new kakao.maps.LatLng(37.5907926, 126.8820561),
    new kakao.maps.LatLng(37.5907588, 126.882095),
    new kakao.maps.LatLng(37.588347, 126.8845533),
    new kakao.maps.LatLng(37.5876412, 126.8852568),
    new kakao.maps.LatLng(37.5870924, 126.8858291),
    new kakao.maps.LatLng(37.5860266, 126.8871243),
    new kakao.maps.LatLng(37.5858059, 126.8874045),
    new kakao.maps.LatLng(37.5815606, 126.8937787),
    new kakao.maps.LatLng(37.5794888, 126.8969354),
    new kakao.maps.LatLng(37.5782229, 126.898808),
    new kakao.maps.LatLng(37.5765458, 126.901833),
    new kakao.maps.LatLng(37.5787907, 126.9044431),
    new kakao.maps.LatLng(37.5803263, 126.9060741),
    new kakao.maps.LatLng(37.58547, 126.9115429),
    new kakao.maps.LatLng(37.5865298, 126.9124768),
    new kakao.maps.LatLng(37.5868917, 126.9126854),
    new kakao.maps.LatLng(37.5870633, 126.9127725),
    new kakao.maps.LatLng(37.5862014, 126.9151912),
    new kakao.maps.LatLng(37.5860447, 126.9155519),
    new kakao.maps.LatLng(37.5853667, 126.9160692),
    new kakao.maps.LatLng(37.5853601, 126.9160646),
    new kakao.maps.LatLng(37.5843543, 126.9156798),
    new kakao.maps.LatLng(37.5837821, 126.9157485),
    new kakao.maps.LatLng(37.5831718, 126.9164206),
    new kakao.maps.LatLng(37.58325, 126.9178162),
    new kakao.maps.LatLng(37.5829392, 126.920859),
    new kakao.maps.LatLng(37.5838591, 126.9218276),
    new kakao.maps.LatLng(37.5846767, 126.9218555),
    new kakao.maps.LatLng(37.5852834, 126.9223929),
    new kakao.maps.LatLng(37.5856304, 126.9228635),
    new kakao.maps.LatLng(37.5869714, 126.923861),
    new kakao.maps.LatLng(37.5871207, 126.9240038),
    new kakao.maps.LatLng(37.5872166, 126.9246107),
    new kakao.maps.LatLng(37.5872168, 126.9252644),
    new kakao.maps.LatLng(37.5883854, 126.928009),
    new kakao.maps.LatLng(37.5911032, 126.927947),
    new kakao.maps.LatLng(37.5915762, 126.9277682),
    new kakao.maps.LatLng(37.5945528, 126.9302704),
    new kakao.maps.LatLng(37.5962984, 126.9327954),
    new kakao.maps.LatLng(37.5974786, 126.9364086),
    new kakao.maps.LatLng(37.5976207, 126.9382703),
    new kakao.maps.LatLng(37.5987329, 126.9408662),
    new kakao.maps.LatLng(37.6006774, 126.9413766),
    new kakao.maps.LatLng(37.6013511, 126.9407255),
    new kakao.maps.LatLng(37.6049576, 126.9421378),
    new kakao.maps.LatLng(37.6086085, 126.9482139),
    new kakao.maps.LatLng(37.609399, 126.9489364),
    new kakao.maps.LatLng(37.6138494, 126.9507966),
    new kakao.maps.LatLng(37.6155379, 126.9507242),
    new kakao.maps.LatLng(37.6199205, 126.9499112),
    new kakao.maps.LatLng(37.6207316, 126.9499381),
    new kakao.maps.LatLng(37.6209324, 126.9499158),
    new kakao.maps.LatLng(37.6232616, 126.9488984),
    new kakao.maps.LatLng(37.626418, 126.9504537),
    new kakao.maps.LatLng(37.6265452, 126.9516053),
    new kakao.maps.LatLng(37.628731, 126.956889),
    new kakao.maps.LatLng(37.6295893, 126.9588137)
];

        var eunpyeongPolygonA = new kakao.maps.Polygon({
            path: eunpyeongPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 마포구 다각형 생성(19대선)
        var mapoPolygonAPath = [
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.55675317809392, 126.93190919632814),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.557241466445234, 126.95913438471307),
            new kakao.maps.LatLng(37.55908394430372, 126.96163689468189),
            new kakao.maps.LatLng(37.55820141918588, 126.96305432966605),
            new kakao.maps.LatLng(37.554784413504734, 126.9617251098019),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.539468942052544, 126.955731506394),
            new kakao.maps.LatLng(37.536292068277106, 126.95128907260018),
            new kakao.maps.LatLng(37.53569162926515, 126.94627494388307),
            new kakao.maps.LatLng(37.53377712226906, 126.94458373402794),
            new kakao.maps.LatLng(37.54135238063506, 126.93031191951576),
            new kakao.maps.LatLng(37.539036674424615, 126.9271006565075),
            new kakao.maps.LatLng(37.54143034750605, 126.9224138272872),
            new kakao.maps.LatLng(37.54141748538761, 126.90483000187002),
            new kakao.maps.LatLng(37.548015078285694, 126.89890097452322),
            new kakao.maps.LatLng(37.56300401736817, 126.86623824787709),
            new kakao.maps.LatLng(37.57178997971358, 126.85363039091744),
            new kakao.maps.LatLng(37.57379738998644, 126.85362646212587),
            new kakao.maps.LatLng(37.57747251471329, 126.864939928088),
            new kakao.maps.LatLng(37.5781913017327, 126.87625939970273),
            new kakao.maps.LatLng(37.57977132158497, 126.87767870371688),
            new kakao.maps.LatLng(37.584440882833654, 126.87653889183002),
            new kakao.maps.LatLng(37.59079311146897, 126.88205386700724),
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884)
        ];

        var mapoPolygonA = new kakao.maps.Polygon({
            path: mapoPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 양천구 다각형 생성(19대선)
        var yangcheonPolygonAPath = [
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5397562, 126.8216026),
    new kakao.maps.LatLng(37.5365431, 126.8224338),
    new kakao.maps.LatLng(37.5348887, 126.821878),
    new kakao.maps.LatLng(37.5299154, 126.8254181),
    new kakao.maps.LatLng(37.528389, 126.8279799),
    new kakao.maps.LatLng(37.5258342, 126.8281793),
    new kakao.maps.LatLng(37.5249238, 126.8264622),
    new kakao.maps.LatLng(37.5230079, 126.8251384),
    new kakao.maps.LatLng(37.5198753, 126.8255944),
    new kakao.maps.LatLng(37.516186, 126.8231123),
    new kakao.maps.LatLng(37.5130434, 126.8244262),
    new kakao.maps.LatLng(37.5090953, 126.8239041),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5187577, 126.8782517),
    new kakao.maps.LatLng(37.5203627, 126.879464),
    new kakao.maps.LatLng(37.5252536, 126.878749),
    new kakao.maps.LatLng(37.5259082, 126.8809399),
    new kakao.maps.LatLng(37.5287593, 126.8843314),
    new kakao.maps.LatLng(37.5301503, 126.8871006),
    new kakao.maps.LatLng(37.5301524, 126.8896671),
    new kakao.maps.LatLng(37.5319258, 126.8890681),
    new kakao.maps.LatLng(37.5351351, 126.8897886),
    new kakao.maps.LatLng(37.5397825, 126.8863138),
    new kakao.maps.LatLng(37.543321, 126.885088),
    new kakao.maps.LatLng(37.5481962, 126.880664),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.546944, 126.8745052)
];

        var yangcheonPolygonA = new kakao.maps.Polygon({
            path: yangcheonPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강서구 다각형 생성(19대선)
        var gangseoPolygonAPath = [
    new kakao.maps.LatLng(37.5717904, 126.8536316),
    new kakao.maps.LatLng(37.5737991, 126.8536283),
    new kakao.maps.LatLng(37.5745142, 126.8510083),
    new kakao.maps.LatLng(37.5773942, 126.8467014),
    new kakao.maps.LatLng(37.5835872, 126.8327892),
    new kakao.maps.LatLng(37.588201, 126.8270511),
    new kakao.maps.LatLng(37.5900825, 126.8252892),
    new kakao.maps.LatLng(37.5912976, 126.822785),
    new kakao.maps.LatLng(37.5976193, 126.8139529),
    new kakao.maps.LatLng(37.5989607, 126.8113687),
    new kakao.maps.LatLng(37.604902, 126.8027567),
    new kakao.maps.LatLng(37.6024867, 126.7999484),
    new kakao.maps.LatLng(37.6013474, 126.7998667),
    new kakao.maps.LatLng(37.5998709, 126.7978909),
    new kakao.maps.LatLng(37.597712, 126.797114),
    new kakao.maps.LatLng(37.5947537, 126.797721),
    new kakao.maps.LatLng(37.5936525, 126.798726),
    new kakao.maps.LatLng(37.5913058, 126.7988344),
    new kakao.maps.LatLng(37.589326, 126.8012524),
    new kakao.maps.LatLng(37.5878099, 126.8007605),
    new kakao.maps.LatLng(37.5880729, 126.7987679),
    new kakao.maps.LatLng(37.583364, 126.7956796),
    new kakao.maps.LatLng(37.5797103, 126.7924063),
    new kakao.maps.LatLng(37.5805208, 126.7907535),
    new kakao.maps.LatLng(37.5777706, 126.790599),
    new kakao.maps.LatLng(37.5777198, 126.7893694),
    new kakao.maps.LatLng(37.5755709, 126.787642),
    new kakao.maps.LatLng(37.5735993, 126.7824424),
    new kakao.maps.LatLng(37.5692071, 126.7816643),
    new kakao.maps.LatLng(37.5672821, 126.7789707),
    new kakao.maps.LatLng(37.5670966, 126.776366),
    new kakao.maps.LatLng(37.5658733, 126.7751607),
    new kakao.maps.LatLng(37.5637152, 126.7771261),
    new kakao.maps.LatLng(37.5618635, 126.7761087),
    new kakao.maps.LatLng(37.5572273, 126.7698955),
    new kakao.maps.LatLng(37.5554503, 126.7645763),
    new kakao.maps.LatLng(37.5539545, 126.7676412),
    new kakao.maps.LatLng(37.551962, 126.7674713),
    new kakao.maps.LatLng(37.5515813, 126.7693259),
    new kakao.maps.LatLng(37.548316, 126.7717031),
    new kakao.maps.LatLng(37.5489742, 126.7752973),
    new kakao.maps.LatLng(37.54671, 126.7775751),
    new kakao.maps.LatLng(37.5460749, 126.7818371),
    new kakao.maps.LatLng(37.545997, 126.7869552),
    new kakao.maps.LatLng(37.5438485, 126.7907616),
    new kakao.maps.LatLng(37.541761, 126.7921302),
    new kakao.maps.LatLng(37.541372, 126.7949442),
    new kakao.maps.LatLng(37.5395572, 126.7938932),
    new kakao.maps.LatLng(37.5373674, 126.7939734),
    new kakao.maps.LatLng(37.5367714, 126.7961149),
    new kakao.maps.LatLng(37.5378446, 126.7994886),
    new kakao.maps.LatLng(37.5403453, 126.7988931),
    new kakao.maps.LatLng(37.5408808, 126.8008976),
    new kakao.maps.LatLng(37.5426716, 126.8016672),
    new kakao.maps.LatLng(37.5436059, 126.8068721),
    new kakao.maps.LatLng(37.5407765, 126.8125684),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5484626, 126.8804437),
    new kakao.maps.LatLng(37.5494053, 126.8798959),
    new kakao.maps.LatLng(37.5497628, 126.8796001),
    new kakao.maps.LatLng(37.5499377, 126.8794778),
    new kakao.maps.LatLng(37.5500282, 126.8794146),
    new kakao.maps.LatLng(37.550412, 126.8791236),
    new kakao.maps.LatLng(37.5507488, 126.8788459),
    new kakao.maps.LatLng(37.5511263, 126.8787108),
    new kakao.maps.LatLng(37.5515205, 126.8781985),
    new kakao.maps.LatLng(37.5519352, 126.8780413),
    new kakao.maps.LatLng(37.5523189, 126.8780313),
    new kakao.maps.LatLng(37.5525651, 126.8780226),
    new kakao.maps.LatLng(37.5527979, 126.8780142),
    new kakao.maps.LatLng(37.5529934, 126.8780067),
    new kakao.maps.LatLng(37.5531701, 126.8779519),
    new kakao.maps.LatLng(37.5532133, 126.8779456),
    new kakao.maps.LatLng(37.5534501, 126.8779539),
    new kakao.maps.LatLng(37.5535245, 126.8780551),
    new kakao.maps.LatLng(37.553546, 126.8781144),
    new kakao.maps.LatLng(37.5535815, 126.8782443),
    new kakao.maps.LatLng(37.5533372, 126.878835),
    new kakao.maps.LatLng(37.5532765, 126.8789601),
    new kakao.maps.LatLng(37.5531512, 126.8792171),
    new kakao.maps.LatLng(37.5537026, 126.879224),
    new kakao.maps.LatLng(37.554747, 126.879237),
    new kakao.maps.LatLng(37.5550643, 126.8794927),
    new kakao.maps.LatLng(37.555305, 126.879688),
    new kakao.maps.LatLng(37.556224, 126.8804278),
    new kakao.maps.LatLng(37.5562828, 126.8804743),
    new kakao.maps.LatLng(37.5565904, 126.8798677),
    new kakao.maps.LatLng(37.5566999, 126.8796536),
    new kakao.maps.LatLng(37.5569932, 126.8790797),
    new kakao.maps.LatLng(37.5571835, 126.8787108),
    new kakao.maps.LatLng(37.5577477, 126.8776168),
    new kakao.maps.LatLng(37.5580956, 126.8769422),
    new kakao.maps.LatLng(37.5582839, 126.8765751),
    new kakao.maps.LatLng(37.5589502, 126.8752775),
    new kakao.maps.LatLng(37.5591563, 126.8748767),
    new kakao.maps.LatLng(37.5595945, 126.874025),
    new kakao.maps.LatLng(37.5596946, 126.8738248),
    new kakao.maps.LatLng(37.5601596, 126.8728588),
    new kakao.maps.LatLng(37.5605276, 126.8720972),
    new kakao.maps.LatLng(37.5609333, 126.8712519),
    new kakao.maps.LatLng(37.5615358, 126.8699951),
    new kakao.maps.LatLng(37.5619632, 126.8691064),
    new kakao.maps.LatLng(37.5621959, 126.868634),
    new kakao.maps.LatLng(37.5627029, 126.8677403),
    new kakao.maps.LatLng(37.5629894, 126.8672261),
    new kakao.maps.LatLng(37.5632825, 126.8666958),
    new kakao.maps.LatLng(37.5637559, 126.8658888),
    new kakao.maps.LatLng(37.5640521, 126.8654083),
    new kakao.maps.LatLng(37.5644624, 126.8647347),
    new kakao.maps.LatLng(37.5647185, 126.8643124),
    new kakao.maps.LatLng(37.5649731, 126.8639165),
    new kakao.maps.LatLng(37.5650512, 126.8637912),
    new kakao.maps.LatLng(37.5652642, 126.8634888),
    new kakao.maps.LatLng(37.5653859, 126.8633098),
    new kakao.maps.LatLng(37.5654471, 126.8632313),
    new kakao.maps.LatLng(37.5655495, 126.8630904),
    new kakao.maps.LatLng(37.5657186, 126.8628754),
    new kakao.maps.LatLng(37.5660443, 126.8624873),
    new kakao.maps.LatLng(37.5663031, 126.8621474),
    new kakao.maps.LatLng(37.5663376, 126.8621034),
    new kakao.maps.LatLng(37.5664484, 126.8619718),
    new kakao.maps.LatLng(37.5667462, 126.861637),
    new kakao.maps.LatLng(37.5672618, 126.8610683),
    new kakao.maps.LatLng(37.5675217, 126.8607424),
    new kakao.maps.LatLng(37.5676648, 126.8605839),
    new kakao.maps.LatLng(37.5679501, 126.8602879),
    new kakao.maps.LatLng(37.5682635, 126.8599471),
    new kakao.maps.LatLng(37.5686039, 126.8595982),
    new kakao.maps.LatLng(37.5688681, 126.8592962),
    new kakao.maps.LatLng(37.5693278, 126.8588345),
    new kakao.maps.LatLng(37.5695699, 126.8585727),
    new kakao.maps.LatLng(37.5700741, 126.8580604),
    new kakao.maps.LatLng(37.5702804, 126.8578288),
    new kakao.maps.LatLng(37.5704464, 126.8576497),
    new kakao.maps.LatLng(37.5705987, 126.8574919),
    new kakao.maps.LatLng(37.5708578, 126.8572342),
    new kakao.maps.LatLng(37.5710034, 126.8571121),
    new kakao.maps.LatLng(37.5712288, 126.8569134),
    new kakao.maps.LatLng(37.5715422, 126.8566245),
    new kakao.maps.LatLng(37.5717665, 126.8564237),
    new kakao.maps.LatLng(37.5717904, 126.8536316)
];

        var gangseoPolygonA = new kakao.maps.Polygon({
            path: gangseoPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 구로구 다각형 생성(19대선)
        var guroPolygonAPath = [
    new kakao.maps.LatLng(37.4849988, 126.9031946),
    new kakao.maps.LatLng(37.4869351, 126.8981442),
    new kakao.maps.LatLng(37.4893387, 126.896124),
    new kakao.maps.LatLng(37.5033326, 126.8926737),
    new kakao.maps.LatLng(37.5050117, 126.8939767),
    new kakao.maps.LatLng(37.5103503, 126.8917119),
    new kakao.maps.LatLng(37.5132264, 126.8875197),
    new kakao.maps.LatLng(37.5138494, 126.8844331),
    new kakao.maps.LatLng(37.5164199, 126.881729),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5076346, 126.8222152),
    new kakao.maps.LatLng(37.5056852, 126.8225503),
    new kakao.maps.LatLng(37.5022364, 126.821611),
    new kakao.maps.LatLng(37.5006401, 126.8194028),
    new kakao.maps.LatLng(37.4993555, 126.8196714),
    new kakao.maps.LatLng(37.4977435, 126.8161301),
    new kakao.maps.LatLng(37.4982134, 126.8141214),
    new kakao.maps.LatLng(37.4964818, 126.8129811),
    new kakao.maps.LatLng(37.4931969, 126.814573),
    new kakao.maps.LatLng(37.4915531, 126.817904),
    new kakao.maps.LatLng(37.4899794, 126.822762),
    new kakao.maps.LatLng(37.4877351, 126.8235061),
    new kakao.maps.LatLng(37.4854809, 126.8192969),
    new kakao.maps.LatLng(37.4816405, 126.8199827),
    new kakao.maps.LatLng(37.4791625, 126.8189971),
    new kakao.maps.LatLng(37.4763621, 126.8152952),
    new kakao.maps.LatLng(37.4747205, 126.8146459),
    new kakao.maps.LatLng(37.4732881, 126.817076),
    new kakao.maps.LatLng(37.4741192, 126.8187239),
    new kakao.maps.LatLng(37.4763553, 126.8195989),
    new kakao.maps.LatLng(37.4759897, 126.8278719),
    new kakao.maps.LatLng(37.4776512, 126.8317475),
    new kakao.maps.LatLng(37.4767532, 126.8339281),
    new kakao.maps.LatLng(37.4744809, 126.8359294),
    new kakao.maps.LatLng(37.475392, 126.8383005),
    new kakao.maps.LatLng(37.4746479, 126.8410321),
    new kakao.maps.LatLng(37.4749715, 126.8427814),
    new kakao.maps.LatLng(37.4738124, 126.8453603),
    new kakao.maps.LatLng(37.480012, 126.8459113),
    new kakao.maps.LatLng(37.48191, 126.8470155),
    new kakao.maps.LatLng(37.481827, 126.8527424),
    new kakao.maps.LatLng(37.4854067, 126.8555066),
    new kakao.maps.LatLng(37.4860846, 126.8579708),
    new kakao.maps.LatLng(37.4899682, 126.8613841),
    new kakao.maps.LatLng(37.4915699, 126.8654623),
    new kakao.maps.LatLng(37.49426, 126.8668088),
    new kakao.maps.LatLng(37.4951278, 126.8683565),
    new kakao.maps.LatLng(37.4940956, 126.8697092),
    new kakao.maps.LatLng(37.4916613, 126.8693466),
    new kakao.maps.LatLng(37.4895402, 126.8704101),
    new kakao.maps.LatLng(37.4906414, 126.8723345),
    new kakao.maps.LatLng(37.4882584, 126.8730843),
    new kakao.maps.LatLng(37.4885708, 126.8767901),
    new kakao.maps.LatLng(37.4853671, 126.8745638),
    new kakao.maps.LatLng(37.4866723, 126.8784581),
    new kakao.maps.LatLng(37.4855632, 126.8813537),
    new kakao.maps.LatLng(37.4823496, 126.886155),
    new kakao.maps.LatLng(37.4804414, 126.8877295),
    new kakao.maps.LatLng(37.4793897, 126.8898815),
    new kakao.maps.LatLng(37.4783336, 126.8964731),
    new kakao.maps.LatLng(37.4789401, 126.8989434),
    new kakao.maps.LatLng(37.4811733, 126.900064),
    new kakao.maps.LatLng(37.4849988, 126.9031946)
];

        var guroPolygonA = new kakao.maps.Polygon({
            path: guroPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 금천구 다각형 생성(19대선)
        var geumcheonPolygonAPath = [ new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4783336, 126.8964731), new kakao.maps.LatLng(37.4793897, 126.8898815), new kakao.maps.LatLng(37.4804414, 126.8877295), new kakao.maps.LatLng(37.4823496, 126.886155), new kakao.maps.LatLng(37.4855632, 126.8813537), new kakao.maps.LatLng(37.4866723, 126.8784581), new kakao.maps.LatLng(37.4853671, 126.8745638), new kakao.maps.LatLng(37.4852298, 126.8718245), new kakao.maps.LatLng(37.4836436, 126.8728822), new kakao.maps.LatLng(37.4771039, 126.8759855), new kakao.maps.LatLng(37.4738278, 126.8780112), new kakao.maps.LatLng(37.4694169, 126.8815927), new kakao.maps.LatLng(37.4684591, 126.881631), new kakao.maps.LatLng(37.4665184, 126.8842988), new kakao.maps.LatLng(37.4643925, 126.8827454), new kakao.maps.LatLng(37.4627255, 126.884317), new kakao.maps.LatLng(37.4627551, 126.8861117), new kakao.maps.LatLng(37.4575101, 126.8858806), new kakao.maps.LatLng(37.4561777, 126.8863993), new kakao.maps.LatLng(37.4544844, 126.8892662), new kakao.maps.LatLng(37.4524961, 126.8903312), new kakao.maps.LatLng(37.451995, 126.8927328), new kakao.maps.LatLng(37.4527181, 126.8939824), new kakao.maps.LatLng(37.4484134, 126.8959156), new kakao.maps.LatLng(37.4466982, 126.8946497), new kakao.maps.LatLng(37.4454288, 126.8972601), new kakao.maps.LatLng(37.4369929, 126.9008673), new kakao.maps.LatLng(37.4358535, 126.902834), new kakao.maps.LatLng(37.4340675, 126.9029873), new kakao.maps.LatLng(37.4338646, 126.9094057), new kakao.maps.LatLng(37.4361712, 126.9113332), new kakao.maps.LatLng(37.4385546, 126.912294), new kakao.maps.LatLng(37.4400154, 126.9161336), new kakao.maps.LatLng(37.439825, 126.9192897), new kakao.maps.LatLng(37.444041, 126.9227625), new kakao.maps.LatLng(37.4457729, 126.923253), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4789401, 126.8989434) ];

        var geumcheonPolygonA = new kakao.maps.Polygon({
            path: geumcheonPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 영등포구 다각형 생성(19대선)
        var yeongdeungpoPolygonAPath = [ new kakao.maps.LatLng(37.5339056, 126.9446791), new kakao.maps.LatLng(37.5378354, 126.938558), new kakao.maps.LatLng(37.5405306, 126.9328982), new kakao.maps.LatLng(37.5413625, 126.9303377), new kakao.maps.LatLng(37.5390762, 126.9276653), new kakao.maps.LatLng(37.5397435, 126.9248228), new kakao.maps.LatLng(37.5414296, 126.922414), new kakao.maps.LatLng(37.5414165, 126.9048307), new kakao.maps.LatLng(37.5480079, 126.898943), new kakao.maps.LatLng(37.5494341, 126.8946416), new kakao.maps.LatLng(37.5523, 126.8881084), new kakao.maps.LatLng(37.5558475, 126.88131), new kakao.maps.LatLng(37.556224, 126.8804278), new kakao.maps.LatLng(37.555305, 126.879688), new kakao.maps.LatLng(37.5550643, 126.8794927), new kakao.maps.LatLng(37.554747, 126.879237), new kakao.maps.LatLng(37.5537026, 126.879224), new kakao.maps.LatLng(37.5531512, 126.8792171), new kakao.maps.LatLng(37.5532765, 126.8789601), new kakao.maps.LatLng(37.5533372, 126.878835), new kakao.maps.LatLng(37.5535815, 126.8782443), new kakao.maps.LatLng(37.553546, 126.8781144), new kakao.maps.LatLng(37.5535245, 126.8780551), new kakao.maps.LatLng(37.5534501, 126.8779539), new kakao.maps.LatLng(37.5532133, 126.8779456), new kakao.maps.LatLng(37.5531701, 126.8779519), new kakao.maps.LatLng(37.5529934, 126.8780067), new kakao.maps.LatLng(37.5527979, 126.8780142), new kakao.maps.LatLng(37.5525651, 126.8780226), new kakao.maps.LatLng(37.5523189, 126.8780313), new kakao.maps.LatLng(37.5519352, 126.8780413), new kakao.maps.LatLng(37.5515205, 126.8781985), new kakao.maps.LatLng(37.5511263, 126.8785301), new kakao.maps.LatLng(37.5507488, 126.8788459), new kakao.maps.LatLng(37.550412, 126.8791236), new kakao.maps.LatLng(37.5500282, 126.8794146), new kakao.maps.LatLng(37.5499377, 126.8794778), new kakao.maps.LatLng(37.5497628, 126.8796001), new kakao.maps.LatLng(37.5494053, 126.8798959), new kakao.maps.LatLng(37.5484626, 126.8804437), new kakao.maps.LatLng(37.5481962, 126.880664), new kakao.maps.LatLng(37.543321, 126.885088), new kakao.maps.LatLng(37.5397825, 126.8863138), new kakao.maps.LatLng(37.5351351, 126.8897886), new kakao.maps.LatLng(37.5319258, 126.8890681), new kakao.maps.LatLng(37.5301524, 126.8896671), new kakao.maps.LatLng(37.5301503, 126.8871006), new kakao.maps.LatLng(37.5287593, 126.8843314), new kakao.maps.LatLng(37.5259082, 126.8809399), new kakao.maps.LatLng(37.5252536, 126.878749), new kakao.maps.LatLng(37.5203627, 126.879464), new kakao.maps.LatLng(37.5187577, 126.8782517), new kakao.maps.LatLng(37.5178764, 126.8791653), new kakao.maps.LatLng(37.5164199, 126.881729), new kakao.maps.LatLng(37.5138494, 126.8844331), new kakao.maps.LatLng(37.5132264, 126.8875197), new kakao.maps.LatLng(37.5103503, 126.8917119), new kakao.maps.LatLng(37.5050117, 126.8939767), new kakao.maps.LatLng(37.5033326, 126.8926737), new kakao.maps.LatLng(37.4893387, 126.896124), new kakao.maps.LatLng(37.4869351, 126.8981442), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4938221, 126.9104722), new kakao.maps.LatLng(37.4964189, 126.9129118), new kakao.maps.LatLng(37.4975997, 126.9194077), new kakao.maps.LatLng(37.5125265, 126.9253894), new kakao.maps.LatLng(37.5127969, 126.9267906), new kakao.maps.LatLng(37.5155543, 126.9268588), new kakao.maps.LatLng(37.5155752, 126.9323857), new kakao.maps.LatLng(37.5160787, 126.9392792), new kakao.maps.LatLng(37.5175262, 126.9498866), new kakao.maps.LatLng(37.5270289, 126.94988), new kakao.maps.LatLng(37.5339056, 126.9446791) ];

        var yeongdeungpoPolygonA = new kakao.maps.Polygon({
            path: yeongdeungpoPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 동작구 다각형 생성(19대선)
        var dongjakPolygonAPath = [
    new kakao.maps.LatLng(37.5065363, 126.9804067),
    new kakao.maps.LatLng(37.5070128, 126.9752589),
    new kakao.maps.LatLng(37.5108166, 126.9649636),
    new kakao.maps.LatLng(37.5135025, 126.9612002),
    new kakao.maps.LatLng(37.516065, 126.9547037),
    new kakao.maps.LatLng(37.5175262, 126.9498866),
    new kakao.maps.LatLng(37.5160787, 126.9392792),
    new kakao.maps.LatLng(37.5155752, 126.9323857),
    new kakao.maps.LatLng(37.5155543, 126.9268588),
    new kakao.maps.LatLng(37.5127969, 126.9267906),
    new kakao.maps.LatLng(37.5125265, 126.9253894),
    new kakao.maps.LatLng(37.4975997, 126.9194077),
    new kakao.maps.LatLng(37.4964189, 126.9129118),
    new kakao.maps.LatLng(37.4938221, 126.9104722),
    new kakao.maps.LatLng(37.4850028, 126.9031989),
    new kakao.maps.LatLng(37.4849606, 126.9060977),
    new kakao.maps.LatLng(37.4865116, 126.911921),
    new kakao.maps.LatLng(37.4880073, 126.9135728),
    new kakao.maps.LatLng(37.489548, 126.9166515),
    new kakao.maps.LatLng(37.4902759, 126.9194523),
    new kakao.maps.LatLng(37.4899637, 126.924155),
    new kakao.maps.LatLng(37.4927983, 126.925577),
    new kakao.maps.LatLng(37.4949943, 126.9274611),
    new kakao.maps.LatLng(37.4932585, 126.9313461),
    new kakao.maps.LatLng(37.493189, 126.933849),
    new kakao.maps.LatLng(37.4919697, 126.9365336),
    new kakao.maps.LatLng(37.4929037, 126.9399265),
    new kakao.maps.LatLng(37.4921435, 126.9426218),
    new kakao.maps.LatLng(37.494039, 126.9471828),
    new kakao.maps.LatLng(37.4922055, 126.9516974),
    new kakao.maps.LatLng(37.4906416, 126.9537273),
    new kakao.maps.LatLng(37.4919773, 126.9574784),
    new kakao.maps.LatLng(37.4936159, 126.9589433),
    new kakao.maps.LatLng(37.4928741, 126.9613777),
    new kakao.maps.LatLng(37.4908252, 126.9607812),
    new kakao.maps.LatLng(37.4886278, 126.9619669),
    new kakao.maps.LatLng(37.4851775, 126.9619872),
    new kakao.maps.LatLng(37.4835752, 126.96107),
    new kakao.maps.LatLng(37.4798186, 126.9644275),
    new kakao.maps.LatLng(37.4789597, 126.9663255),
    new kakao.maps.LatLng(37.4753765, 126.9705226),
    new kakao.maps.LatLng(37.476201, 126.9742856),
    new kakao.maps.LatLng(37.4770573, 126.9816808),
    new kakao.maps.LatLng(37.4969936, 126.9829297),
    new kakao.maps.LatLng(37.499859, 126.9853872),
    new kakao.maps.LatLng(37.5026966, 126.9805363),
    new kakao.maps.LatLng(37.5065363, 126.9804067)
];

        var dongjakPolygonA = new kakao.maps.Polygon({
            path: dongjakPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 관악구 다각형 생성(19대선)
        var gwanakPolygonAPath = [ new kakao.maps.LatLng(37.4770573, 126.9816808), new kakao.maps.LatLng(37.476201, 126.9742856), new kakao.maps.LatLng(37.4753765, 126.9705226), new kakao.maps.LatLng(37.4789597, 126.9663255), new kakao.maps.LatLng(37.4798186, 126.9644275), new kakao.maps.LatLng(37.4835752, 126.96107), new kakao.maps.LatLng(37.4851775, 126.9619872), new kakao.maps.LatLng(37.4886278, 126.9619669), new kakao.maps.LatLng(37.4908252, 126.9607812), new kakao.maps.LatLng(37.4928741, 126.9613777), new kakao.maps.LatLng(37.4936159, 126.9589433), new kakao.maps.LatLng(37.4919773, 126.9574784), new kakao.maps.LatLng(37.4906416, 126.9537273), new kakao.maps.LatLng(37.4922055, 126.9516974), new kakao.maps.LatLng(37.494039, 126.9471828), new kakao.maps.LatLng(37.4921435, 126.9426218), new kakao.maps.LatLng(37.4929037, 126.9399265), new kakao.maps.LatLng(37.4919697, 126.9365336), new kakao.maps.LatLng(37.493189, 126.933849), new kakao.maps.LatLng(37.4932585, 126.9313461), new kakao.maps.LatLng(37.4949943, 126.9274611), new kakao.maps.LatLng(37.4927983, 126.925577), new kakao.maps.LatLng(37.4899637, 126.924155), new kakao.maps.LatLng(37.4902759, 126.9194523), new kakao.maps.LatLng(37.489548, 126.9166515), new kakao.maps.LatLng(37.4880073, 126.9135728), new kakao.maps.LatLng(37.4865116, 126.911921), new kakao.maps.LatLng(37.4849606, 126.9060977), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4811733, 126.900064), new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4483842, 126.9301661), new kakao.maps.LatLng(37.445463, 126.9305669), new kakao.maps.LatLng(37.4417395, 126.9366582), new kakao.maps.LatLng(37.4402029, 126.9378509), new kakao.maps.LatLng(37.4373807, 126.9377535), new kakao.maps.LatLng(37.4357034, 126.9402441), new kakao.maps.LatLng(37.4373944, 126.9414554), new kakao.maps.LatLng(37.4370754, 126.9451252), new kakao.maps.LatLng(37.4387126, 126.9483629), new kakao.maps.LatLng(37.4382501, 126.9492839), new kakao.maps.LatLng(37.4392385, 126.9523939), new kakao.maps.LatLng(37.4387351, 126.9551493), new kakao.maps.LatLng(37.4391229, 126.9589137), new kakao.maps.LatLng(37.4404007, 126.9600556), new kakao.maps.LatLng(37.4402806, 126.9629426), new kakao.maps.LatLng(37.4420397, 126.9646338), new kakao.maps.LatLng(37.4462673, 126.9642894), new kakao.maps.LatLng(37.4483804, 126.9676626), new kakao.maps.LatLng(37.4494526, 126.9705691), new kakao.maps.LatLng(37.4516571, 126.9718463), new kakao.maps.LatLng(37.454323, 126.9746584), new kakao.maps.LatLng(37.4556507, 126.978552), new kakao.maps.LatLng(37.4558313, 126.9824203), new kakao.maps.LatLng(37.4568271, 126.9828879), new kakao.maps.LatLng(37.4572124, 126.9866124), new kakao.maps.LatLng(37.4581534, 126.9886043), new kakao.maps.LatLng(37.4600297, 126.9875747), new kakao.maps.LatLng(37.4639986, 126.988344), new kakao.maps.LatLng(37.4676122, 126.9873023), new kakao.maps.LatLng(37.4698246, 126.9845159), new kakao.maps.LatLng(37.4737189, 126.9821725), new kakao.maps.LatLng(37.4770573, 126.9816808) ];

        var gwanakPolygonA = new kakao.maps.Polygon({
            path: gwanakPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        
        // 서초구 다각형 생성(19대선)
        var seochoPolygonAPath = [
    new kakao.maps.LatLng(37.4585341, 127.101167),
    new kakao.maps.LatLng(37.456285, 127.0990383),
    new kakao.maps.LatLng(37.4564649, 127.0952452),
    new kakao.maps.LatLng(37.458464, 127.0949315),
    new kakao.maps.LatLng(37.460993, 127.0956975),
    new kakao.maps.LatLng(37.4612481, 127.0933434),
    new kakao.maps.LatLng(37.4622744, 127.0920966),
    new kakao.maps.LatLng(37.4649182, 127.0920416),
    new kakao.maps.LatLng(37.4671484, 127.0904301),
    new kakao.maps.LatLng(37.4684889, 127.0881284),
    new kakao.maps.LatLng(37.4698449, 127.0875642),
    new kakao.maps.LatLng(37.4713002, 127.0850167),
    new kakao.maps.LatLng(37.4729288, 127.0841728),
    new kakao.maps.LatLng(37.4757966, 127.0844785),
    new kakao.maps.LatLng(37.4748544, 127.0779631),
    new kakao.maps.LatLng(37.4709943, 127.0704221),
    new kakao.maps.LatLng(37.4709576, 127.0685473),
    new kakao.maps.LatLng(37.4692945, 127.0650747),
    new kakao.maps.LatLng(37.469237, 127.059066),
    new kakao.maps.LatLng(37.4688702, 127.0553919),
    new kakao.maps.LatLng(37.4675849, 127.0509517),
    new kakao.maps.LatLng(37.4693652, 127.0510504),
    new kakao.maps.LatLng(37.4700597, 127.0486692),
    new kakao.maps.LatLng(37.4718104, 127.0509002),
    new kakao.maps.LatLng(37.4775193, 127.0450987),
    new kakao.maps.LatLng(37.4852405, 127.0416088),
    new kakao.maps.LatLng(37.4843691, 127.0340872),
    new kakao.maps.LatLng(37.5127991, 127.0205151),
    new kakao.maps.LatLng(37.521812, 127.0178222),
    new kakao.maps.LatLng(37.5248454, 127.0152308),
    new kakao.maps.LatLng(37.5260027, 127.0163404),
    new kakao.maps.LatLng(37.52974, 127.0126563),
    new kakao.maps.LatLng(37.5308993, 127.0137073),
    new kakao.maps.LatLng(37.5234361, 127.0064445),
    new kakao.maps.LatLng(37.5194968, 127.0007883),
    new kakao.maps.LatLng(37.5131024, 126.9906716),
    new kakao.maps.LatLng(37.5065431, 126.9855327),
    new kakao.maps.LatLng(37.5065363, 126.9804067),
    new kakao.maps.LatLng(37.5026966, 126.9805363),
    new kakao.maps.LatLng(37.499859, 126.9853872),
    new kakao.maps.LatLng(37.4969936, 126.9829297),
    new kakao.maps.LatLng(37.4770573, 126.9816808),
    new kakao.maps.LatLng(37.4737189, 126.9821725),
    new kakao.maps.LatLng(37.4698246, 126.9845159),
    new kakao.maps.LatLng(37.4676122, 126.9873023),
    new kakao.maps.LatLng(37.4639986, 126.988344),
    new kakao.maps.LatLng(37.4600297, 126.9875747),
    new kakao.maps.LatLng(37.4581534, 126.9886043),
    new kakao.maps.LatLng(37.4614959, 126.9933541),
    new kakao.maps.LatLng(37.4618734, 126.9967683),
    new kakao.maps.LatLng(37.464215, 126.9972632),
    new kakao.maps.LatLng(37.4666083, 126.9962307),
    new kakao.maps.LatLng(37.4671797, 126.9969853),
    new kakao.maps.LatLng(37.4671246, 127.0027346),
    new kakao.maps.LatLng(37.4657636, 127.0049273),
    new kakao.maps.LatLng(37.4640347, 127.0045148),
    new kakao.maps.LatLng(37.4578423, 127.0086622),
    new kakao.maps.LatLng(37.4554428, 127.010818),
    new kakao.maps.LatLng(37.4548611, 127.0145094),
    new kakao.maps.LatLng(37.4561351, 127.017545),
    new kakao.maps.LatLng(37.4556938, 127.0192823),
    new kakao.maps.LatLng(37.4572538, 127.022851),
    new kakao.maps.LatLng(37.4574817, 127.0252753),
    new kakao.maps.LatLng(37.4596417, 127.0265719),
    new kakao.maps.LatLng(37.4633413, 127.0296306),
    new kakao.maps.LatLng(37.4653746, 127.0295269),
    new kakao.maps.LatLng(37.4656262, 127.0311954),
    new kakao.maps.LatLng(37.4641547, 127.0346931),
    new kakao.maps.LatLng(37.4612371, 127.0337319),
    new kakao.maps.LatLng(37.4601754, 127.0349239),
    new kakao.maps.LatLng(37.4578668, 127.0350694),
    new kakao.maps.LatLng(37.455203, 127.0371709),
    new kakao.maps.LatLng(37.4526095, 127.0347723),
    new kakao.maps.LatLng(37.4514669, 127.0364748),
    new kakao.maps.LatLng(37.4494531, 127.037741),
    new kakao.maps.LatLng(37.4464509, 127.0372545),
    new kakao.maps.LatLng(37.4451803, 127.0382301),
    new kakao.maps.LatLng(37.4432667, 127.0374826),
    new kakao.maps.LatLng(37.4410155, 127.0352603),
    new kakao.maps.LatLng(37.4391373, 127.0356865),
    new kakao.maps.LatLng(37.4383913, 127.0371471),
    new kakao.maps.LatLng(37.4383412, 127.0401422),
    new kakao.maps.LatLng(37.4335915, 127.0463942),
    new kakao.maps.LatLng(37.4307906, 127.0473967),
    new kakao.maps.LatLng(37.4303374, 127.0493227),
    new kakao.maps.LatLng(37.4284561, 127.0520464),
    new kakao.maps.LatLng(37.4301499, 127.0578618),
    new kakao.maps.LatLng(37.4301216, 127.0608665),
    new kakao.maps.LatLng(37.4290228, 127.0656551),
    new kakao.maps.LatLng(37.4307189, 127.0683088),
    new kakao.maps.LatLng(37.4308177, 127.0712064),
    new kakao.maps.LatLng(37.4324169, 127.0705709),
    new kakao.maps.LatLng(37.4358635, 127.0714392),
    new kakao.maps.LatLng(37.4374234, 127.0738798),
    new kakao.maps.LatLng(37.4388568, 127.0720075),
    new kakao.maps.LatLng(37.4415239, 127.0716257),
    new kakao.maps.LatLng(37.442133, 127.0761442),
    new kakao.maps.LatLng(37.4410297, 127.0803008),
    new kakao.maps.LatLng(37.4413384, 127.0821566),
    new kakao.maps.LatLng(37.4439083, 127.083954),
    new kakao.maps.LatLng(37.4442491, 127.0865305),
    new kakao.maps.LatLng(37.4454138, 127.0882762),
    new kakao.maps.LatLng(37.4486278, 127.0883265),
    new kakao.maps.LatLng(37.4527827, 127.0909588),
    new kakao.maps.LatLng(37.4536339, 127.0927253),
    new kakao.maps.LatLng(37.4558885, 127.0935402),
    new kakao.maps.LatLng(37.4565198, 127.095769),
    new kakao.maps.LatLng(37.4562188, 127.0990955),
    new kakao.maps.LatLng(37.4585341, 127.101167)
];

        var seochoPolygonA = new kakao.maps.Polygon({
            path: seochoPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강남구 다각형 생성(19대선)
        var gangnamPolygonAPath = [
    new kakao.maps.LatLng(37.4665205, 127.1242057),
    new kakao.maps.LatLng(37.4817224, 127.1129675),
    new kakao.maps.LatLng(37.4902947, 127.1070066),
    new kakao.maps.LatLng(37.4927054, 127.1035119),
    new kakao.maps.LatLng(37.4966827, 127.0947945),
    new kakao.maps.LatLng(37.499673, 127.0841541),
    new kakao.maps.LatLng(37.5020674, 127.0769871),
    new kakao.maps.LatLng(37.5027396, 127.0698181),
    new kakao.maps.LatLng(37.5208765, 127.0675889),
    new kakao.maps.LatLng(37.5245822, 127.0674791),
    new kakao.maps.LatLng(37.5250565, 127.0654321),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5286757, 127.0551335),
    new kakao.maps.LatLng(37.5342726, 127.0460023),
    new kakao.maps.LatLng(37.5358577, 127.0396637),
    new kakao.maps.LatLng(37.5358238, 127.0211723),
    new kakao.maps.LatLng(37.5342595, 127.0177593),
    new kakao.maps.LatLng(37.5308993, 127.0137073),
    new kakao.maps.LatLng(37.52974, 127.0126563),
    new kakao.maps.LatLng(37.5260027, 127.0163404),
    new kakao.maps.LatLng(37.5248454, 127.0152308),
    new kakao.maps.LatLng(37.521812, 127.0178222),
    new kakao.maps.LatLng(37.5127991, 127.0205151),
    new kakao.maps.LatLng(37.4843691, 127.0340872),
    new kakao.maps.LatLng(37.4852405, 127.0416088),
    new kakao.maps.LatLng(37.4775193, 127.0450987),
    new kakao.maps.LatLng(37.4718104, 127.0509002),
    new kakao.maps.LatLng(37.4700597, 127.0486692),
    new kakao.maps.LatLng(37.4693652, 127.0510504),
    new kakao.maps.LatLng(37.4675849, 127.0509517),
    new kakao.maps.LatLng(37.4688702, 127.0553919),
    new kakao.maps.LatLng(37.469237, 127.059066),
    new kakao.maps.LatLng(37.4692945, 127.0650747),
    new kakao.maps.LatLng(37.4709576, 127.0685473),
    new kakao.maps.LatLng(37.4709943, 127.0704221),
    new kakao.maps.LatLng(37.4748544, 127.0779631),
    new kakao.maps.LatLng(37.4757966, 127.0844785),
    new kakao.maps.LatLng(37.4729288, 127.0841728),
    new kakao.maps.LatLng(37.4713002, 127.0850167),
    new kakao.maps.LatLng(37.4698449, 127.0875642),
    new kakao.maps.LatLng(37.4684889, 127.0881284),
    new kakao.maps.LatLng(37.4671484, 127.0904301),
    new kakao.maps.LatLng(37.4649182, 127.0920416),
    new kakao.maps.LatLng(37.4622744, 127.0920966),
    new kakao.maps.LatLng(37.4612481, 127.0933434),
    new kakao.maps.LatLng(37.460993, 127.0956975),
    new kakao.maps.LatLng(37.458464, 127.0949315),
    new kakao.maps.LatLng(37.4564649, 127.0952452),
    new kakao.maps.LatLng(37.456285, 127.0990383),
    new kakao.maps.LatLng(37.4585341, 127.101167),
    new kakao.maps.LatLng(37.4600566, 127.1039435),
    new kakao.maps.LatLng(37.4621594, 127.1043465),
    new kakao.maps.LatLng(37.4624345, 127.1064566),
    new kakao.maps.LatLng(37.4616446, 127.1118201),
    new kakao.maps.LatLng(37.4598893, 127.1134332),
    new kakao.maps.LatLng(37.458634, 127.116896),
    new kakao.maps.LatLng(37.4622006, 127.1174754),
    new kakao.maps.LatLng(37.464372, 127.12144),
    new kakao.maps.LatLng(37.4665205, 127.1242057)
];

        var gangnamPolygonA = new kakao.maps.Polygon({
            path: gangnamPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 송파구 다각형 생성(19대선)
        var songpaPolygonAPath = [
    new kakao.maps.LatLng(37.516886, 127.1450901),
    new kakao.maps.LatLng(37.517039, 127.1438278),
    new kakao.maps.LatLng(37.5279602, 127.1190926),
    new kakao.maps.LatLng(37.5296629, 127.1201352),
    new kakao.maps.LatLng(37.5386463, 127.1234424),
    new kakao.maps.LatLng(37.5410718, 127.1188769),
    new kakao.maps.LatLng(37.5429792, 127.1130478),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5414079, 127.1082818),
    new kakao.maps.LatLng(37.5270069, 127.090161),
    new kakao.maps.LatLng(37.524759, 127.0856328),
    new kakao.maps.LatLng(37.5229485, 127.0799746),
    new kakao.maps.LatLng(37.522514, 127.0769544),
    new kakao.maps.LatLng(37.523872, 127.0686631),
    new kakao.maps.LatLng(37.5268818, 127.0607945),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5250565, 127.0654321),
    new kakao.maps.LatLng(37.5245822, 127.0674791),
    new kakao.maps.LatLng(37.5208765, 127.0675889),
    new kakao.maps.LatLng(37.5027396, 127.0698181),
    new kakao.maps.LatLng(37.5020674, 127.0769871),
    new kakao.maps.LatLng(37.499673, 127.0841541),
    new kakao.maps.LatLng(37.4966827, 127.0947945),
    new kakao.maps.LatLng(37.4927054, 127.1035119),
    new kakao.maps.LatLng(37.4902947, 127.1070066),
    new kakao.maps.LatLng(37.4817224, 127.1129675),
    new kakao.maps.LatLng(37.4665205, 127.1242057),
    new kakao.maps.LatLng(37.4684191, 127.1270342),
    new kakao.maps.LatLng(37.4677511, 127.1301405),
    new kakao.maps.LatLng(37.4683941, 127.1327994),
    new kakao.maps.LatLng(37.4697986, 127.1319826),
    new kakao.maps.LatLng(37.4715382, 127.1328449),
    new kakao.maps.LatLng(37.4746269, 127.1328558),
    new kakao.maps.LatLng(37.4742406, 127.1354681),
    new kakao.maps.LatLng(37.4739308, 127.1435264),
    new kakao.maps.LatLng(37.4773315, 127.1443703),
    new kakao.maps.LatLng(37.4772222, 127.1471451),
    new kakao.maps.LatLng(37.4815898, 127.1474588),
    new kakao.maps.LatLng(37.4840436, 127.1486828),
    new kakao.maps.LatLng(37.4862358, 127.1521778),
    new kakao.maps.LatLng(37.489672, 127.1585233),
    new kakao.maps.LatLng(37.492048, 127.1584792),
    new kakao.maps.LatLng(37.4943902, 127.1600312),
    new kakao.maps.LatLng(37.4968237, 127.1597796),
    new kakao.maps.LatLng(37.4995369, 127.1613552),
    new kakao.maps.LatLng(37.5031794, 127.1577291),
    new kakao.maps.LatLng(37.5018946, 127.1565548),
    new kakao.maps.LatLng(37.5029854, 127.1521336),
    new kakao.maps.LatLng(37.5046783, 127.1502631),
    new kakao.maps.LatLng(37.5032338, 127.1477163),
    new kakao.maps.LatLng(37.5054583, 127.1411493),
    new kakao.maps.LatLng(37.5067087, 127.1415163),
    new kakao.maps.LatLng(37.5085171, 127.139952),
    new kakao.maps.LatLng(37.5123608, 127.1413929),
    new kakao.maps.LatLng(37.5126573, 127.1435398),
    new kakao.maps.LatLng(37.5156419, 127.1421313),
    new kakao.maps.LatLng(37.5155915, 127.1446078),
    new kakao.maps.LatLng(37.516886, 127.1450901)
];

        var songpaPolygonA = new kakao.maps.Polygon({
            path: songpaPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강동구 다각형 생성(19대선)
        var gangdongPolygonAPath =[
    new kakao.maps.LatLng(37.516886, 127.1450901),
    new kakao.maps.LatLng(37.5196245, 127.1447856),
    new kakao.maps.LatLng(37.5219397, 127.1457414),
    new kakao.maps.LatLng(37.5221448, 127.1478181),
    new kakao.maps.LatLng(37.5263728, 127.1504017),
    new kakao.maps.LatLng(37.5285295, 127.1526867),
    new kakao.maps.LatLng(37.5319199, 127.1539334),
    new kakao.maps.LatLng(37.533683, 127.1536063),
    new kakao.maps.LatLng(37.5392702, 127.1576512),
    new kakao.maps.LatLng(37.5411651, 127.1598933),
    new kakao.maps.LatLng(37.5449999, 127.1631595),
    new kakao.maps.LatLng(37.5442561, 127.1666417),
    new kakao.maps.LatLng(37.5455346, 127.1721068),
    new kakao.maps.LatLng(37.5452104, 127.1757181),
    new kakao.maps.LatLng(37.5466816, 127.1793088),
    new kakao.maps.LatLng(37.5463443, 127.1828251),
    new kakao.maps.LatLng(37.5518204, 127.1829114),
    new kakao.maps.LatLng(37.5528619, 127.1813807),
    new kakao.maps.LatLng(37.5609928, 127.1819994),
    new kakao.maps.LatLng(37.5654958, 127.179585),
    new kakao.maps.LatLng(37.5689182, 127.1792158),
    new kakao.maps.LatLng(37.5722139, 127.1777375),
    new kakao.maps.LatLng(37.5740993, 127.17614),
    new kakao.maps.LatLng(37.5783633, 127.1754421),
    new kakao.maps.LatLng(37.5792655, 127.1768832),
    new kakao.maps.LatLng(37.5812008, 127.1771547),
    new kakao.maps.LatLng(37.5797349, 127.1738711),
    new kakao.maps.LatLng(37.5786946, 127.1671595),
    new kakao.maps.LatLng(37.5764649, 127.1629721),
    new kakao.maps.LatLng(37.5704037, 127.1536011),
    new kakao.maps.LatLng(37.5681865, 127.1493618),
    new kakao.maps.LatLng(37.5682007, 127.138063),
    new kakao.maps.LatLng(37.567884, 127.135692),
    new kakao.maps.LatLng(37.565944, 127.1290179),
    new kakao.maps.LatLng(37.5633331, 127.1234369),
    new kakao.maps.LatLng(37.5592439, 127.1176932),
    new kakao.maps.LatLng(37.5568724, 127.1153231),
    new kakao.maps.LatLng(37.5543662, 127.1143095),
    new kakao.maps.LatLng(37.5504987, 127.1115571),
    new kakao.maps.LatLng(37.5469267, 127.1114708),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5429792, 127.1130478),
    new kakao.maps.LatLng(37.5410718, 127.1188769),
    new kakao.maps.LatLng(37.5386463, 127.1234424),
    new kakao.maps.LatLng(37.5296629, 127.1201352),
    new kakao.maps.LatLng(37.5279602, 127.1190926),
    new kakao.maps.LatLng(37.517039, 127.1438278),
    new kakao.maps.LatLng(37.516886, 127.1450901)
];

        var gangdongPolygonA = new kakao.maps.Polygon({
            path: gangdongPolygonAPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });


        // (2022대선) 용산구 다각형 생성
        var yongsanPolygonBPath = [
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.54413326436179, 127.00898460651953),
            new kakao.maps.LatLng(37.539639030116945, 127.00959054834321),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.52290225898471, 127.00614038053493),
            new kakao.maps.LatLng(37.51309192794448, 126.99070240960813),
            new kakao.maps.LatLng(37.50654651085339, 126.98553683648308),
            new kakao.maps.LatLng(37.50702053393398, 126.97524914998174),
            new kakao.maps.LatLng(37.51751820477105, 126.94988506562748),
            new kakao.maps.LatLng(37.52702918583156, 126.94987870367682),
            new kakao.maps.LatLng(37.534519656862926, 126.94481851935942),
            new kakao.maps.LatLng(37.537500243531994, 126.95335659960566),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.5541513366375, 126.9657135934734),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994)
        ];

        var yongsanPolygonB = new kakao.maps.Polygon({
            path: yongsanPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: 'E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        var dongdaemunPolygonBPath = [
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496),
            new kakao.maps.LatLng(37.60107201319839, 127.07287376670605),
            new kakao.maps.LatLng(37.59724304056685, 127.06949105186925),
            new kakao.maps.LatLng(37.58953367466315, 127.07030363208528),
            new kakao.maps.LatLng(37.58651213184981, 127.07264218709383),
            new kakao.maps.LatLng(37.5849555116177, 127.07216063016078),
            new kakao.maps.LatLng(37.58026781100598, 127.07619547037923),
            new kakao.maps.LatLng(37.571869232268774, 127.0782018408153),
            new kakao.maps.LatLng(37.559961773835425, 127.07239004251258),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.572878529071055, 127.04263554582458),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.57838361223621, 127.0232348231103),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5956815721534, 127.04062845365279),
            new kakao.maps.LatLng(37.5969637344377, 127.04302522879048),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496)
        ];

        var dongdaemunPolygonB = new kakao.maps.Polygon({
            path: dongdaemunPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성동구 다각형 생성(22대선)
        var seungdongPolygonBPath = [
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.5594131360664, 127.07373408220053),
            new kakao.maps.LatLng(37.52832388381049, 127.05621773388143),
            new kakao.maps.LatLng(37.53423885672233, 127.04604398310076),
            new kakao.maps.LatLng(37.53582328355087, 127.03979942567628),
            new kakao.maps.LatLng(37.53581367627865, 127.0211714455564),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53938672166098, 127.00993448922989),
            new kakao.maps.LatLng(37.54157804358092, 127.00879872996808),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706)
        ];

        var seungdongPolygonB = new kakao.maps.Polygon({
            path: seungdongPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 서대문구 다각형 생성(22대선)
        var seodaemunPolygonBPath = [
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003),
            new kakao.maps.LatLng(37.5992407011344, 126.95499403097206),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.5575156365052, 126.95991288916548),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.57599550420081, 126.902091747923),
            new kakao.maps.LatLng(37.587223103650295, 126.91284666446226),
            new kakao.maps.LatLng(37.58541570520177, 126.91531241017965),
            new kakao.maps.LatLng(37.585870567159255, 126.91638068573187),
            new kakao.maps.LatLng(37.583095195853055, 126.9159399866114),
            new kakao.maps.LatLng(37.583459593417196, 126.92175886498167),
            new kakao.maps.LatLng(37.587104600730505, 126.92388813813815),
            new kakao.maps.LatLng(37.588386594820484, 126.92800815682232),
            new kakao.maps.LatLng(37.59157595859555, 126.92776504133688),
            new kakao.maps.LatLng(37.59455434247408, 126.93027139545339),
            new kakao.maps.LatLng(37.59869748704149, 126.94088480070904),
            new kakao.maps.LatLng(37.60065830191363, 126.9414041615336),
            new kakao.maps.LatLng(37.60305781086164, 126.93995273804141),
            new kakao.maps.LatLng(37.610598531321436, 126.95037536795142),
            new kakao.maps.LatLng(37.6083605525023, 126.95056259057313),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003)
        ];

        var seodaemunPolygonB = new kakao.maps.Polygon({
            path: seodaemunPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 종로구 다각형 생성(22대선)
        var jongnoPolygonBPath = [
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046),
            new kakao.maps.LatLng(37.632194205253654, 126.97609588529602),
            new kakao.maps.LatLng(37.629026103322374, 126.97496405167149),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.60401657024552, 126.98665951539246),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.5788668917658, 127.02140099081309),
            new kakao.maps.LatLng(37.578034045208426, 127.02313962015988),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.5681357695346, 126.99014772014593),
            new kakao.maps.LatLng(37.569315246023024, 126.9732046364419),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.59875701675023, 126.95306020161668),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.60912809443569, 126.95032198271032),
            new kakao.maps.LatLng(37.615539700280216, 126.95072546923387),
            new kakao.maps.LatLng(37.62433621196653, 126.94900237336302),
            new kakao.maps.LatLng(37.62642708817027, 126.95037844036497),
            new kakao.maps.LatLng(37.629590994617104, 126.95881385457929),
            new kakao.maps.LatLng(37.629794440379136, 126.96376660599225),
            new kakao.maps.LatLng(37.632373740990175, 126.97302793692637),
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046)
        ];

        var jongnoPolygonB = new kakao.maps.Polygon({
            path: jongnoPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중구 다각형 생성(22대선)
        var jungPolygonBPath = [
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55487749311664, 126.97240854546743),
            new kakao.maps.LatLng(37.5548766923893, 126.9691718124876),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.55498984534305, 126.96173858545431),
            new kakao.maps.LatLng(37.55695455613004, 126.96343068837372),
            new kakao.maps.LatLng(37.5590262922649, 126.9616731414449),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.569485309984174, 126.97637402412326),
            new kakao.maps.LatLng(37.56810323716611, 126.98905202099309),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.572022763755164, 127.0223363152772),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56973041414113, 127.0234585247501),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894)
        ];

        var jungPolygonB = new kakao.maps.Polygon({
            path: jungPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 광진구 다각형 생성(22대선)
        var gwangjinPolygonBPath = [
    new kakao.maps.LatLng(37.5568724, 127.1153231),
    new kakao.maps.LatLng(37.5585233, 127.113965),
    new kakao.maps.LatLng(37.5590006, 127.112297),
    new kakao.maps.LatLng(37.5585538, 127.1095286),
    new kakao.maps.LatLng(37.5564601, 127.1063932),
    new kakao.maps.LatLng(37.5595269, 127.1019134),
    new kakao.maps.LatLng(37.5616054, 127.1012509),
    new kakao.maps.LatLng(37.5643129, 127.1023143),
    new kakao.maps.LatLng(37.5701103, 127.1035059),
    new kakao.maps.LatLng(37.5714514, 127.104295),
    new kakao.maps.LatLng(37.5724694, 127.1017021),
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.5679178, 127.0768757),
    new kakao.maps.LatLng(37.5645904, 127.0740989),
    new kakao.maps.LatLng(37.5599603, 127.0723852),
    new kakao.maps.LatLng(37.559414, 127.0737358),
    new kakao.maps.LatLng(37.5393084, 127.0623676),
    new kakao.maps.LatLng(37.539291, 127.0623585),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5268818, 127.0607945),
    new kakao.maps.LatLng(37.523872, 127.0686631),
    new kakao.maps.LatLng(37.522514, 127.0769544),
    new kakao.maps.LatLng(37.5229485, 127.0799746),
    new kakao.maps.LatLng(37.524759, 127.0856328),
    new kakao.maps.LatLng(37.5270069, 127.090161),
    new kakao.maps.LatLng(37.5414079, 127.1082818),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5469267, 127.1114708),
    new kakao.maps.LatLng(37.5504987, 127.1115571),
    new kakao.maps.LatLng(37.5543662, 127.1143095),
    new kakao.maps.LatLng(37.5568724, 127.1153231)
];  
        var gwangjinPolygonB = new kakao.maps.Polygon({
            path: gwangjinPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중랑구 다각형 생성(22대선)
        var jungnangPolygonBPath = [
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.5760708, 127.1011435),
    new kakao.maps.LatLng(37.578907, 127.1030254),
    new kakao.maps.LatLng(37.5805343, 127.103429),
    new kakao.maps.LatLng(37.5833044, 127.109002),
    new kakao.maps.LatLng(37.5891647, 127.1106433),
    new kakao.maps.LatLng(37.5932091, 127.1131972),
    new kakao.maps.LatLng(37.5940164, 127.1166645),
    new kakao.maps.LatLng(37.5954971, 127.1168775),
    new kakao.maps.LatLng(37.599521, 127.1140639),
    new kakao.maps.LatLng(37.6021085, 127.1157227),
    new kakao.maps.LatLng(37.6046024, 127.118047),
    new kakao.maps.LatLng(37.607613, 127.1184769),
    new kakao.maps.LatLng(37.6088335, 127.1166833),
    new kakao.maps.LatLng(37.6118276, 127.1174901),
    new kakao.maps.LatLng(37.6160155, 127.1166717),
    new kakao.maps.LatLng(37.6178884, 127.1171467),
    new kakao.maps.LatLng(37.6195377, 127.115021),
    new kakao.maps.LatLng(37.6210546, 127.110519),
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6153366, 127.0701774),
    new kakao.maps.LatLng(37.6153196, 127.0702079),
    new kakao.maps.LatLng(37.6135142, 127.0717529),
    new kakao.maps.LatLng(37.6070224, 127.0711169),
    new kakao.maps.LatLng(37.6046424, 127.0715334),
    new kakao.maps.LatLng(37.6013304, 127.0728729),
    new kakao.maps.LatLng(37.600246, 127.0724977),
    new kakao.maps.LatLng(37.5972431, 127.069494),
    new kakao.maps.LatLng(37.5951242, 127.0694344),
    new kakao.maps.LatLng(37.5919078, 127.0707184),
    new kakao.maps.LatLng(37.5899586, 127.070228),
    new kakao.maps.LatLng(37.5865116, 127.0726438),
    new kakao.maps.LatLng(37.5849569, 127.0721613),
    new kakao.maps.LatLng(37.5793357, 127.076458),
    new kakao.maps.LatLng(37.5729206, 127.0772314),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5737318, 127.1008637)
];

        var jungnangPolygonB = new kakao.maps.Polygon({
            path: jungnangPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성북구 다각형 생성(22대선)
        var seongbukPolygonBPath = [
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235),
            new kakao.maps.LatLng(37.631446839436855, 126.99372381657889),
            new kakao.maps.LatLng(37.626192451322005, 126.99927047335905),
            new kakao.maps.LatLng(37.62382095469671, 127.00488450145781),
            new kakao.maps.LatLng(37.624026217174986, 127.00788862747375),
            new kakao.maps.LatLng(37.6205124078061, 127.00724034082933),
            new kakao.maps.LatLng(37.61679651952433, 127.01014412786792),
            new kakao.maps.LatLng(37.61472018601129, 127.01451127202589),
            new kakao.maps.LatLng(37.614629670135216, 127.01757841621624),
            new kakao.maps.LatLng(37.61137091590441, 127.02219857751122),
            new kakao.maps.LatLng(37.612692696824915, 127.02642583551054),
            new kakao.maps.LatLng(37.612367438936786, 127.03018593770908),
            new kakao.maps.LatLng(37.60896889076571, 127.0302525167858),
            new kakao.maps.LatLng(37.61279787695882, 127.03730791358603),
            new kakao.maps.LatLng(37.62426467261789, 127.04973339977498),
            new kakao.maps.LatLng(37.61449950127667, 127.06174181124696),
            new kakao.maps.LatLng(37.61561580859776, 127.06985247014711),
            new kakao.maps.LatLng(37.61351359068103, 127.07170798866412),
            new kakao.maps.LatLng(37.60762512162974, 127.07105453180604),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.59644879095525, 127.04184728392097),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.57782865303167, 127.02296295333255),
            new kakao.maps.LatLng(37.57889204835333, 127.02179043639809),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.60451393107786, 126.98678626394351),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.62980449548538, 126.97468284124939),
            new kakao.maps.LatLng(37.633657663246694, 126.97740053878216),
            new kakao.maps.LatLng(37.63476479485093, 126.98154674721893),
            new kakao.maps.LatLng(37.63780700422825, 126.9849494717052),
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235)
        ];

        var seongbukPolygonB = new kakao.maps.Polygon({
            path: seongbukPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강북구 다각형 생성(22대선)
        var gangbukPolygonBPath = [
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6850889, 127.0045265),
    new kakao.maps.LatLng(37.6834224, 126.9973582),
    new kakao.maps.LatLng(37.678828, 126.9929755),
    new kakao.maps.LatLng(37.6757199, 126.9931995),
    new kakao.maps.LatLng(37.672422, 126.9942076),
    new kakao.maps.LatLng(37.6678322, 126.993576),
    new kakao.maps.LatLng(37.6670301, 126.9941291),
    new kakao.maps.LatLng(37.6652317, 126.9922245),
    new kakao.maps.LatLng(37.6643912, 126.9882682),
    new kakao.maps.LatLng(37.6606003, 126.9872768),
    new kakao.maps.LatLng(37.6589432, 126.9860205),
    new kakao.maps.LatLng(37.6570035, 126.9830101),
    new kakao.maps.LatLng(37.6560387, 126.9796581),
    new kakao.maps.LatLng(37.6548152, 126.9799441),
    new kakao.maps.LatLng(37.6505404, 126.9824953),
    new kakao.maps.LatLng(37.64961, 126.9839369),
    new kakao.maps.LatLng(37.6457101, 126.9850955),
    new kakao.maps.LatLng(37.6436716, 126.9832554),
    new kakao.maps.LatLng(37.6400446, 126.9856762),
    new kakao.maps.LatLng(37.6363484, 126.9841726),
    new kakao.maps.LatLng(37.6340757, 126.9894095),
    new kakao.maps.LatLng(37.6302496, 126.9953935),
    new kakao.maps.LatLng(37.6262023, 126.999273),
    new kakao.maps.LatLng(37.625951, 127.0000402),
    new kakao.maps.LatLng(37.6259335, 127.0000628),
    new kakao.maps.LatLng(37.6242258, 127.0038971),
    new kakao.maps.LatLng(37.6240272, 127.0078883),
    new kakao.maps.LatLng(37.6208272, 127.0072158),
    new kakao.maps.LatLng(37.618622, 127.0085),
    new kakao.maps.LatLng(37.6162859, 127.0109519),
    new kakao.maps.LatLng(37.6146854, 127.0144744),
    new kakao.maps.LatLng(37.6146161, 127.0175368),
    new kakao.maps.LatLng(37.6113717, 127.0221965),
    new kakao.maps.LatLng(37.6126938, 127.0264334),
    new kakao.maps.LatLng(37.6123662, 127.0301844),
    new kakao.maps.LatLng(37.6089762, 127.0302524),
    new kakao.maps.LatLng(37.6129618, 127.0375131),
    new kakao.maps.LatLng(37.6157606, 127.0399847),
    new kakao.maps.LatLng(37.6186436, 127.0439485),
    new kakao.maps.LatLng(37.6226012, 127.0468685),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6843696, 127.0086619)
];

        var gangbukPolygonB = new kakao.maps.Polygon({
            path: gangbukPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 도봉구 다각형 생성(22대선)
        var dobongPolygonBPath = [
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6879759, 127.0498208),
    new kakao.maps.LatLng(37.6908702, 127.0499658),
    new kakao.maps.LatLng(37.6940664, 127.0486327),
    new kakao.maps.LatLng(37.6923802, 127.0456492),
    new kakao.maps.LatLng(37.693687, 127.043083),
    new kakao.maps.LatLng(37.6952354, 127.0430909),
    new kakao.maps.LatLng(37.6952919, 127.0411383),
    new kakao.maps.LatLng(37.6926381, 127.0368093),
    new kakao.maps.LatLng(37.6918448, 127.0324625),
    new kakao.maps.LatLng(37.6930733, 127.0310969),
    new kakao.maps.LatLng(37.6962653, 127.0297701),
    new kakao.maps.LatLng(37.6992843, 127.0293125),
    new kakao.maps.LatLng(37.7009462, 127.02771),
    new kakao.maps.LatLng(37.6995947, 127.0253836),
    new kakao.maps.LatLng(37.6997207, 127.0221482),
    new kakao.maps.LatLng(37.7010174, 127.0198271),
    new kakao.maps.LatLng(37.7014553, 127.0154151),
    new kakao.maps.LatLng(37.6988007, 127.0138784),
    new kakao.maps.LatLng(37.6973775, 127.0121243),
    new kakao.maps.LatLng(37.6966991, 127.0096662),
    new kakao.maps.LatLng(37.6933154, 127.0097568),
    new kakao.maps.LatLng(37.6915772, 127.007678),
    new kakao.maps.LatLng(37.6900533, 127.0083369),
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6858137, 127.0518033)
];

        var dobongPolygonB = new kakao.maps.Polygon({
            path: dobongPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 노원구 다각형 생성(22대선)
        var nowonPolygonBPath = [
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6216472, 127.1040704),
    new kakao.maps.LatLng(37.6275838, 127.1059087),
    new kakao.maps.LatLng(37.6293016, 127.1088847),
    new kakao.maps.LatLng(37.6315033, 127.1116324),
    new kakao.maps.LatLng(37.6326429, 127.1122035),
    new kakao.maps.LatLng(37.6364891, 127.1124833),
    new kakao.maps.LatLng(37.6391262, 127.1105493),
    new kakao.maps.LatLng(37.6398412, 127.1120504),
    new kakao.maps.LatLng(37.6425246, 127.1108099),
    new kakao.maps.LatLng(37.6426948, 127.1093228),
    new kakao.maps.LatLng(37.6451721, 127.1067673),
    new kakao.maps.LatLng(37.6452258, 127.1028086),
    new kakao.maps.LatLng(37.6439649, 127.0975589),
    new kakao.maps.LatLng(37.6445705, 127.09457),
    new kakao.maps.LatLng(37.6496973, 127.0924745),
    new kakao.maps.LatLng(37.6524386, 127.0940495),
    new kakao.maps.LatLng(37.6537758, 127.0930673),
    new kakao.maps.LatLng(37.6593346, 127.0912069),
    new kakao.maps.LatLng(37.6632988, 127.0941422),
    new kakao.maps.LatLng(37.6675788, 127.095017),
    new kakao.maps.LatLng(37.6687685, 127.0962455),
    new kakao.maps.LatLng(37.6727011, 127.0957715),
    new kakao.maps.LatLng(37.673564, 127.0946559),
    new kakao.maps.LatLng(37.6767064, 127.0938558),
    new kakao.maps.LatLng(37.6786397, 127.0919859),
    new kakao.maps.LatLng(37.6814411, 127.0929524),
    new kakao.maps.LatLng(37.6855375, 127.0964162),
    new kakao.maps.LatLng(37.689071, 127.095996),
    new kakao.maps.LatLng(37.6899664, 127.0930367),
    new kakao.maps.LatLng(37.6895704, 127.0905519),
    new kakao.maps.LatLng(37.6899122, 127.0865306),
    new kakao.maps.LatLng(37.6917823, 127.083905),
    new kakao.maps.LatLng(37.694269, 127.0838433),
    new kakao.maps.LatLng(37.6961376, 127.0811047),
    new kakao.maps.LatLng(37.6959864, 127.0781963),
    new kakao.maps.LatLng(37.6951465, 127.0748951),
    new kakao.maps.LatLng(37.6937786, 127.0727908),
    new kakao.maps.LatLng(37.6939832, 127.0686396),
    new kakao.maps.LatLng(37.6949371, 127.0634232),
    new kakao.maps.LatLng(37.6930035, 127.0624128),
    new kakao.maps.LatLng(37.6902838, 127.0597139),
    new kakao.maps.LatLng(37.6892048, 127.0551791),
    new kakao.maps.LatLng(37.6870667, 127.0518042),
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6197959, 127.0544081),
    new kakao.maps.LatLng(37.6174813, 127.0574206),
    new kakao.maps.LatLng(37.6142587, 127.0632852),
    new kakao.maps.LatLng(37.6157243, 127.0697122),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.6203794, 127.105654)
];

        var nowonPolygonB = new kakao.maps.Polygon({
            path: nowonPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 은평구 다각형 생성(22대선)
        var eunpyeongPolygonBPath = [
    new kakao.maps.LatLng(37.6295893, 126.9588137),
    new kakao.maps.LatLng(37.62973, 126.9597977),
    new kakao.maps.LatLng(37.6332338, 126.9634013),
    new kakao.maps.LatLng(37.6357828, 126.9626334),
    new kakao.maps.LatLng(37.6421387, 126.9593275),
    new kakao.maps.LatLng(37.6467834, 126.959027),
    new kakao.maps.LatLng(37.6480477, 126.9578392),
    new kakao.maps.LatLng(37.6528372, 126.9571078),
    new kakao.maps.LatLng(37.6546009, 126.9543453),
    new kakao.maps.LatLng(37.6549496, 126.9513757),
    new kakao.maps.LatLng(37.6571298, 126.9478961),
    new kakao.maps.LatLng(37.6592154, 126.9475649),
    new kakao.maps.LatLng(37.6577222, 126.9421),
    new kakao.maps.LatLng(37.6566359, 126.9401282),
    new kakao.maps.LatLng(37.6523011, 126.9371587),
    new kakao.maps.LatLng(37.6511999, 126.9357024),
    new kakao.maps.LatLng(37.6500481, 126.9296991),
    new kakao.maps.LatLng(37.6461063, 126.9241229),
    new kakao.maps.LatLng(37.6447557, 126.9137208),
    new kakao.maps.LatLng(37.6476455, 126.9095352),
    new kakao.maps.LatLng(37.6486884, 126.905964),
    new kakao.maps.LatLng(37.6462898, 126.9077049),
    new kakao.maps.LatLng(37.6442586, 126.9122604),
    new kakao.maps.LatLng(37.6385095, 126.9100918),
    new kakao.maps.LatLng(37.6353165, 126.9108542),
    new kakao.maps.LatLng(37.633398, 126.9070962),
    new kakao.maps.LatLng(37.6308672, 126.9072938),
    new kakao.maps.LatLng(37.6293276, 126.9087697),
    new kakao.maps.LatLng(37.6262657, 126.9086108),
    new kakao.maps.LatLng(37.6244956, 126.9066268),
    new kakao.maps.LatLng(37.6219415, 126.9071175),
    new kakao.maps.LatLng(37.6207039, 126.9056125),
    new kakao.maps.LatLng(37.6190745, 126.9052311),
    new kakao.maps.LatLng(37.6188394, 126.903361),
    new kakao.maps.LatLng(37.6157535, 126.9018223),
    new kakao.maps.LatLng(37.6140692, 126.9017342),
    new kakao.maps.LatLng(37.6111913, 126.9003043),
    new kakao.maps.LatLng(37.6037417, 126.9021083),
    new kakao.maps.LatLng(37.6020402, 126.8999819),
    new kakao.maps.LatLng(37.5993665, 126.9013224),
    new kakao.maps.LatLng(37.5973371, 126.9010115),
    new kakao.maps.LatLng(37.5951135, 126.9018381),
    new kakao.maps.LatLng(37.5926784, 126.8989613),
    new kakao.maps.LatLng(37.589938, 126.8997501),
    new kakao.maps.LatLng(37.5885666, 126.896859),
    new kakao.maps.LatLng(37.5890755, 126.8932905),
    new kakao.maps.LatLng(37.5885221, 126.8922355),
    new kakao.maps.LatLng(37.5885328, 126.8871589),
    new kakao.maps.LatLng(37.5895376, 126.8858088),
    new kakao.maps.LatLng(37.593639, 126.885004),
    new kakao.maps.LatLng(37.5907926, 126.8820561),
    new kakao.maps.LatLng(37.5907588, 126.882095),
    new kakao.maps.LatLng(37.588347, 126.8845533),
    new kakao.maps.LatLng(37.5876412, 126.8852568),
    new kakao.maps.LatLng(37.5870924, 126.8858291),
    new kakao.maps.LatLng(37.5860266, 126.8871243),
    new kakao.maps.LatLng(37.5858059, 126.8874045),
    new kakao.maps.LatLng(37.5815606, 126.8937787),
    new kakao.maps.LatLng(37.5794888, 126.8969354),
    new kakao.maps.LatLng(37.5782229, 126.898808),
    new kakao.maps.LatLng(37.5765458, 126.901833),
    new kakao.maps.LatLng(37.5787907, 126.9044431),
    new kakao.maps.LatLng(37.5803263, 126.9060741),
    new kakao.maps.LatLng(37.58547, 126.9115429),
    new kakao.maps.LatLng(37.5865298, 126.9124768),
    new kakao.maps.LatLng(37.5868917, 126.9126854),
    new kakao.maps.LatLng(37.5870633, 126.9127725),
    new kakao.maps.LatLng(37.5862014, 126.9151912),
    new kakao.maps.LatLng(37.5860447, 126.9155519),
    new kakao.maps.LatLng(37.5853667, 126.9160692),
    new kakao.maps.LatLng(37.5853601, 126.9160646),
    new kakao.maps.LatLng(37.5843543, 126.9156798),
    new kakao.maps.LatLng(37.5837821, 126.9157485),
    new kakao.maps.LatLng(37.5831718, 126.9164206),
    new kakao.maps.LatLng(37.58325, 126.9178162),
    new kakao.maps.LatLng(37.5829392, 126.920859),
    new kakao.maps.LatLng(37.5838591, 126.9218276),
    new kakao.maps.LatLng(37.5846767, 126.9218555),
    new kakao.maps.LatLng(37.5852834, 126.9223929),
    new kakao.maps.LatLng(37.5856304, 126.9228635),
    new kakao.maps.LatLng(37.5869714, 126.923861),
    new kakao.maps.LatLng(37.5871207, 126.9240038),
    new kakao.maps.LatLng(37.5872166, 126.9246107),
    new kakao.maps.LatLng(37.5872168, 126.9252644),
    new kakao.maps.LatLng(37.5883854, 126.928009),
    new kakao.maps.LatLng(37.5911032, 126.927947),
    new kakao.maps.LatLng(37.5915762, 126.9277682),
    new kakao.maps.LatLng(37.5945528, 126.9302704),
    new kakao.maps.LatLng(37.5962984, 126.9327954),
    new kakao.maps.LatLng(37.5974786, 126.9364086),
    new kakao.maps.LatLng(37.5976207, 126.9382703),
    new kakao.maps.LatLng(37.5987329, 126.9408662),
    new kakao.maps.LatLng(37.6006774, 126.9413766),
    new kakao.maps.LatLng(37.6013511, 126.9407255),
    new kakao.maps.LatLng(37.6049576, 126.9421378),
    new kakao.maps.LatLng(37.6086085, 126.9482139),
    new kakao.maps.LatLng(37.609399, 126.9489364),
    new kakao.maps.LatLng(37.6138494, 126.9507966),
    new kakao.maps.LatLng(37.6155379, 126.9507242),
    new kakao.maps.LatLng(37.6199205, 126.9499112),
    new kakao.maps.LatLng(37.6207316, 126.9499381),
    new kakao.maps.LatLng(37.6209324, 126.9499158),
    new kakao.maps.LatLng(37.6232616, 126.9488984),
    new kakao.maps.LatLng(37.626418, 126.9504537),
    new kakao.maps.LatLng(37.6265452, 126.9516053),
    new kakao.maps.LatLng(37.628731, 126.956889),
    new kakao.maps.LatLng(37.6295893, 126.9588137)
];

        var eunpyeongPolygonB = new kakao.maps.Polygon({
            path: eunpyeongPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 마포구 다각형 생성(22대선)
        var mapoPolygonBPath = [
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.55675317809392, 126.93190919632814),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.557241466445234, 126.95913438471307),
            new kakao.maps.LatLng(37.55908394430372, 126.96163689468189),
            new kakao.maps.LatLng(37.55820141918588, 126.96305432966605),
            new kakao.maps.LatLng(37.554784413504734, 126.9617251098019),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.539468942052544, 126.955731506394),
            new kakao.maps.LatLng(37.536292068277106, 126.95128907260018),
            new kakao.maps.LatLng(37.53569162926515, 126.94627494388307),
            new kakao.maps.LatLng(37.53377712226906, 126.94458373402794),
            new kakao.maps.LatLng(37.54135238063506, 126.93031191951576),
            new kakao.maps.LatLng(37.539036674424615, 126.9271006565075),
            new kakao.maps.LatLng(37.54143034750605, 126.9224138272872),
            new kakao.maps.LatLng(37.54141748538761, 126.90483000187002),
            new kakao.maps.LatLng(37.548015078285694, 126.89890097452322),
            new kakao.maps.LatLng(37.56300401736817, 126.86623824787709),
            new kakao.maps.LatLng(37.57178997971358, 126.85363039091744),
            new kakao.maps.LatLng(37.57379738998644, 126.85362646212587),
            new kakao.maps.LatLng(37.57747251471329, 126.864939928088),
            new kakao.maps.LatLng(37.5781913017327, 126.87625939970273),
            new kakao.maps.LatLng(37.57977132158497, 126.87767870371688),
            new kakao.maps.LatLng(37.584440882833654, 126.87653889183002),
            new kakao.maps.LatLng(37.59079311146897, 126.88205386700724),
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884)
        ];

        var mapoPolygonB = new kakao.maps.Polygon({
            path: mapoPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 양천구 다각형 생성(22대선)
        var yangcheonPolygonBPath = [
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5397562, 126.8216026),
    new kakao.maps.LatLng(37.5365431, 126.8224338),
    new kakao.maps.LatLng(37.5348887, 126.821878),
    new kakao.maps.LatLng(37.5299154, 126.8254181),
    new kakao.maps.LatLng(37.528389, 126.8279799),
    new kakao.maps.LatLng(37.5258342, 126.8281793),
    new kakao.maps.LatLng(37.5249238, 126.8264622),
    new kakao.maps.LatLng(37.5230079, 126.8251384),
    new kakao.maps.LatLng(37.5198753, 126.8255944),
    new kakao.maps.LatLng(37.516186, 126.8231123),
    new kakao.maps.LatLng(37.5130434, 126.8244262),
    new kakao.maps.LatLng(37.5090953, 126.8239041),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5187577, 126.8782517),
    new kakao.maps.LatLng(37.5203627, 126.879464),
    new kakao.maps.LatLng(37.5252536, 126.878749),
    new kakao.maps.LatLng(37.5259082, 126.8809399),
    new kakao.maps.LatLng(37.5287593, 126.8843314),
    new kakao.maps.LatLng(37.5301503, 126.8871006),
    new kakao.maps.LatLng(37.5301524, 126.8896671),
    new kakao.maps.LatLng(37.5319258, 126.8890681),
    new kakao.maps.LatLng(37.5351351, 126.8897886),
    new kakao.maps.LatLng(37.5397825, 126.8863138),
    new kakao.maps.LatLng(37.543321, 126.885088),
    new kakao.maps.LatLng(37.5481962, 126.880664),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.546944, 126.8745052)
];

        var yangcheonPolygonB = new kakao.maps.Polygon({
            path: yangcheonPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강서구 다각형 생성(22대선)
        var gangseoPolygonBPath = [
    new kakao.maps.LatLng(37.5717904, 126.8536316),
    new kakao.maps.LatLng(37.5737991, 126.8536283),
    new kakao.maps.LatLng(37.5745142, 126.8510083),
    new kakao.maps.LatLng(37.5773942, 126.8467014),
    new kakao.maps.LatLng(37.5835872, 126.8327892),
    new kakao.maps.LatLng(37.588201, 126.8270511),
    new kakao.maps.LatLng(37.5900825, 126.8252892),
    new kakao.maps.LatLng(37.5912976, 126.822785),
    new kakao.maps.LatLng(37.5976193, 126.8139529),
    new kakao.maps.LatLng(37.5989607, 126.8113687),
    new kakao.maps.LatLng(37.604902, 126.8027567),
    new kakao.maps.LatLng(37.6024867, 126.7999484),
    new kakao.maps.LatLng(37.6013474, 126.7998667),
    new kakao.maps.LatLng(37.5998709, 126.7978909),
    new kakao.maps.LatLng(37.597712, 126.797114),
    new kakao.maps.LatLng(37.5947537, 126.797721),
    new kakao.maps.LatLng(37.5936525, 126.798726),
    new kakao.maps.LatLng(37.5913058, 126.7988344),
    new kakao.maps.LatLng(37.589326, 126.8012524),
    new kakao.maps.LatLng(37.5878099, 126.8007605),
    new kakao.maps.LatLng(37.5880729, 126.7987679),
    new kakao.maps.LatLng(37.583364, 126.7956796),
    new kakao.maps.LatLng(37.5797103, 126.7924063),
    new kakao.maps.LatLng(37.5805208, 126.7907535),
    new kakao.maps.LatLng(37.5777706, 126.790599),
    new kakao.maps.LatLng(37.5777198, 126.7893694),
    new kakao.maps.LatLng(37.5755709, 126.787642),
    new kakao.maps.LatLng(37.5735993, 126.7824424),
    new kakao.maps.LatLng(37.5692071, 126.7816643),
    new kakao.maps.LatLng(37.5672821, 126.7789707),
    new kakao.maps.LatLng(37.5670966, 126.776366),
    new kakao.maps.LatLng(37.5658733, 126.7751607),
    new kakao.maps.LatLng(37.5637152, 126.7771261),
    new kakao.maps.LatLng(37.5618635, 126.7761087),
    new kakao.maps.LatLng(37.5572273, 126.7698955),
    new kakao.maps.LatLng(37.5554503, 126.7645763),
    new kakao.maps.LatLng(37.5539545, 126.7676412),
    new kakao.maps.LatLng(37.551962, 126.7674713),
    new kakao.maps.LatLng(37.5515813, 126.7693259),
    new kakao.maps.LatLng(37.548316, 126.7717031),
    new kakao.maps.LatLng(37.5489742, 126.7752973),
    new kakao.maps.LatLng(37.54671, 126.7775751),
    new kakao.maps.LatLng(37.5460749, 126.7818371),
    new kakao.maps.LatLng(37.545997, 126.7869552),
    new kakao.maps.LatLng(37.5438485, 126.7907616),
    new kakao.maps.LatLng(37.541761, 126.7921302),
    new kakao.maps.LatLng(37.541372, 126.7949442),
    new kakao.maps.LatLng(37.5395572, 126.7938932),
    new kakao.maps.LatLng(37.5373674, 126.7939734),
    new kakao.maps.LatLng(37.5367714, 126.7961149),
    new kakao.maps.LatLng(37.5378446, 126.7994886),
    new kakao.maps.LatLng(37.5403453, 126.7988931),
    new kakao.maps.LatLng(37.5408808, 126.8008976),
    new kakao.maps.LatLng(37.5426716, 126.8016672),
    new kakao.maps.LatLng(37.5436059, 126.8068721),
    new kakao.maps.LatLng(37.5407765, 126.8125684),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5484626, 126.8804437),
    new kakao.maps.LatLng(37.5494053, 126.8798959),
    new kakao.maps.LatLng(37.5497628, 126.8796001),
    new kakao.maps.LatLng(37.5499377, 126.8794778),
    new kakao.maps.LatLng(37.5500282, 126.8794146),
    new kakao.maps.LatLng(37.550412, 126.8791236),
    new kakao.maps.LatLng(37.5507488, 126.8788459),
    new kakao.maps.LatLng(37.5511263, 126.8787108),
    new kakao.maps.LatLng(37.5515205, 126.8781985),
    new kakao.maps.LatLng(37.5519352, 126.8780413),
    new kakao.maps.LatLng(37.5523189, 126.8780313),
    new kakao.maps.LatLng(37.5525651, 126.8780226),
    new kakao.maps.LatLng(37.5527979, 126.8780142),
    new kakao.maps.LatLng(37.5529934, 126.8780067),
    new kakao.maps.LatLng(37.5531701, 126.8779519),
    new kakao.maps.LatLng(37.5532133, 126.8779456),
    new kakao.maps.LatLng(37.5534501, 126.8779539),
    new kakao.maps.LatLng(37.5535245, 126.8780551),
    new kakao.maps.LatLng(37.553546, 126.8781144),
    new kakao.maps.LatLng(37.5535815, 126.8782443),
    new kakao.maps.LatLng(37.5533372, 126.878835),
    new kakao.maps.LatLng(37.5532765, 126.8789601),
    new kakao.maps.LatLng(37.5531512, 126.8792171),
    new kakao.maps.LatLng(37.5537026, 126.879224),
    new kakao.maps.LatLng(37.554747, 126.879237),
    new kakao.maps.LatLng(37.5550643, 126.8794927),
    new kakao.maps.LatLng(37.555305, 126.879688),
    new kakao.maps.LatLng(37.556224, 126.8804278),
    new kakao.maps.LatLng(37.5562828, 126.8804743),
    new kakao.maps.LatLng(37.5565904, 126.8798677),
    new kakao.maps.LatLng(37.5566999, 126.8796536),
    new kakao.maps.LatLng(37.5569932, 126.8790797),
    new kakao.maps.LatLng(37.5571835, 126.8787108),
    new kakao.maps.LatLng(37.5577477, 126.8776168),
    new kakao.maps.LatLng(37.5580956, 126.8769422),
    new kakao.maps.LatLng(37.5582839, 126.8765751),
    new kakao.maps.LatLng(37.5589502, 126.8752775),
    new kakao.maps.LatLng(37.5591563, 126.8748767),
    new kakao.maps.LatLng(37.5595945, 126.874025),
    new kakao.maps.LatLng(37.5596946, 126.8738248),
    new kakao.maps.LatLng(37.5601596, 126.8728588),
    new kakao.maps.LatLng(37.5605276, 126.8720972),
    new kakao.maps.LatLng(37.5609333, 126.8712519),
    new kakao.maps.LatLng(37.5615358, 126.8699951),
    new kakao.maps.LatLng(37.5619632, 126.8691064),
    new kakao.maps.LatLng(37.5621959, 126.868634),
    new kakao.maps.LatLng(37.5627029, 126.8677403),
    new kakao.maps.LatLng(37.5629894, 126.8672261),
    new kakao.maps.LatLng(37.5632825, 126.8666958),
    new kakao.maps.LatLng(37.5637559, 126.8658888),
    new kakao.maps.LatLng(37.5640521, 126.8654083),
    new kakao.maps.LatLng(37.5644624, 126.8647347),
    new kakao.maps.LatLng(37.5647185, 126.8643124),
    new kakao.maps.LatLng(37.5649731, 126.8639165),
    new kakao.maps.LatLng(37.5650512, 126.8637912),
    new kakao.maps.LatLng(37.5652642, 126.8634888),
    new kakao.maps.LatLng(37.5653859, 126.8633098),
    new kakao.maps.LatLng(37.5654471, 126.8632313),
    new kakao.maps.LatLng(37.5655495, 126.8630904),
    new kakao.maps.LatLng(37.5657186, 126.8628754),
    new kakao.maps.LatLng(37.5660443, 126.8624873),
    new kakao.maps.LatLng(37.5663031, 126.8621474),
    new kakao.maps.LatLng(37.5663376, 126.8621034),
    new kakao.maps.LatLng(37.5664484, 126.8619718),
    new kakao.maps.LatLng(37.5667462, 126.861637),
    new kakao.maps.LatLng(37.5672618, 126.8610683),
    new kakao.maps.LatLng(37.5675217, 126.8607424),
    new kakao.maps.LatLng(37.5676648, 126.8605839),
    new kakao.maps.LatLng(37.5679501, 126.8602879),
    new kakao.maps.LatLng(37.5682635, 126.8599471),
    new kakao.maps.LatLng(37.5686039, 126.8595982),
    new kakao.maps.LatLng(37.5688681, 126.8592962),
    new kakao.maps.LatLng(37.5693278, 126.8588345),
    new kakao.maps.LatLng(37.5695699, 126.8585727),
    new kakao.maps.LatLng(37.5700741, 126.8580604),
    new kakao.maps.LatLng(37.5702804, 126.8578288),
    new kakao.maps.LatLng(37.5704464, 126.8576497),
    new kakao.maps.LatLng(37.5705987, 126.8574919),
    new kakao.maps.LatLng(37.5708578, 126.8572342),
    new kakao.maps.LatLng(37.5710034, 126.8571121),
    new kakao.maps.LatLng(37.5712288, 126.8569134),
    new kakao.maps.LatLng(37.5715422, 126.8566245),
    new kakao.maps.LatLng(37.5717665, 126.8564237),
    new kakao.maps.LatLng(37.5717904, 126.8536316)
];

        var gangseoPolygonB = new kakao.maps.Polygon({
            path: gangseoPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 구로구 다각형 생성(22대선)
        var guroPolygonBPath = [
    new kakao.maps.LatLng(37.4849988, 126.9031946),
    new kakao.maps.LatLng(37.4869351, 126.8981442),
    new kakao.maps.LatLng(37.4893387, 126.896124),
    new kakao.maps.LatLng(37.5033326, 126.8926737),
    new kakao.maps.LatLng(37.5050117, 126.8939767),
    new kakao.maps.LatLng(37.5103503, 126.8917119),
    new kakao.maps.LatLng(37.5132264, 126.8875197),
    new kakao.maps.LatLng(37.5138494, 126.8844331),
    new kakao.maps.LatLng(37.5164199, 126.881729),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5076346, 126.8222152),
    new kakao.maps.LatLng(37.5056852, 126.8225503),
    new kakao.maps.LatLng(37.5022364, 126.821611),
    new kakao.maps.LatLng(37.5006401, 126.8194028),
    new kakao.maps.LatLng(37.4993555, 126.8196714),
    new kakao.maps.LatLng(37.4977435, 126.8161301),
    new kakao.maps.LatLng(37.4982134, 126.8141214),
    new kakao.maps.LatLng(37.4964818, 126.8129811),
    new kakao.maps.LatLng(37.4931969, 126.814573),
    new kakao.maps.LatLng(37.4915531, 126.817904),
    new kakao.maps.LatLng(37.4899794, 126.822762),
    new kakao.maps.LatLng(37.4877351, 126.8235061),
    new kakao.maps.LatLng(37.4854809, 126.8192969),
    new kakao.maps.LatLng(37.4816405, 126.8199827),
    new kakao.maps.LatLng(37.4791625, 126.8189971),
    new kakao.maps.LatLng(37.4763621, 126.8152952),
    new kakao.maps.LatLng(37.4747205, 126.8146459),
    new kakao.maps.LatLng(37.4732881, 126.817076),
    new kakao.maps.LatLng(37.4741192, 126.8187239),
    new kakao.maps.LatLng(37.4763553, 126.8195989),
    new kakao.maps.LatLng(37.4759897, 126.8278719),
    new kakao.maps.LatLng(37.4776512, 126.8317475),
    new kakao.maps.LatLng(37.4767532, 126.8339281),
    new kakao.maps.LatLng(37.4744809, 126.8359294),
    new kakao.maps.LatLng(37.475392, 126.8383005),
    new kakao.maps.LatLng(37.4746479, 126.8410321),
    new kakao.maps.LatLng(37.4749715, 126.8427814),
    new kakao.maps.LatLng(37.4738124, 126.8453603),
    new kakao.maps.LatLng(37.480012, 126.8459113),
    new kakao.maps.LatLng(37.48191, 126.8470155),
    new kakao.maps.LatLng(37.481827, 126.8527424),
    new kakao.maps.LatLng(37.4854067, 126.8555066),
    new kakao.maps.LatLng(37.4860846, 126.8579708),
    new kakao.maps.LatLng(37.4899682, 126.8613841),
    new kakao.maps.LatLng(37.4915699, 126.8654623),
    new kakao.maps.LatLng(37.49426, 126.8668088),
    new kakao.maps.LatLng(37.4951278, 126.8683565),
    new kakao.maps.LatLng(37.4940956, 126.8697092),
    new kakao.maps.LatLng(37.4916613, 126.8693466),
    new kakao.maps.LatLng(37.4895402, 126.8704101),
    new kakao.maps.LatLng(37.4906414, 126.8723345),
    new kakao.maps.LatLng(37.4882584, 126.8730843),
    new kakao.maps.LatLng(37.4885708, 126.8767901),
    new kakao.maps.LatLng(37.4853671, 126.8745638),
    new kakao.maps.LatLng(37.4866723, 126.8784581),
    new kakao.maps.LatLng(37.4855632, 126.8813537),
    new kakao.maps.LatLng(37.4823496, 126.886155),
    new kakao.maps.LatLng(37.4804414, 126.8877295),
    new kakao.maps.LatLng(37.4793897, 126.8898815),
    new kakao.maps.LatLng(37.4783336, 126.8964731),
    new kakao.maps.LatLng(37.4789401, 126.8989434),
    new kakao.maps.LatLng(37.4811733, 126.900064),
    new kakao.maps.LatLng(37.4849988, 126.9031946)
];

        var guroPolygonB = new kakao.maps.Polygon({
            path: guroPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
     
        // 금천구 다각형 생성(22대선)
        var geumcheonPolygonBPath = [ new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4783336, 126.8964731), new kakao.maps.LatLng(37.4793897, 126.8898815), new kakao.maps.LatLng(37.4804414, 126.8877295), new kakao.maps.LatLng(37.4823496, 126.886155), new kakao.maps.LatLng(37.4855632, 126.8813537), new kakao.maps.LatLng(37.4866723, 126.8784581), new kakao.maps.LatLng(37.4853671, 126.8745638), new kakao.maps.LatLng(37.4852298, 126.8718245), new kakao.maps.LatLng(37.4836436, 126.8728822), new kakao.maps.LatLng(37.4771039, 126.8759855), new kakao.maps.LatLng(37.4738278, 126.8780112), new kakao.maps.LatLng(37.4694169, 126.8815927), new kakao.maps.LatLng(37.4684591, 126.881631), new kakao.maps.LatLng(37.4665184, 126.8842988), new kakao.maps.LatLng(37.4643925, 126.8827454), new kakao.maps.LatLng(37.4627255, 126.884317), new kakao.maps.LatLng(37.4627551, 126.8861117), new kakao.maps.LatLng(37.4575101, 126.8858806), new kakao.maps.LatLng(37.4561777, 126.8863993), new kakao.maps.LatLng(37.4544844, 126.8892662), new kakao.maps.LatLng(37.4524961, 126.8903312), new kakao.maps.LatLng(37.451995, 126.8927328), new kakao.maps.LatLng(37.4527181, 126.8939824), new kakao.maps.LatLng(37.4484134, 126.8959156), new kakao.maps.LatLng(37.4466982, 126.8946497), new kakao.maps.LatLng(37.4454288, 126.8972601), new kakao.maps.LatLng(37.4369929, 126.9008673), new kakao.maps.LatLng(37.4358535, 126.902834), new kakao.maps.LatLng(37.4340675, 126.9029873), new kakao.maps.LatLng(37.4338646, 126.9094057), new kakao.maps.LatLng(37.4361712, 126.9113332), new kakao.maps.LatLng(37.4385546, 126.912294), new kakao.maps.LatLng(37.4400154, 126.9161336), new kakao.maps.LatLng(37.439825, 126.9192897), new kakao.maps.LatLng(37.444041, 126.9227625), new kakao.maps.LatLng(37.4457729, 126.923253), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4789401, 126.8989434) ];

        var geumcheonPolygonB = new kakao.maps.Polygon({
            path: geumcheonPolygonBPath,
            fillColor: '#0066ff',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#0066ff',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

                // 영등포구 다각형 생성(22대선)
        var yeongdeungpoPolygonBPath = [ new kakao.maps.LatLng(37.5339056, 126.9446791), new kakao.maps.LatLng(37.5378354, 126.938558), new kakao.maps.LatLng(37.5405306, 126.9328982), new kakao.maps.LatLng(37.5413625, 126.9303377), new kakao.maps.LatLng(37.5390762, 126.9276653), new kakao.maps.LatLng(37.5397435, 126.9248228), new kakao.maps.LatLng(37.5414296, 126.922414), new kakao.maps.LatLng(37.5414165, 126.9048307), new kakao.maps.LatLng(37.5480079, 126.898943), new kakao.maps.LatLng(37.5494341, 126.8946416), new kakao.maps.LatLng(37.5523, 126.8881084), new kakao.maps.LatLng(37.5558475, 126.88131), new kakao.maps.LatLng(37.556224, 126.8804278), new kakao.maps.LatLng(37.555305, 126.879688), new kakao.maps.LatLng(37.5550643, 126.8794927), new kakao.maps.LatLng(37.554747, 126.879237), new kakao.maps.LatLng(37.5537026, 126.879224), new kakao.maps.LatLng(37.5531512, 126.8792171), new kakao.maps.LatLng(37.5532765, 126.8789601), new kakao.maps.LatLng(37.5533372, 126.878835), new kakao.maps.LatLng(37.5535815, 126.8782443), new kakao.maps.LatLng(37.553546, 126.8781144), new kakao.maps.LatLng(37.5535245, 126.8780551), new kakao.maps.LatLng(37.5534501, 126.8779539), new kakao.maps.LatLng(37.5532133, 126.8779456), new kakao.maps.LatLng(37.5531701, 126.8779519), new kakao.maps.LatLng(37.5529934, 126.8780067), new kakao.maps.LatLng(37.5527979, 126.8780142), new kakao.maps.LatLng(37.5525651, 126.8780226), new kakao.maps.LatLng(37.5523189, 126.8780313), new kakao.maps.LatLng(37.5519352, 126.8780413), new kakao.maps.LatLng(37.5515205, 126.8781985), new kakao.maps.LatLng(37.5511263, 126.8785301), new kakao.maps.LatLng(37.5507488, 126.8788459), new kakao.maps.LatLng(37.550412, 126.8791236), new kakao.maps.LatLng(37.5500282, 126.8794146), new kakao.maps.LatLng(37.5499377, 126.8794778), new kakao.maps.LatLng(37.5497628, 126.8796001), new kakao.maps.LatLng(37.5494053, 126.8798959), new kakao.maps.LatLng(37.5484626, 126.8804437), new kakao.maps.LatLng(37.5481962, 126.880664), new kakao.maps.LatLng(37.543321, 126.885088), new kakao.maps.LatLng(37.5397825, 126.8863138), new kakao.maps.LatLng(37.5351351, 126.8897886), new kakao.maps.LatLng(37.5319258, 126.8890681), new kakao.maps.LatLng(37.5301524, 126.8896671), new kakao.maps.LatLng(37.5301503, 126.8871006), new kakao.maps.LatLng(37.5287593, 126.8843314), new kakao.maps.LatLng(37.5259082, 126.8809399), new kakao.maps.LatLng(37.5252536, 126.878749), new kakao.maps.LatLng(37.5203627, 126.879464), new kakao.maps.LatLng(37.5187577, 126.8782517), new kakao.maps.LatLng(37.5178764, 126.8791653), new kakao.maps.LatLng(37.5164199, 126.881729), new kakao.maps.LatLng(37.5138494, 126.8844331), new kakao.maps.LatLng(37.5132264, 126.8875197), new kakao.maps.LatLng(37.5103503, 126.8917119), new kakao.maps.LatLng(37.5050117, 126.8939767), new kakao.maps.LatLng(37.5033326, 126.8926737), new kakao.maps.LatLng(37.4893387, 126.896124), new kakao.maps.LatLng(37.4869351, 126.8981442), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4938221, 126.9104722), new kakao.maps.LatLng(37.4964189, 126.9129118), new kakao.maps.LatLng(37.4975997, 126.9194077), new kakao.maps.LatLng(37.5125265, 126.9253894), new kakao.maps.LatLng(37.5127969, 126.9267906), new kakao.maps.LatLng(37.5155543, 126.9268588), new kakao.maps.LatLng(37.5155752, 126.9323857), new kakao.maps.LatLng(37.5160787, 126.9392792), new kakao.maps.LatLng(37.5175262, 126.9498866), new kakao.maps.LatLng(37.5270289, 126.94988), new kakao.maps.LatLng(37.5339056, 126.9446791) ];

        var yeongdeungpoPolygonB = new kakao.maps.Polygon({
            path: yeongdeungpoPolygonAPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        
                // 동작구 다각형 생성(22대선)
                var dongjakPolygonBPath = [
    new kakao.maps.LatLng(37.5065363, 126.9804067),
    new kakao.maps.LatLng(37.5070128, 126.9752589),
    new kakao.maps.LatLng(37.5108166, 126.9649636),
    new kakao.maps.LatLng(37.5135025, 126.9612002),
    new kakao.maps.LatLng(37.516065, 126.9547037),
    new kakao.maps.LatLng(37.5175262, 126.9498866),
    new kakao.maps.LatLng(37.5160787, 126.9392792),
    new kakao.maps.LatLng(37.5155752, 126.9323857),
    new kakao.maps.LatLng(37.5155543, 126.9268588),
    new kakao.maps.LatLng(37.5127969, 126.9267906),
    new kakao.maps.LatLng(37.5125265, 126.9253894),
    new kakao.maps.LatLng(37.4975997, 126.9194077),
    new kakao.maps.LatLng(37.4964189, 126.9129118),
    new kakao.maps.LatLng(37.4938221, 126.9104722),
    new kakao.maps.LatLng(37.4850028, 126.9031989),
    new kakao.maps.LatLng(37.4849606, 126.9060977),
    new kakao.maps.LatLng(37.4865116, 126.911921),
    new kakao.maps.LatLng(37.4880073, 126.9135728),
    new kakao.maps.LatLng(37.489548, 126.9166515),
    new kakao.maps.LatLng(37.4902759, 126.9194523),
    new kakao.maps.LatLng(37.4899637, 126.924155),
    new kakao.maps.LatLng(37.4927983, 126.925577),
    new kakao.maps.LatLng(37.4949943, 126.9274611),
    new kakao.maps.LatLng(37.4932585, 126.9313461),
    new kakao.maps.LatLng(37.493189, 126.933849),
    new kakao.maps.LatLng(37.4919697, 126.9365336),
    new kakao.maps.LatLng(37.4929037, 126.9399265),
    new kakao.maps.LatLng(37.4921435, 126.9426218),
    new kakao.maps.LatLng(37.494039, 126.9471828),
    new kakao.maps.LatLng(37.4922055, 126.9516974),
    new kakao.maps.LatLng(37.4906416, 126.9537273),
    new kakao.maps.LatLng(37.4919773, 126.9574784),
    new kakao.maps.LatLng(37.4936159, 126.9589433),
    new kakao.maps.LatLng(37.4928741, 126.9613777),
    new kakao.maps.LatLng(37.4908252, 126.9607812),
    new kakao.maps.LatLng(37.4886278, 126.9619669),
    new kakao.maps.LatLng(37.4851775, 126.9619872),
    new kakao.maps.LatLng(37.4835752, 126.96107),
    new kakao.maps.LatLng(37.4798186, 126.9644275),
    new kakao.maps.LatLng(37.4789597, 126.9663255),
    new kakao.maps.LatLng(37.4753765, 126.9705226),
    new kakao.maps.LatLng(37.476201, 126.9742856),
    new kakao.maps.LatLng(37.4770573, 126.9816808),
    new kakao.maps.LatLng(37.4969936, 126.9829297),
    new kakao.maps.LatLng(37.499859, 126.9853872),
    new kakao.maps.LatLng(37.5026966, 126.9805363),
    new kakao.maps.LatLng(37.5065363, 126.9804067)
];

        var dongjakPolygonB = new kakao.maps.Polygon({
            path: dongjakPolygonBPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

// 관악구 다각형 생성(22대선)
var gwanakPolygonBPath = [ new kakao.maps.LatLng(37.4770573, 126.9816808), new kakao.maps.LatLng(37.476201, 126.9742856), new kakao.maps.LatLng(37.4753765, 126.9705226), new kakao.maps.LatLng(37.4789597, 126.9663255), new kakao.maps.LatLng(37.4798186, 126.9644275), new kakao.maps.LatLng(37.4835752, 126.96107), new kakao.maps.LatLng(37.4851775, 126.9619872), new kakao.maps.LatLng(37.4886278, 126.9619669), new kakao.maps.LatLng(37.4908252, 126.9607812), new kakao.maps.LatLng(37.4928741, 126.9613777), new kakao.maps.LatLng(37.4936159, 126.9589433), new kakao.maps.LatLng(37.4919773, 126.9574784), new kakao.maps.LatLng(37.4906416, 126.9537273), new kakao.maps.LatLng(37.4922055, 126.9516974), new kakao.maps.LatLng(37.494039, 126.9471828), new kakao.maps.LatLng(37.4921435, 126.9426218), new kakao.maps.LatLng(37.4929037, 126.9399265), new kakao.maps.LatLng(37.4919697, 126.9365336), new kakao.maps.LatLng(37.493189, 126.933849), new kakao.maps.LatLng(37.4932585, 126.9313461), new kakao.maps.LatLng(37.4949943, 126.9274611), new kakao.maps.LatLng(37.4927983, 126.925577), new kakao.maps.LatLng(37.4899637, 126.924155), new kakao.maps.LatLng(37.4902759, 126.9194523), new kakao.maps.LatLng(37.489548, 126.9166515), new kakao.maps.LatLng(37.4880073, 126.9135728), new kakao.maps.LatLng(37.4865116, 126.911921), new kakao.maps.LatLng(37.4849606, 126.9060977), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4811733, 126.900064), new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4483842, 126.9301661), new kakao.maps.LatLng(37.445463, 126.9305669), new kakao.maps.LatLng(37.4417395, 126.9366582), new kakao.maps.LatLng(37.4402029, 126.9378509), new kakao.maps.LatLng(37.4373807, 126.9377535), new kakao.maps.LatLng(37.4357034, 126.9402441), new kakao.maps.LatLng(37.4373944, 126.9414554), new kakao.maps.LatLng(37.4370754, 126.9451252), new kakao.maps.LatLng(37.4387126, 126.9483629), new kakao.maps.LatLng(37.4382501, 126.9492839), new kakao.maps.LatLng(37.4392385, 126.9523939), new kakao.maps.LatLng(37.4387351, 126.9551493), new kakao.maps.LatLng(37.4391229, 126.9589137), new kakao.maps.LatLng(37.4404007, 126.9600556), new kakao.maps.LatLng(37.4402806, 126.9629426), new kakao.maps.LatLng(37.4420397, 126.9646338), new kakao.maps.LatLng(37.4462673, 126.9642894), new kakao.maps.LatLng(37.4483804, 126.9676626), new kakao.maps.LatLng(37.4494526, 126.9705691), new kakao.maps.LatLng(37.4516571, 126.9718463), new kakao.maps.LatLng(37.454323, 126.9746584), new kakao.maps.LatLng(37.4556507, 126.978552), new kakao.maps.LatLng(37.4558313, 126.9824203), new kakao.maps.LatLng(37.4568271, 126.9828879), new kakao.maps.LatLng(37.4572124, 126.9866124), new kakao.maps.LatLng(37.4581534, 126.9886043), new kakao.maps.LatLng(37.4600297, 126.9875747), new kakao.maps.LatLng(37.4639986, 126.988344), new kakao.maps.LatLng(37.4676122, 126.9873023), new kakao.maps.LatLng(37.4698246, 126.9845159), new kakao.maps.LatLng(37.4737189, 126.9821725), new kakao.maps.LatLng(37.4770573, 126.9816808) ];

var gwanakPolygonB = new kakao.maps.Polygon({
    path: gwanakPolygonBPath,
    fillColor: '#0066ff',
    fillOpacity: 0.5,
    strokeWeight: 1,
    strokeColor: '#0066ff',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 서초구 다각형 생성(22대선)
var seochoPolygonBPath = [
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.5234361, 127.0064445),
new kakao.maps.LatLng(37.5194968, 127.0007883),
new kakao.maps.LatLng(37.5131024, 126.9906716),
new kakao.maps.LatLng(37.5065431, 126.9855327),
new kakao.maps.LatLng(37.5065363, 126.9804067),
new kakao.maps.LatLng(37.5026966, 126.9805363),
new kakao.maps.LatLng(37.499859, 126.9853872),
new kakao.maps.LatLng(37.4969936, 126.9829297),
new kakao.maps.LatLng(37.4770573, 126.9816808),
new kakao.maps.LatLng(37.4737189, 126.9821725),
new kakao.maps.LatLng(37.4698246, 126.9845159),
new kakao.maps.LatLng(37.4676122, 126.9873023),
new kakao.maps.LatLng(37.4639986, 126.988344),
new kakao.maps.LatLng(37.4600297, 126.9875747),
new kakao.maps.LatLng(37.4581534, 126.9886043),
new kakao.maps.LatLng(37.4614959, 126.9933541),
new kakao.maps.LatLng(37.4618734, 126.9967683),
new kakao.maps.LatLng(37.464215, 126.9972632),
new kakao.maps.LatLng(37.4666083, 126.9962307),
new kakao.maps.LatLng(37.4671797, 126.9969853),
new kakao.maps.LatLng(37.4671246, 127.0027346),
new kakao.maps.LatLng(37.4657636, 127.0049273),
new kakao.maps.LatLng(37.4640347, 127.0045148),
new kakao.maps.LatLng(37.4578423, 127.0086622),
new kakao.maps.LatLng(37.4554428, 127.010818),
new kakao.maps.LatLng(37.4548611, 127.0145094),
new kakao.maps.LatLng(37.4561351, 127.017545),
new kakao.maps.LatLng(37.4556938, 127.0192823),
new kakao.maps.LatLng(37.4572538, 127.022851),
new kakao.maps.LatLng(37.4574817, 127.0252753),
new kakao.maps.LatLng(37.4596417, 127.0265719),
new kakao.maps.LatLng(37.4633413, 127.0296306),
new kakao.maps.LatLng(37.4653746, 127.0295269),
new kakao.maps.LatLng(37.4656262, 127.0311954),
new kakao.maps.LatLng(37.4641547, 127.0346931),
new kakao.maps.LatLng(37.4612371, 127.0337319),
new kakao.maps.LatLng(37.4601754, 127.0349239),
new kakao.maps.LatLng(37.4578668, 127.0350694),
new kakao.maps.LatLng(37.455203, 127.0371709),
new kakao.maps.LatLng(37.4526095, 127.0347723),
new kakao.maps.LatLng(37.4514669, 127.0364748),
new kakao.maps.LatLng(37.4494531, 127.037741),
new kakao.maps.LatLng(37.4464509, 127.0372545),
new kakao.maps.LatLng(37.4451803, 127.0382301),
new kakao.maps.LatLng(37.4432667, 127.0374826),
new kakao.maps.LatLng(37.4410155, 127.0352603),
new kakao.maps.LatLng(37.4391373, 127.0356865),
new kakao.maps.LatLng(37.4383913, 127.0371471),
new kakao.maps.LatLng(37.4383412, 127.0401422),
new kakao.maps.LatLng(37.4335915, 127.0463942),
new kakao.maps.LatLng(37.4307906, 127.0473967),
new kakao.maps.LatLng(37.4303374, 127.0493227),
new kakao.maps.LatLng(37.4284561, 127.0520464),
new kakao.maps.LatLng(37.4301499, 127.0578618),
new kakao.maps.LatLng(37.4301216, 127.0608665),
new kakao.maps.LatLng(37.4290228, 127.0656551),
new kakao.maps.LatLng(37.4307189, 127.0683088),
new kakao.maps.LatLng(37.4308177, 127.0712064),
new kakao.maps.LatLng(37.4324169, 127.0705709),
new kakao.maps.LatLng(37.4358635, 127.0714392),
new kakao.maps.LatLng(37.4374234, 127.0738798),
new kakao.maps.LatLng(37.4388568, 127.0720075),
new kakao.maps.LatLng(37.4415239, 127.0716257),
new kakao.maps.LatLng(37.442133, 127.0761442),
new kakao.maps.LatLng(37.4410297, 127.0803008),
new kakao.maps.LatLng(37.4413384, 127.0821566),
new kakao.maps.LatLng(37.4439083, 127.083954),
new kakao.maps.LatLng(37.4442491, 127.0865305),
new kakao.maps.LatLng(37.4454138, 127.0882762),
new kakao.maps.LatLng(37.4486278, 127.0883265),
new kakao.maps.LatLng(37.4527827, 127.0909588),
new kakao.maps.LatLng(37.4536339, 127.0927253),
new kakao.maps.LatLng(37.4558885, 127.0935402),
new kakao.maps.LatLng(37.4565198, 127.095769),
new kakao.maps.LatLng(37.4562188, 127.0990955),
new kakao.maps.LatLng(37.4585341, 127.101167)
];

var seochoPolygonB = new kakao.maps.Polygon({
    path: seochoPolygonBPath,
    fillColor: '#E61E2B',
    fillOpacity: 0.5,
    strokeWeight: 1,
    strokeColor: '#E61E2B',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강남구 다각형 생성(22대선)
var gangnamPolygonBPath = [
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5286757, 127.0551335),
new kakao.maps.LatLng(37.5342726, 127.0460023),
new kakao.maps.LatLng(37.5358577, 127.0396637),
new kakao.maps.LatLng(37.5358238, 127.0211723),
new kakao.maps.LatLng(37.5342595, 127.0177593),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.4600566, 127.1039435),
new kakao.maps.LatLng(37.4621594, 127.1043465),
new kakao.maps.LatLng(37.4624345, 127.1064566),
new kakao.maps.LatLng(37.4616446, 127.1118201),
new kakao.maps.LatLng(37.4598893, 127.1134332),
new kakao.maps.LatLng(37.458634, 127.116896),
new kakao.maps.LatLng(37.4622006, 127.1174754),
new kakao.maps.LatLng(37.464372, 127.12144),
new kakao.maps.LatLng(37.4665205, 127.1242057)
];

var gangnamPolygonB = new kakao.maps.Polygon({
    path: gangnamPolygonBPath,
    fillColor: '#E61E2B',
    fillOpacity: 0.5,
    strokeWeight: 1,
    strokeColor: '#E61E2B',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 송파구 다각형 생성(22대선)
var songpaPolygonBPath = [
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5414079, 127.1082818),
new kakao.maps.LatLng(37.5270069, 127.090161),
new kakao.maps.LatLng(37.524759, 127.0856328),
new kakao.maps.LatLng(37.5229485, 127.0799746),
new kakao.maps.LatLng(37.522514, 127.0769544),
new kakao.maps.LatLng(37.523872, 127.0686631),
new kakao.maps.LatLng(37.5268818, 127.0607945),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4684191, 127.1270342),
new kakao.maps.LatLng(37.4677511, 127.1301405),
new kakao.maps.LatLng(37.4683941, 127.1327994),
new kakao.maps.LatLng(37.4697986, 127.1319826),
new kakao.maps.LatLng(37.4715382, 127.1328449),
new kakao.maps.LatLng(37.4746269, 127.1328558),
new kakao.maps.LatLng(37.4742406, 127.1354681),
new kakao.maps.LatLng(37.4739308, 127.1435264),
new kakao.maps.LatLng(37.4773315, 127.1443703),
new kakao.maps.LatLng(37.4772222, 127.1471451),
new kakao.maps.LatLng(37.4815898, 127.1474588),
new kakao.maps.LatLng(37.4840436, 127.1486828),
new kakao.maps.LatLng(37.4862358, 127.1521778),
new kakao.maps.LatLng(37.489672, 127.1585233),
new kakao.maps.LatLng(37.492048, 127.1584792),
new kakao.maps.LatLng(37.4943902, 127.1600312),
new kakao.maps.LatLng(37.4968237, 127.1597796),
new kakao.maps.LatLng(37.4995369, 127.1613552),
new kakao.maps.LatLng(37.5031794, 127.1577291),
new kakao.maps.LatLng(37.5018946, 127.1565548),
new kakao.maps.LatLng(37.5029854, 127.1521336),
new kakao.maps.LatLng(37.5046783, 127.1502631),
new kakao.maps.LatLng(37.5032338, 127.1477163),
new kakao.maps.LatLng(37.5054583, 127.1411493),
new kakao.maps.LatLng(37.5067087, 127.1415163),
new kakao.maps.LatLng(37.5085171, 127.139952),
new kakao.maps.LatLng(37.5123608, 127.1413929),
new kakao.maps.LatLng(37.5126573, 127.1435398),
new kakao.maps.LatLng(37.5156419, 127.1421313),
new kakao.maps.LatLng(37.5155915, 127.1446078),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var songpaPolygonB = new kakao.maps.Polygon({
    path: songpaPolygonBPath,
    fillColor: '#E61E2B',
    fillOpacity: 0.5,
    strokeWeight: 1,
    strokeColor: '#E61E2B',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강동구 다각형 생성(22대선)
var gangdongPolygonBPath =[
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.5196245, 127.1447856),
new kakao.maps.LatLng(37.5219397, 127.1457414),
new kakao.maps.LatLng(37.5221448, 127.1478181),
new kakao.maps.LatLng(37.5263728, 127.1504017),
new kakao.maps.LatLng(37.5285295, 127.1526867),
new kakao.maps.LatLng(37.5319199, 127.1539334),
new kakao.maps.LatLng(37.533683, 127.1536063),
new kakao.maps.LatLng(37.5392702, 127.1576512),
new kakao.maps.LatLng(37.5411651, 127.1598933),
new kakao.maps.LatLng(37.5449999, 127.1631595),
new kakao.maps.LatLng(37.5442561, 127.1666417),
new kakao.maps.LatLng(37.5455346, 127.1721068),
new kakao.maps.LatLng(37.5452104, 127.1757181),
new kakao.maps.LatLng(37.5466816, 127.1793088),
new kakao.maps.LatLng(37.5463443, 127.1828251),
new kakao.maps.LatLng(37.5518204, 127.1829114),
new kakao.maps.LatLng(37.5528619, 127.1813807),
new kakao.maps.LatLng(37.5609928, 127.1819994),
new kakao.maps.LatLng(37.5654958, 127.179585),
new kakao.maps.LatLng(37.5689182, 127.1792158),
new kakao.maps.LatLng(37.5722139, 127.1777375),
new kakao.maps.LatLng(37.5740993, 127.17614),
new kakao.maps.LatLng(37.5783633, 127.1754421),
new kakao.maps.LatLng(37.5792655, 127.1768832),
new kakao.maps.LatLng(37.5812008, 127.1771547),
new kakao.maps.LatLng(37.5797349, 127.1738711),
new kakao.maps.LatLng(37.5786946, 127.1671595),
new kakao.maps.LatLng(37.5764649, 127.1629721),
new kakao.maps.LatLng(37.5704037, 127.1536011),
new kakao.maps.LatLng(37.5681865, 127.1493618),
new kakao.maps.LatLng(37.5682007, 127.138063),
new kakao.maps.LatLng(37.567884, 127.135692),
new kakao.maps.LatLng(37.565944, 127.1290179),
new kakao.maps.LatLng(37.5633331, 127.1234369),
new kakao.maps.LatLng(37.5592439, 127.1176932),
new kakao.maps.LatLng(37.5568724, 127.1153231),
new kakao.maps.LatLng(37.5543662, 127.1143095),
new kakao.maps.LatLng(37.5504987, 127.1115571),
new kakao.maps.LatLng(37.5469267, 127.1114708),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var gangdongPolygonB = new kakao.maps.Polygon({
    path: gangdongPolygonBPath,
    fillColor: '#E61E2B',
    fillOpacity: 0.5,
    strokeWeight: 1,
    strokeColor: '#E61E2B',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

                 // (22비율별) 용산구 다각형 생성
                 var yongsanPolygonCPath = [
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.54413326436179, 127.00898460651953),
            new kakao.maps.LatLng(37.539639030116945, 127.00959054834321),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.52290225898471, 127.00614038053493),
            new kakao.maps.LatLng(37.51309192794448, 126.99070240960813),
            new kakao.maps.LatLng(37.50654651085339, 126.98553683648308),
            new kakao.maps.LatLng(37.50702053393398, 126.97524914998174),
            new kakao.maps.LatLng(37.51751820477105, 126.94988506562748),
            new kakao.maps.LatLng(37.52702918583156, 126.94987870367682),
            new kakao.maps.LatLng(37.534519656862926, 126.94481851935942),
            new kakao.maps.LatLng(37.537500243531994, 126.95335659960566),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.5541513366375, 126.9657135934734),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994)
        ];

        var yongsanPolygonC = new kakao.maps.Polygon({
            path: yongsanPolygonCPath,
            fillColor: '#A61914',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#A61914',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        // 동대문구 다각형 생성(22비율)        
        var dongdaemunPolygonCPath = [
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496),
            new kakao.maps.LatLng(37.60107201319839, 127.07287376670605),
            new kakao.maps.LatLng(37.59724304056685, 127.06949105186925),
            new kakao.maps.LatLng(37.58953367466315, 127.07030363208528),
            new kakao.maps.LatLng(37.58651213184981, 127.07264218709383),
            new kakao.maps.LatLng(37.5849555116177, 127.07216063016078),
            new kakao.maps.LatLng(37.58026781100598, 127.07619547037923),
            new kakao.maps.LatLng(37.571869232268774, 127.0782018408153),
            new kakao.maps.LatLng(37.559961773835425, 127.07239004251258),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.572878529071055, 127.04263554582458),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.57838361223621, 127.0232348231103),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5956815721534, 127.04062845365279),
            new kakao.maps.LatLng(37.5969637344377, 127.04302522879048),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496)
        ];

        var dongdaemunPolygonC = new kakao.maps.Polygon({
            path: dongdaemunPolygonCPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#E85239',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성동구 다각형 생성(22비율)
        var seungdongPolygonCPath = [
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.5594131360664, 127.07373408220053),
            new kakao.maps.LatLng(37.52832388381049, 127.05621773388143),
            new kakao.maps.LatLng(37.53423885672233, 127.04604398310076),
            new kakao.maps.LatLng(37.53582328355087, 127.03979942567628),
            new kakao.maps.LatLng(37.53581367627865, 127.0211714455564),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53938672166098, 127.00993448922989),
            new kakao.maps.LatLng(37.54157804358092, 127.00879872996808),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706)
        ];

        var seungdongPolygonC = new kakao.maps.Polygon({
            path: seungdongPolygonCPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#E85239',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 서대문구 다각형 생성(22비율)
        var seodaemunPolygonCPath = [
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003),
            new kakao.maps.LatLng(37.5992407011344, 126.95499403097206),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.5575156365052, 126.95991288916548),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.57599550420081, 126.902091747923),
            new kakao.maps.LatLng(37.587223103650295, 126.91284666446226),
            new kakao.maps.LatLng(37.58541570520177, 126.91531241017965),
            new kakao.maps.LatLng(37.585870567159255, 126.91638068573187),
            new kakao.maps.LatLng(37.583095195853055, 126.9159399866114),
            new kakao.maps.LatLng(37.583459593417196, 126.92175886498167),
            new kakao.maps.LatLng(37.587104600730505, 126.92388813813815),
            new kakao.maps.LatLng(37.588386594820484, 126.92800815682232),
            new kakao.maps.LatLng(37.59157595859555, 126.92776504133688),
            new kakao.maps.LatLng(37.59455434247408, 126.93027139545339),
            new kakao.maps.LatLng(37.59869748704149, 126.94088480070904),
            new kakao.maps.LatLng(37.60065830191363, 126.9414041615336),
            new kakao.maps.LatLng(37.60305781086164, 126.93995273804141),
            new kakao.maps.LatLng(37.610598531321436, 126.95037536795142),
            new kakao.maps.LatLng(37.6083605525023, 126.95056259057313),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003)
        ];

        var seodaemunPolygonC = new kakao.maps.Polygon({
            path: seodaemunPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 종로구 다각형 생성(22비율)
        var jongnoPolygonCPath = [
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046),
            new kakao.maps.LatLng(37.632194205253654, 126.97609588529602),
            new kakao.maps.LatLng(37.629026103322374, 126.97496405167149),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.60401657024552, 126.98665951539246),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.5788668917658, 127.02140099081309),
            new kakao.maps.LatLng(37.578034045208426, 127.02313962015988),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.5681357695346, 126.99014772014593),
            new kakao.maps.LatLng(37.569315246023024, 126.9732046364419),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.59875701675023, 126.95306020161668),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.60912809443569, 126.95032198271032),
            new kakao.maps.LatLng(37.615539700280216, 126.95072546923387),
            new kakao.maps.LatLng(37.62433621196653, 126.94900237336302),
            new kakao.maps.LatLng(37.62642708817027, 126.95037844036497),
            new kakao.maps.LatLng(37.629590994617104, 126.95881385457929),
            new kakao.maps.LatLng(37.629794440379136, 126.96376660599225),
            new kakao.maps.LatLng(37.632373740990175, 126.97302793692637),
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046)
        ];

        var jongnoPolygonC = new kakao.maps.Polygon({
            path: jongnoPolygonCPath,
            fillColor: '#F18077',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#F18077',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중구 다각형 생성(22비율)
        var jungPolygonCPath = [
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55487749311664, 126.97240854546743),
            new kakao.maps.LatLng(37.5548766923893, 126.9691718124876),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.55498984534305, 126.96173858545431),
            new kakao.maps.LatLng(37.55695455613004, 126.96343068837372),
            new kakao.maps.LatLng(37.5590262922649, 126.9616731414449),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.569485309984174, 126.97637402412326),
            new kakao.maps.LatLng(37.56810323716611, 126.98905202099309),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.572022763755164, 127.0223363152772),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56973041414113, 127.0234585247501),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894)
        ];

        var jungPolygonC = new kakao.maps.Polygon({
            path: jungPolygonCPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#E85239',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 광진구 다각형 생성(22비율)
        var gwangjinPolygonCPath = [
    new kakao.maps.LatLng(37.5568724, 127.1153231),
    new kakao.maps.LatLng(37.5585233, 127.113965),
    new kakao.maps.LatLng(37.5590006, 127.112297),
    new kakao.maps.LatLng(37.5585538, 127.1095286),
    new kakao.maps.LatLng(37.5564601, 127.1063932),
    new kakao.maps.LatLng(37.5595269, 127.1019134),
    new kakao.maps.LatLng(37.5616054, 127.1012509),
    new kakao.maps.LatLng(37.5643129, 127.1023143),
    new kakao.maps.LatLng(37.5701103, 127.1035059),
    new kakao.maps.LatLng(37.5714514, 127.104295),
    new kakao.maps.LatLng(37.5724694, 127.1017021),
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.5679178, 127.0768757),
    new kakao.maps.LatLng(37.5645904, 127.0740989),
    new kakao.maps.LatLng(37.5599603, 127.0723852),
    new kakao.maps.LatLng(37.559414, 127.0737358),
    new kakao.maps.LatLng(37.5393084, 127.0623676),
    new kakao.maps.LatLng(37.539291, 127.0623585),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5268818, 127.0607945),
    new kakao.maps.LatLng(37.523872, 127.0686631),
    new kakao.maps.LatLng(37.522514, 127.0769544),
    new kakao.maps.LatLng(37.5229485, 127.0799746),
    new kakao.maps.LatLng(37.524759, 127.0856328),
    new kakao.maps.LatLng(37.5270069, 127.090161),
    new kakao.maps.LatLng(37.5414079, 127.1082818),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5469267, 127.1114708),
    new kakao.maps.LatLng(37.5504987, 127.1115571),
    new kakao.maps.LatLng(37.5543662, 127.1143095),
    new kakao.maps.LatLng(37.5568724, 127.1153231)
];  
        var gwangjinPolygonC = new kakao.maps.Polygon({
            path: gwangjinPolygonCPath,
            fillColor: '#F18077',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#F18077',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중랑구 다각형 생성(22비율)
        var jungnangPolygonCPath = [
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.5760708, 127.1011435),
    new kakao.maps.LatLng(37.578907, 127.1030254),
    new kakao.maps.LatLng(37.5805343, 127.103429),
    new kakao.maps.LatLng(37.5833044, 127.109002),
    new kakao.maps.LatLng(37.5891647, 127.1106433),
    new kakao.maps.LatLng(37.5932091, 127.1131972),
    new kakao.maps.LatLng(37.5940164, 127.1166645),
    new kakao.maps.LatLng(37.5954971, 127.1168775),
    new kakao.maps.LatLng(37.599521, 127.1140639),
    new kakao.maps.LatLng(37.6021085, 127.1157227),
    new kakao.maps.LatLng(37.6046024, 127.118047),
    new kakao.maps.LatLng(37.607613, 127.1184769),
    new kakao.maps.LatLng(37.6088335, 127.1166833),
    new kakao.maps.LatLng(37.6118276, 127.1174901),
    new kakao.maps.LatLng(37.6160155, 127.1166717),
    new kakao.maps.LatLng(37.6178884, 127.1171467),
    new kakao.maps.LatLng(37.6195377, 127.115021),
    new kakao.maps.LatLng(37.6210546, 127.110519),
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6153366, 127.0701774),
    new kakao.maps.LatLng(37.6153196, 127.0702079),
    new kakao.maps.LatLng(37.6135142, 127.0717529),
    new kakao.maps.LatLng(37.6070224, 127.0711169),
    new kakao.maps.LatLng(37.6046424, 127.0715334),
    new kakao.maps.LatLng(37.6013304, 127.0728729),
    new kakao.maps.LatLng(37.600246, 127.0724977),
    new kakao.maps.LatLng(37.5972431, 127.069494),
    new kakao.maps.LatLng(37.5951242, 127.0694344),
    new kakao.maps.LatLng(37.5919078, 127.0707184),
    new kakao.maps.LatLng(37.5899586, 127.070228),
    new kakao.maps.LatLng(37.5865116, 127.0726438),
    new kakao.maps.LatLng(37.5849569, 127.0721613),
    new kakao.maps.LatLng(37.5793357, 127.076458),
    new kakao.maps.LatLng(37.5729206, 127.0772314),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5737318, 127.1008637)
];

        var jungnangPolygonC = new kakao.maps.Polygon({
            path: jungnangPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성북구 다각형 생성(22비율)
        var seongbukPolygonCPath = [
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235),
            new kakao.maps.LatLng(37.631446839436855, 126.99372381657889),
            new kakao.maps.LatLng(37.626192451322005, 126.99927047335905),
            new kakao.maps.LatLng(37.62382095469671, 127.00488450145781),
            new kakao.maps.LatLng(37.624026217174986, 127.00788862747375),
            new kakao.maps.LatLng(37.6205124078061, 127.00724034082933),
            new kakao.maps.LatLng(37.61679651952433, 127.01014412786792),
            new kakao.maps.LatLng(37.61472018601129, 127.01451127202589),
            new kakao.maps.LatLng(37.614629670135216, 127.01757841621624),
            new kakao.maps.LatLng(37.61137091590441, 127.02219857751122),
            new kakao.maps.LatLng(37.612692696824915, 127.02642583551054),
            new kakao.maps.LatLng(37.612367438936786, 127.03018593770908),
            new kakao.maps.LatLng(37.60896889076571, 127.0302525167858),
            new kakao.maps.LatLng(37.61279787695882, 127.03730791358603),
            new kakao.maps.LatLng(37.62426467261789, 127.04973339977498),
            new kakao.maps.LatLng(37.61449950127667, 127.06174181124696),
            new kakao.maps.LatLng(37.61561580859776, 127.06985247014711),
            new kakao.maps.LatLng(37.61351359068103, 127.07170798866412),
            new kakao.maps.LatLng(37.60762512162974, 127.07105453180604),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.59644879095525, 127.04184728392097),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.57782865303167, 127.02296295333255),
            new kakao.maps.LatLng(37.57889204835333, 127.02179043639809),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.60451393107786, 126.98678626394351),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.62980449548538, 126.97468284124939),
            new kakao.maps.LatLng(37.633657663246694, 126.97740053878216),
            new kakao.maps.LatLng(37.63476479485093, 126.98154674721893),
            new kakao.maps.LatLng(37.63780700422825, 126.9849494717052),
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235)
        ];

        var seongbukPolygonC = new kakao.maps.Polygon({
            path: seongbukPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강북구 다각형 생성(22비율)
        var gangbukPolygonCPath = [
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6850889, 127.0045265),
    new kakao.maps.LatLng(37.6834224, 126.9973582),
    new kakao.maps.LatLng(37.678828, 126.9929755),
    new kakao.maps.LatLng(37.6757199, 126.9931995),
    new kakao.maps.LatLng(37.672422, 126.9942076),
    new kakao.maps.LatLng(37.6678322, 126.993576),
    new kakao.maps.LatLng(37.6670301, 126.9941291),
    new kakao.maps.LatLng(37.6652317, 126.9922245),
    new kakao.maps.LatLng(37.6643912, 126.9882682),
    new kakao.maps.LatLng(37.6606003, 126.9872768),
    new kakao.maps.LatLng(37.6589432, 126.9860205),
    new kakao.maps.LatLng(37.6570035, 126.9830101),
    new kakao.maps.LatLng(37.6560387, 126.9796581),
    new kakao.maps.LatLng(37.6548152, 126.9799441),
    new kakao.maps.LatLng(37.6505404, 126.9824953),
    new kakao.maps.LatLng(37.64961, 126.9839369),
    new kakao.maps.LatLng(37.6457101, 126.9850955),
    new kakao.maps.LatLng(37.6436716, 126.9832554),
    new kakao.maps.LatLng(37.6400446, 126.9856762),
    new kakao.maps.LatLng(37.6363484, 126.9841726),
    new kakao.maps.LatLng(37.6340757, 126.9894095),
    new kakao.maps.LatLng(37.6302496, 126.9953935),
    new kakao.maps.LatLng(37.6262023, 126.999273),
    new kakao.maps.LatLng(37.625951, 127.0000402),
    new kakao.maps.LatLng(37.6259335, 127.0000628),
    new kakao.maps.LatLng(37.6242258, 127.0038971),
    new kakao.maps.LatLng(37.6240272, 127.0078883),
    new kakao.maps.LatLng(37.6208272, 127.0072158),
    new kakao.maps.LatLng(37.618622, 127.0085),
    new kakao.maps.LatLng(37.6162859, 127.0109519),
    new kakao.maps.LatLng(37.6146854, 127.0144744),
    new kakao.maps.LatLng(37.6146161, 127.0175368),
    new kakao.maps.LatLng(37.6113717, 127.0221965),
    new kakao.maps.LatLng(37.6126938, 127.0264334),
    new kakao.maps.LatLng(37.6123662, 127.0301844),
    new kakao.maps.LatLng(37.6089762, 127.0302524),
    new kakao.maps.LatLng(37.6129618, 127.0375131),
    new kakao.maps.LatLng(37.6157606, 127.0399847),
    new kakao.maps.LatLng(37.6186436, 127.0439485),
    new kakao.maps.LatLng(37.6226012, 127.0468685),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6843696, 127.0086619)
];

        var gangbukPolygonC = new kakao.maps.Polygon({
            path: gangbukPolygonCPath,
            fillColor: '#0074BD',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#0074BD',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 도봉구 다각형 생성(22비율)
        var dobongPolygonCPath = [
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6879759, 127.0498208),
    new kakao.maps.LatLng(37.6908702, 127.0499658),
    new kakao.maps.LatLng(37.6940664, 127.0486327),
    new kakao.maps.LatLng(37.6923802, 127.0456492),
    new kakao.maps.LatLng(37.693687, 127.043083),
    new kakao.maps.LatLng(37.6952354, 127.0430909),
    new kakao.maps.LatLng(37.6952919, 127.0411383),
    new kakao.maps.LatLng(37.6926381, 127.0368093),
    new kakao.maps.LatLng(37.6918448, 127.0324625),
    new kakao.maps.LatLng(37.6930733, 127.0310969),
    new kakao.maps.LatLng(37.6962653, 127.0297701),
    new kakao.maps.LatLng(37.6992843, 127.0293125),
    new kakao.maps.LatLng(37.7009462, 127.02771),
    new kakao.maps.LatLng(37.6995947, 127.0253836),
    new kakao.maps.LatLng(37.6997207, 127.0221482),
    new kakao.maps.LatLng(37.7010174, 127.0198271),
    new kakao.maps.LatLng(37.7014553, 127.0154151),
    new kakao.maps.LatLng(37.6988007, 127.0138784),
    new kakao.maps.LatLng(37.6973775, 127.0121243),
    new kakao.maps.LatLng(37.6966991, 127.0096662),
    new kakao.maps.LatLng(37.6933154, 127.0097568),
    new kakao.maps.LatLng(37.6915772, 127.007678),
    new kakao.maps.LatLng(37.6900533, 127.0083369),
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6858137, 127.0518033)
];

        var dobongPolygonC = new kakao.maps.Polygon({
            path: dobongPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 노원구 다각형 생성(22비율)
        var nowonPolygonCPath = [
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6216472, 127.1040704),
    new kakao.maps.LatLng(37.6275838, 127.1059087),
    new kakao.maps.LatLng(37.6293016, 127.1088847),
    new kakao.maps.LatLng(37.6315033, 127.1116324),
    new kakao.maps.LatLng(37.6326429, 127.1122035),
    new kakao.maps.LatLng(37.6364891, 127.1124833),
    new kakao.maps.LatLng(37.6391262, 127.1105493),
    new kakao.maps.LatLng(37.6398412, 127.1120504),
    new kakao.maps.LatLng(37.6425246, 127.1108099),
    new kakao.maps.LatLng(37.6426948, 127.1093228),
    new kakao.maps.LatLng(37.6451721, 127.1067673),
    new kakao.maps.LatLng(37.6452258, 127.1028086),
    new kakao.maps.LatLng(37.6439649, 127.0975589),
    new kakao.maps.LatLng(37.6445705, 127.09457),
    new kakao.maps.LatLng(37.6496973, 127.0924745),
    new kakao.maps.LatLng(37.6524386, 127.0940495),
    new kakao.maps.LatLng(37.6537758, 127.0930673),
    new kakao.maps.LatLng(37.6593346, 127.0912069),
    new kakao.maps.LatLng(37.6632988, 127.0941422),
    new kakao.maps.LatLng(37.6675788, 127.095017),
    new kakao.maps.LatLng(37.6687685, 127.0962455),
    new kakao.maps.LatLng(37.6727011, 127.0957715),
    new kakao.maps.LatLng(37.673564, 127.0946559),
    new kakao.maps.LatLng(37.6767064, 127.0938558),
    new kakao.maps.LatLng(37.6786397, 127.0919859),
    new kakao.maps.LatLng(37.6814411, 127.0929524),
    new kakao.maps.LatLng(37.6855375, 127.0964162),
    new kakao.maps.LatLng(37.689071, 127.095996),
    new kakao.maps.LatLng(37.6899664, 127.0930367),
    new kakao.maps.LatLng(37.6895704, 127.0905519),
    new kakao.maps.LatLng(37.6899122, 127.0865306),
    new kakao.maps.LatLng(37.6917823, 127.083905),
    new kakao.maps.LatLng(37.694269, 127.0838433),
    new kakao.maps.LatLng(37.6961376, 127.0811047),
    new kakao.maps.LatLng(37.6959864, 127.0781963),
    new kakao.maps.LatLng(37.6951465, 127.0748951),
    new kakao.maps.LatLng(37.6937786, 127.0727908),
    new kakao.maps.LatLng(37.6939832, 127.0686396),
    new kakao.maps.LatLng(37.6949371, 127.0634232),
    new kakao.maps.LatLng(37.6930035, 127.0624128),
    new kakao.maps.LatLng(37.6902838, 127.0597139),
    new kakao.maps.LatLng(37.6892048, 127.0551791),
    new kakao.maps.LatLng(37.6870667, 127.0518042),
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6197959, 127.0544081),
    new kakao.maps.LatLng(37.6174813, 127.0574206),
    new kakao.maps.LatLng(37.6142587, 127.0632852),
    new kakao.maps.LatLng(37.6157243, 127.0697122),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.6203794, 127.105654)
];

        var nowonPolygonC = new kakao.maps.Polygon({
            path: nowonPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 은평구 다각형 생성(22비율)
        var eunpyeongPolygonCPath = [
    new kakao.maps.LatLng(37.6295893, 126.9588137),
    new kakao.maps.LatLng(37.62973, 126.9597977),
    new kakao.maps.LatLng(37.6332338, 126.9634013),
    new kakao.maps.LatLng(37.6357828, 126.9626334),
    new kakao.maps.LatLng(37.6421387, 126.9593275),
    new kakao.maps.LatLng(37.6467834, 126.959027),
    new kakao.maps.LatLng(37.6480477, 126.9578392),
    new kakao.maps.LatLng(37.6528372, 126.9571078),
    new kakao.maps.LatLng(37.6546009, 126.9543453),
    new kakao.maps.LatLng(37.6549496, 126.9513757),
    new kakao.maps.LatLng(37.6571298, 126.9478961),
    new kakao.maps.LatLng(37.6592154, 126.9475649),
    new kakao.maps.LatLng(37.6577222, 126.9421),
    new kakao.maps.LatLng(37.6566359, 126.9401282),
    new kakao.maps.LatLng(37.6523011, 126.9371587),
    new kakao.maps.LatLng(37.6511999, 126.9357024),
    new kakao.maps.LatLng(37.6500481, 126.9296991),
    new kakao.maps.LatLng(37.6461063, 126.9241229),
    new kakao.maps.LatLng(37.6447557, 126.9137208),
    new kakao.maps.LatLng(37.6476455, 126.9095352),
    new kakao.maps.LatLng(37.6486884, 126.905964),
    new kakao.maps.LatLng(37.6462898, 126.9077049),
    new kakao.maps.LatLng(37.6442586, 126.9122604),
    new kakao.maps.LatLng(37.6385095, 126.9100918),
    new kakao.maps.LatLng(37.6353165, 126.9108542),
    new kakao.maps.LatLng(37.633398, 126.9070962),
    new kakao.maps.LatLng(37.6308672, 126.9072938),
    new kakao.maps.LatLng(37.6293276, 126.9087697),
    new kakao.maps.LatLng(37.6262657, 126.9086108),
    new kakao.maps.LatLng(37.6244956, 126.9066268),
    new kakao.maps.LatLng(37.6219415, 126.9071175),
    new kakao.maps.LatLng(37.6207039, 126.9056125),
    new kakao.maps.LatLng(37.6190745, 126.9052311),
    new kakao.maps.LatLng(37.6188394, 126.903361),
    new kakao.maps.LatLng(37.6157535, 126.9018223),
    new kakao.maps.LatLng(37.6140692, 126.9017342),
    new kakao.maps.LatLng(37.6111913, 126.9003043),
    new kakao.maps.LatLng(37.6037417, 126.9021083),
    new kakao.maps.LatLng(37.6020402, 126.8999819),
    new kakao.maps.LatLng(37.5993665, 126.9013224),
    new kakao.maps.LatLng(37.5973371, 126.9010115),
    new kakao.maps.LatLng(37.5951135, 126.9018381),
    new kakao.maps.LatLng(37.5926784, 126.8989613),
    new kakao.maps.LatLng(37.589938, 126.8997501),
    new kakao.maps.LatLng(37.5885666, 126.896859),
    new kakao.maps.LatLng(37.5890755, 126.8932905),
    new kakao.maps.LatLng(37.5885221, 126.8922355),
    new kakao.maps.LatLng(37.5885328, 126.8871589),
    new kakao.maps.LatLng(37.5895376, 126.8858088),
    new kakao.maps.LatLng(37.593639, 126.885004),
    new kakao.maps.LatLng(37.5907926, 126.8820561),
    new kakao.maps.LatLng(37.5907588, 126.882095),
    new kakao.maps.LatLng(37.588347, 126.8845533),
    new kakao.maps.LatLng(37.5876412, 126.8852568),
    new kakao.maps.LatLng(37.5870924, 126.8858291),
    new kakao.maps.LatLng(37.5860266, 126.8871243),
    new kakao.maps.LatLng(37.5858059, 126.8874045),
    new kakao.maps.LatLng(37.5815606, 126.8937787),
    new kakao.maps.LatLng(37.5794888, 126.8969354),
    new kakao.maps.LatLng(37.5782229, 126.898808),
    new kakao.maps.LatLng(37.5765458, 126.901833),
    new kakao.maps.LatLng(37.5787907, 126.9044431),
    new kakao.maps.LatLng(37.5803263, 126.9060741),
    new kakao.maps.LatLng(37.58547, 126.9115429),
    new kakao.maps.LatLng(37.5865298, 126.9124768),
    new kakao.maps.LatLng(37.5868917, 126.9126854),
    new kakao.maps.LatLng(37.5870633, 126.9127725),
    new kakao.maps.LatLng(37.5862014, 126.9151912),
    new kakao.maps.LatLng(37.5860447, 126.9155519),
    new kakao.maps.LatLng(37.5853667, 126.9160692),
    new kakao.maps.LatLng(37.5853601, 126.9160646),
    new kakao.maps.LatLng(37.5843543, 126.9156798),
    new kakao.maps.LatLng(37.5837821, 126.9157485),
    new kakao.maps.LatLng(37.5831718, 126.9164206),
    new kakao.maps.LatLng(37.58325, 126.9178162),
    new kakao.maps.LatLng(37.5829392, 126.920859),
    new kakao.maps.LatLng(37.5838591, 126.9218276),
    new kakao.maps.LatLng(37.5846767, 126.9218555),
    new kakao.maps.LatLng(37.5852834, 126.9223929),
    new kakao.maps.LatLng(37.5856304, 126.9228635),
    new kakao.maps.LatLng(37.5869714, 126.923861),
    new kakao.maps.LatLng(37.5871207, 126.9240038),
    new kakao.maps.LatLng(37.5872166, 126.9246107),
    new kakao.maps.LatLng(37.5872168, 126.9252644),
    new kakao.maps.LatLng(37.5883854, 126.928009),
    new kakao.maps.LatLng(37.5911032, 126.927947),
    new kakao.maps.LatLng(37.5915762, 126.9277682),
    new kakao.maps.LatLng(37.5945528, 126.9302704),
    new kakao.maps.LatLng(37.5962984, 126.9327954),
    new kakao.maps.LatLng(37.5974786, 126.9364086),
    new kakao.maps.LatLng(37.5976207, 126.9382703),
    new kakao.maps.LatLng(37.5987329, 126.9408662),
    new kakao.maps.LatLng(37.6006774, 126.9413766),
    new kakao.maps.LatLng(37.6013511, 126.9407255),
    new kakao.maps.LatLng(37.6049576, 126.9421378),
    new kakao.maps.LatLng(37.6086085, 126.9482139),
    new kakao.maps.LatLng(37.609399, 126.9489364),
    new kakao.maps.LatLng(37.6138494, 126.9507966),
    new kakao.maps.LatLng(37.6155379, 126.9507242),
    new kakao.maps.LatLng(37.6199205, 126.9499112),
    new kakao.maps.LatLng(37.6207316, 126.9499381),
    new kakao.maps.LatLng(37.6209324, 126.9499158),
    new kakao.maps.LatLng(37.6232616, 126.9488984),
    new kakao.maps.LatLng(37.626418, 126.9504537),
    new kakao.maps.LatLng(37.6265452, 126.9516053),
    new kakao.maps.LatLng(37.628731, 126.956889),
    new kakao.maps.LatLng(37.6295893, 126.9588137)
];

        var eunpyeongPolygonC = new kakao.maps.Polygon({
            path: eunpyeongPolygonCPath,
            fillColor: '#0074BD',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#0074BD',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 마포구 다각형 생성(22비율)
        var mapoPolygonCPath = [
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.55675317809392, 126.93190919632814),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.557241466445234, 126.95913438471307),
            new kakao.maps.LatLng(37.55908394430372, 126.96163689468189),
            new kakao.maps.LatLng(37.55820141918588, 126.96305432966605),
            new kakao.maps.LatLng(37.554784413504734, 126.9617251098019),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.539468942052544, 126.955731506394),
            new kakao.maps.LatLng(37.536292068277106, 126.95128907260018),
            new kakao.maps.LatLng(37.53569162926515, 126.94627494388307),
            new kakao.maps.LatLng(37.53377712226906, 126.94458373402794),
            new kakao.maps.LatLng(37.54135238063506, 126.93031191951576),
            new kakao.maps.LatLng(37.539036674424615, 126.9271006565075),
            new kakao.maps.LatLng(37.54143034750605, 126.9224138272872),
            new kakao.maps.LatLng(37.54141748538761, 126.90483000187002),
            new kakao.maps.LatLng(37.548015078285694, 126.89890097452322),
            new kakao.maps.LatLng(37.56300401736817, 126.86623824787709),
            new kakao.maps.LatLng(37.57178997971358, 126.85363039091744),
            new kakao.maps.LatLng(37.57379738998644, 126.85362646212587),
            new kakao.maps.LatLng(37.57747251471329, 126.864939928088),
            new kakao.maps.LatLng(37.5781913017327, 126.87625939970273),
            new kakao.maps.LatLng(37.57977132158497, 126.87767870371688),
            new kakao.maps.LatLng(37.584440882833654, 126.87653889183002),
            new kakao.maps.LatLng(37.59079311146897, 126.88205386700724),
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884)
        ];

        var mapoPolygonC = new kakao.maps.Polygon({
            path: mapoPolygonCPath,
            fillColor: '#F18077',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#F18077',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 양천구 다각형 생성(22비율)
        var yangcheonPolygonCPath = [
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5397562, 126.8216026),
    new kakao.maps.LatLng(37.5365431, 126.8224338),
    new kakao.maps.LatLng(37.5348887, 126.821878),
    new kakao.maps.LatLng(37.5299154, 126.8254181),
    new kakao.maps.LatLng(37.528389, 126.8279799),
    new kakao.maps.LatLng(37.5258342, 126.8281793),
    new kakao.maps.LatLng(37.5249238, 126.8264622),
    new kakao.maps.LatLng(37.5230079, 126.8251384),
    new kakao.maps.LatLng(37.5198753, 126.8255944),
    new kakao.maps.LatLng(37.516186, 126.8231123),
    new kakao.maps.LatLng(37.5130434, 126.8244262),
    new kakao.maps.LatLng(37.5090953, 126.8239041),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5187577, 126.8782517),
    new kakao.maps.LatLng(37.5203627, 126.879464),
    new kakao.maps.LatLng(37.5252536, 126.878749),
    new kakao.maps.LatLng(37.5259082, 126.8809399),
    new kakao.maps.LatLng(37.5287593, 126.8843314),
    new kakao.maps.LatLng(37.5301503, 126.8871006),
    new kakao.maps.LatLng(37.5301524, 126.8896671),
    new kakao.maps.LatLng(37.5319258, 126.8890681),
    new kakao.maps.LatLng(37.5351351, 126.8897886),
    new kakao.maps.LatLng(37.5397825, 126.8863138),
    new kakao.maps.LatLng(37.543321, 126.885088),
    new kakao.maps.LatLng(37.5481962, 126.880664),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.546944, 126.8745052)
];

        var yangcheonPolygonC = new kakao.maps.Polygon({
            path: yangcheonPolygonCPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#E85239',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강서구 다각형 생성(22비율)
        var gangseoPolygonCPath = [
    new kakao.maps.LatLng(37.5717904, 126.8536316),
    new kakao.maps.LatLng(37.5737991, 126.8536283),
    new kakao.maps.LatLng(37.5745142, 126.8510083),
    new kakao.maps.LatLng(37.5773942, 126.8467014),
    new kakao.maps.LatLng(37.5835872, 126.8327892),
    new kakao.maps.LatLng(37.588201, 126.8270511),
    new kakao.maps.LatLng(37.5900825, 126.8252892),
    new kakao.maps.LatLng(37.5912976, 126.822785),
    new kakao.maps.LatLng(37.5976193, 126.8139529),
    new kakao.maps.LatLng(37.5989607, 126.8113687),
    new kakao.maps.LatLng(37.604902, 126.8027567),
    new kakao.maps.LatLng(37.6024867, 126.7999484),
    new kakao.maps.LatLng(37.6013474, 126.7998667),
    new kakao.maps.LatLng(37.5998709, 126.7978909),
    new kakao.maps.LatLng(37.597712, 126.797114),
    new kakao.maps.LatLng(37.5947537, 126.797721),
    new kakao.maps.LatLng(37.5936525, 126.798726),
    new kakao.maps.LatLng(37.5913058, 126.7988344),
    new kakao.maps.LatLng(37.589326, 126.8012524),
    new kakao.maps.LatLng(37.5878099, 126.8007605),
    new kakao.maps.LatLng(37.5880729, 126.7987679),
    new kakao.maps.LatLng(37.583364, 126.7956796),
    new kakao.maps.LatLng(37.5797103, 126.7924063),
    new kakao.maps.LatLng(37.5805208, 126.7907535),
    new kakao.maps.LatLng(37.5777706, 126.790599),
    new kakao.maps.LatLng(37.5777198, 126.7893694),
    new kakao.maps.LatLng(37.5755709, 126.787642),
    new kakao.maps.LatLng(37.5735993, 126.7824424),
    new kakao.maps.LatLng(37.5692071, 126.7816643),
    new kakao.maps.LatLng(37.5672821, 126.7789707),
    new kakao.maps.LatLng(37.5670966, 126.776366),
    new kakao.maps.LatLng(37.5658733, 126.7751607),
    new kakao.maps.LatLng(37.5637152, 126.7771261),
    new kakao.maps.LatLng(37.5618635, 126.7761087),
    new kakao.maps.LatLng(37.5572273, 126.7698955),
    new kakao.maps.LatLng(37.5554503, 126.7645763),
    new kakao.maps.LatLng(37.5539545, 126.7676412),
    new kakao.maps.LatLng(37.551962, 126.7674713),
    new kakao.maps.LatLng(37.5515813, 126.7693259),
    new kakao.maps.LatLng(37.548316, 126.7717031),
    new kakao.maps.LatLng(37.5489742, 126.7752973),
    new kakao.maps.LatLng(37.54671, 126.7775751),
    new kakao.maps.LatLng(37.5460749, 126.7818371),
    new kakao.maps.LatLng(37.545997, 126.7869552),
    new kakao.maps.LatLng(37.5438485, 126.7907616),
    new kakao.maps.LatLng(37.541761, 126.7921302),
    new kakao.maps.LatLng(37.541372, 126.7949442),
    new kakao.maps.LatLng(37.5395572, 126.7938932),
    new kakao.maps.LatLng(37.5373674, 126.7939734),
    new kakao.maps.LatLng(37.5367714, 126.7961149),
    new kakao.maps.LatLng(37.5378446, 126.7994886),
    new kakao.maps.LatLng(37.5403453, 126.7988931),
    new kakao.maps.LatLng(37.5408808, 126.8008976),
    new kakao.maps.LatLng(37.5426716, 126.8016672),
    new kakao.maps.LatLng(37.5436059, 126.8068721),
    new kakao.maps.LatLng(37.5407765, 126.8125684),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5484626, 126.8804437),
    new kakao.maps.LatLng(37.5494053, 126.8798959),
    new kakao.maps.LatLng(37.5497628, 126.8796001),
    new kakao.maps.LatLng(37.5499377, 126.8794778),
    new kakao.maps.LatLng(37.5500282, 126.8794146),
    new kakao.maps.LatLng(37.550412, 126.8791236),
    new kakao.maps.LatLng(37.5507488, 126.8788459),
    new kakao.maps.LatLng(37.5511263, 126.8787108),
    new kakao.maps.LatLng(37.5515205, 126.8781985),
    new kakao.maps.LatLng(37.5519352, 126.8780413),
    new kakao.maps.LatLng(37.5523189, 126.8780313),
    new kakao.maps.LatLng(37.5525651, 126.8780226),
    new kakao.maps.LatLng(37.5527979, 126.8780142),
    new kakao.maps.LatLng(37.5529934, 126.8780067),
    new kakao.maps.LatLng(37.5531701, 126.8779519),
    new kakao.maps.LatLng(37.5532133, 126.8779456),
    new kakao.maps.LatLng(37.5534501, 126.8779539),
    new kakao.maps.LatLng(37.5535245, 126.8780551),
    new kakao.maps.LatLng(37.553546, 126.8781144),
    new kakao.maps.LatLng(37.5535815, 126.8782443),
    new kakao.maps.LatLng(37.5533372, 126.878835),
    new kakao.maps.LatLng(37.5532765, 126.8789601),
    new kakao.maps.LatLng(37.5531512, 126.8792171),
    new kakao.maps.LatLng(37.5537026, 126.879224),
    new kakao.maps.LatLng(37.554747, 126.879237),
    new kakao.maps.LatLng(37.5550643, 126.8794927),
    new kakao.maps.LatLng(37.555305, 126.879688),
    new kakao.maps.LatLng(37.556224, 126.8804278),
    new kakao.maps.LatLng(37.5562828, 126.8804743),
    new kakao.maps.LatLng(37.5565904, 126.8798677),
    new kakao.maps.LatLng(37.5566999, 126.8796536),
    new kakao.maps.LatLng(37.5569932, 126.8790797),
    new kakao.maps.LatLng(37.5571835, 126.8787108),
    new kakao.maps.LatLng(37.5577477, 126.8776168),
    new kakao.maps.LatLng(37.5580956, 126.8769422),
    new kakao.maps.LatLng(37.5582839, 126.8765751),
    new kakao.maps.LatLng(37.5589502, 126.8752775),
    new kakao.maps.LatLng(37.5591563, 126.8748767),
    new kakao.maps.LatLng(37.5595945, 126.874025),
    new kakao.maps.LatLng(37.5596946, 126.8738248),
    new kakao.maps.LatLng(37.5601596, 126.8728588),
    new kakao.maps.LatLng(37.5605276, 126.8720972),
    new kakao.maps.LatLng(37.5609333, 126.8712519),
    new kakao.maps.LatLng(37.5615358, 126.8699951),
    new kakao.maps.LatLng(37.5619632, 126.8691064),
    new kakao.maps.LatLng(37.5621959, 126.868634),
    new kakao.maps.LatLng(37.5627029, 126.8677403),
    new kakao.maps.LatLng(37.5629894, 126.8672261),
    new kakao.maps.LatLng(37.5632825, 126.8666958),
    new kakao.maps.LatLng(37.5637559, 126.8658888),
    new kakao.maps.LatLng(37.5640521, 126.8654083),
    new kakao.maps.LatLng(37.5644624, 126.8647347),
    new kakao.maps.LatLng(37.5647185, 126.8643124),
    new kakao.maps.LatLng(37.5649731, 126.8639165),
    new kakao.maps.LatLng(37.5650512, 126.8637912),
    new kakao.maps.LatLng(37.5652642, 126.8634888),
    new kakao.maps.LatLng(37.5653859, 126.8633098),
    new kakao.maps.LatLng(37.5654471, 126.8632313),
    new kakao.maps.LatLng(37.5655495, 126.8630904),
    new kakao.maps.LatLng(37.5657186, 126.8628754),
    new kakao.maps.LatLng(37.5660443, 126.8624873),
    new kakao.maps.LatLng(37.5663031, 126.8621474),
    new kakao.maps.LatLng(37.5663376, 126.8621034),
    new kakao.maps.LatLng(37.5664484, 126.8619718),
    new kakao.maps.LatLng(37.5667462, 126.861637),
    new kakao.maps.LatLng(37.5672618, 126.8610683),
    new kakao.maps.LatLng(37.5675217, 126.8607424),
    new kakao.maps.LatLng(37.5676648, 126.8605839),
    new kakao.maps.LatLng(37.5679501, 126.8602879),
    new kakao.maps.LatLng(37.5682635, 126.8599471),
    new kakao.maps.LatLng(37.5686039, 126.8595982),
    new kakao.maps.LatLng(37.5688681, 126.8592962),
    new kakao.maps.LatLng(37.5693278, 126.8588345),
    new kakao.maps.LatLng(37.5695699, 126.8585727),
    new kakao.maps.LatLng(37.5700741, 126.8580604),
    new kakao.maps.LatLng(37.5702804, 126.8578288),
    new kakao.maps.LatLng(37.5704464, 126.8576497),
    new kakao.maps.LatLng(37.5705987, 126.8574919),
    new kakao.maps.LatLng(37.5708578, 126.8572342),
    new kakao.maps.LatLng(37.5710034, 126.8571121),
    new kakao.maps.LatLng(37.5712288, 126.8569134),
    new kakao.maps.LatLng(37.5715422, 126.8566245),
    new kakao.maps.LatLng(37.5717665, 126.8564237),
    new kakao.maps.LatLng(37.5717904, 126.8536316)
];

        var gangseoPolygonC = new kakao.maps.Polygon({
            path: gangseoPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 구로구 다각형 생성(22비율)
        var guroPolygonCPath = [
    new kakao.maps.LatLng(37.4849988, 126.9031946),
    new kakao.maps.LatLng(37.4869351, 126.8981442),
    new kakao.maps.LatLng(37.4893387, 126.896124),
    new kakao.maps.LatLng(37.5033326, 126.8926737),
    new kakao.maps.LatLng(37.5050117, 126.8939767),
    new kakao.maps.LatLng(37.5103503, 126.8917119),
    new kakao.maps.LatLng(37.5132264, 126.8875197),
    new kakao.maps.LatLng(37.5138494, 126.8844331),
    new kakao.maps.LatLng(37.5164199, 126.881729),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5076346, 126.8222152),
    new kakao.maps.LatLng(37.5056852, 126.8225503),
    new kakao.maps.LatLng(37.5022364, 126.821611),
    new kakao.maps.LatLng(37.5006401, 126.8194028),
    new kakao.maps.LatLng(37.4993555, 126.8196714),
    new kakao.maps.LatLng(37.4977435, 126.8161301),
    new kakao.maps.LatLng(37.4982134, 126.8141214),
    new kakao.maps.LatLng(37.4964818, 126.8129811),
    new kakao.maps.LatLng(37.4931969, 126.814573),
    new kakao.maps.LatLng(37.4915531, 126.817904),
    new kakao.maps.LatLng(37.4899794, 126.822762),
    new kakao.maps.LatLng(37.4877351, 126.8235061),
    new kakao.maps.LatLng(37.4854809, 126.8192969),
    new kakao.maps.LatLng(37.4816405, 126.8199827),
    new kakao.maps.LatLng(37.4791625, 126.8189971),
    new kakao.maps.LatLng(37.4763621, 126.8152952),
    new kakao.maps.LatLng(37.4747205, 126.8146459),
    new kakao.maps.LatLng(37.4732881, 126.817076),
    new kakao.maps.LatLng(37.4741192, 126.8187239),
    new kakao.maps.LatLng(37.4763553, 126.8195989),
    new kakao.maps.LatLng(37.4759897, 126.8278719),
    new kakao.maps.LatLng(37.4776512, 126.8317475),
    new kakao.maps.LatLng(37.4767532, 126.8339281),
    new kakao.maps.LatLng(37.4744809, 126.8359294),
    new kakao.maps.LatLng(37.475392, 126.8383005),
    new kakao.maps.LatLng(37.4746479, 126.8410321),
    new kakao.maps.LatLng(37.4749715, 126.8427814),
    new kakao.maps.LatLng(37.4738124, 126.8453603),
    new kakao.maps.LatLng(37.480012, 126.8459113),
    new kakao.maps.LatLng(37.48191, 126.8470155),
    new kakao.maps.LatLng(37.481827, 126.8527424),
    new kakao.maps.LatLng(37.4854067, 126.8555066),
    new kakao.maps.LatLng(37.4860846, 126.8579708),
    new kakao.maps.LatLng(37.4899682, 126.8613841),
    new kakao.maps.LatLng(37.4915699, 126.8654623),
    new kakao.maps.LatLng(37.49426, 126.8668088),
    new kakao.maps.LatLng(37.4951278, 126.8683565),
    new kakao.maps.LatLng(37.4940956, 126.8697092),
    new kakao.maps.LatLng(37.4916613, 126.8693466),
    new kakao.maps.LatLng(37.4895402, 126.8704101),
    new kakao.maps.LatLng(37.4906414, 126.8723345),
    new kakao.maps.LatLng(37.4882584, 126.8730843),
    new kakao.maps.LatLng(37.4885708, 126.8767901),
    new kakao.maps.LatLng(37.4853671, 126.8745638),
    new kakao.maps.LatLng(37.4866723, 126.8784581),
    new kakao.maps.LatLng(37.4855632, 126.8813537),
    new kakao.maps.LatLng(37.4823496, 126.886155),
    new kakao.maps.LatLng(37.4804414, 126.8877295),
    new kakao.maps.LatLng(37.4793897, 126.8898815),
    new kakao.maps.LatLng(37.4783336, 126.8964731),
    new kakao.maps.LatLng(37.4789401, 126.8989434),
    new kakao.maps.LatLng(37.4811733, 126.900064),
    new kakao.maps.LatLng(37.4849988, 126.9031946)
];

        var guroPolygonC = new kakao.maps.Polygon({
            path: guroPolygonCPath,
            fillColor: '#009EDF',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#009EDF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
     
        // 금천구 다각형 생성(22비율)
        var geumcheonPolygonCPath = [ new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4783336, 126.8964731), new kakao.maps.LatLng(37.4793897, 126.8898815), new kakao.maps.LatLng(37.4804414, 126.8877295), new kakao.maps.LatLng(37.4823496, 126.886155), new kakao.maps.LatLng(37.4855632, 126.8813537), new kakao.maps.LatLng(37.4866723, 126.8784581), new kakao.maps.LatLng(37.4853671, 126.8745638), new kakao.maps.LatLng(37.4852298, 126.8718245), new kakao.maps.LatLng(37.4836436, 126.8728822), new kakao.maps.LatLng(37.4771039, 126.8759855), new kakao.maps.LatLng(37.4738278, 126.8780112), new kakao.maps.LatLng(37.4694169, 126.8815927), new kakao.maps.LatLng(37.4684591, 126.881631), new kakao.maps.LatLng(37.4665184, 126.8842988), new kakao.maps.LatLng(37.4643925, 126.8827454), new kakao.maps.LatLng(37.4627255, 126.884317), new kakao.maps.LatLng(37.4627551, 126.8861117), new kakao.maps.LatLng(37.4575101, 126.8858806), new kakao.maps.LatLng(37.4561777, 126.8863993), new kakao.maps.LatLng(37.4544844, 126.8892662), new kakao.maps.LatLng(37.4524961, 126.8903312), new kakao.maps.LatLng(37.451995, 126.8927328), new kakao.maps.LatLng(37.4527181, 126.8939824), new kakao.maps.LatLng(37.4484134, 126.8959156), new kakao.maps.LatLng(37.4466982, 126.8946497), new kakao.maps.LatLng(37.4454288, 126.8972601), new kakao.maps.LatLng(37.4369929, 126.9008673), new kakao.maps.LatLng(37.4358535, 126.902834), new kakao.maps.LatLng(37.4340675, 126.9029873), new kakao.maps.LatLng(37.4338646, 126.9094057), new kakao.maps.LatLng(37.4361712, 126.9113332), new kakao.maps.LatLng(37.4385546, 126.912294), new kakao.maps.LatLng(37.4400154, 126.9161336), new kakao.maps.LatLng(37.439825, 126.9192897), new kakao.maps.LatLng(37.444041, 126.9227625), new kakao.maps.LatLng(37.4457729, 126.923253), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4789401, 126.8989434) ];

        var geumcheonPolygonC = new kakao.maps.Polygon({
            path: geumcheonPolygonCPath,
            fillColor: '#0074BD',
            fillOpacity: 0.7,
            strokeWeight: 1,
            strokeColor: '#0074BD',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

                // 영등포구 다각형 생성(22비율)
        var yeongdeungpoPolygonCPath = [ new kakao.maps.LatLng(37.5339056, 126.9446791), new kakao.maps.LatLng(37.5378354, 126.938558), new kakao.maps.LatLng(37.5405306, 126.9328982), new kakao.maps.LatLng(37.5413625, 126.9303377), new kakao.maps.LatLng(37.5390762, 126.9276653), new kakao.maps.LatLng(37.5397435, 126.9248228), new kakao.maps.LatLng(37.5414296, 126.922414), new kakao.maps.LatLng(37.5414165, 126.9048307), new kakao.maps.LatLng(37.5480079, 126.898943), new kakao.maps.LatLng(37.5494341, 126.8946416), new kakao.maps.LatLng(37.5523, 126.8881084), new kakao.maps.LatLng(37.5558475, 126.88131), new kakao.maps.LatLng(37.556224, 126.8804278), new kakao.maps.LatLng(37.555305, 126.879688), new kakao.maps.LatLng(37.5550643, 126.8794927), new kakao.maps.LatLng(37.554747, 126.879237), new kakao.maps.LatLng(37.5537026, 126.879224), new kakao.maps.LatLng(37.5531512, 126.8792171), new kakao.maps.LatLng(37.5532765, 126.8789601), new kakao.maps.LatLng(37.5533372, 126.878835), new kakao.maps.LatLng(37.5535815, 126.8782443), new kakao.maps.LatLng(37.553546, 126.8781144), new kakao.maps.LatLng(37.5535245, 126.8780551), new kakao.maps.LatLng(37.5534501, 126.8779539), new kakao.maps.LatLng(37.5532133, 126.8779456), new kakao.maps.LatLng(37.5531701, 126.8779519), new kakao.maps.LatLng(37.5529934, 126.8780067), new kakao.maps.LatLng(37.5527979, 126.8780142), new kakao.maps.LatLng(37.5525651, 126.8780226), new kakao.maps.LatLng(37.5523189, 126.8780313), new kakao.maps.LatLng(37.5519352, 126.8780413), new kakao.maps.LatLng(37.5515205, 126.8781985), new kakao.maps.LatLng(37.5511263, 126.8785301), new kakao.maps.LatLng(37.5507488, 126.8788459), new kakao.maps.LatLng(37.550412, 126.8791236), new kakao.maps.LatLng(37.5500282, 126.8794146), new kakao.maps.LatLng(37.5499377, 126.8794778), new kakao.maps.LatLng(37.5497628, 126.8796001), new kakao.maps.LatLng(37.5494053, 126.8798959), new kakao.maps.LatLng(37.5484626, 126.8804437), new kakao.maps.LatLng(37.5481962, 126.880664), new kakao.maps.LatLng(37.543321, 126.885088), new kakao.maps.LatLng(37.5397825, 126.8863138), new kakao.maps.LatLng(37.5351351, 126.8897886), new kakao.maps.LatLng(37.5319258, 126.8890681), new kakao.maps.LatLng(37.5301524, 126.8896671), new kakao.maps.LatLng(37.5301503, 126.8871006), new kakao.maps.LatLng(37.5287593, 126.8843314), new kakao.maps.LatLng(37.5259082, 126.8809399), new kakao.maps.LatLng(37.5252536, 126.878749), new kakao.maps.LatLng(37.5203627, 126.879464), new kakao.maps.LatLng(37.5187577, 126.8782517), new kakao.maps.LatLng(37.5178764, 126.8791653), new kakao.maps.LatLng(37.5164199, 126.881729), new kakao.maps.LatLng(37.5138494, 126.8844331), new kakao.maps.LatLng(37.5132264, 126.8875197), new kakao.maps.LatLng(37.5103503, 126.8917119), new kakao.maps.LatLng(37.5050117, 126.8939767), new kakao.maps.LatLng(37.5033326, 126.8926737), new kakao.maps.LatLng(37.4893387, 126.896124), new kakao.maps.LatLng(37.4869351, 126.8981442), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4938221, 126.9104722), new kakao.maps.LatLng(37.4964189, 126.9129118), new kakao.maps.LatLng(37.4975997, 126.9194077), new kakao.maps.LatLng(37.5125265, 126.9253894), new kakao.maps.LatLng(37.5127969, 126.9267906), new kakao.maps.LatLng(37.5155543, 126.9268588), new kakao.maps.LatLng(37.5155752, 126.9323857), new kakao.maps.LatLng(37.5160787, 126.9392792), new kakao.maps.LatLng(37.5175262, 126.9498866), new kakao.maps.LatLng(37.5270289, 126.94988), new kakao.maps.LatLng(37.5339056, 126.9446791) ];

        var yeongdeungpoPolygonC = new kakao.maps.Polygon({
            path: yeongdeungpoPolygonAPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#E85239',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        
                // 동작구 다각형 생성(22비율)
                var dongjakPolygonCPath = [
    new kakao.maps.LatLng(37.5065363, 126.9804067),
    new kakao.maps.LatLng(37.5070128, 126.9752589),
    new kakao.maps.LatLng(37.5108166, 126.9649636),
    new kakao.maps.LatLng(37.5135025, 126.9612002),
    new kakao.maps.LatLng(37.516065, 126.9547037),
    new kakao.maps.LatLng(37.5175262, 126.9498866),
    new kakao.maps.LatLng(37.5160787, 126.9392792),
    new kakao.maps.LatLng(37.5155752, 126.9323857),
    new kakao.maps.LatLng(37.5155543, 126.9268588),
    new kakao.maps.LatLng(37.5127969, 126.9267906),
    new kakao.maps.LatLng(37.5125265, 126.9253894),
    new kakao.maps.LatLng(37.4975997, 126.9194077),
    new kakao.maps.LatLng(37.4964189, 126.9129118),
    new kakao.maps.LatLng(37.4938221, 126.9104722),
    new kakao.maps.LatLng(37.4850028, 126.9031989),
    new kakao.maps.LatLng(37.4849606, 126.9060977),
    new kakao.maps.LatLng(37.4865116, 126.911921),
    new kakao.maps.LatLng(37.4880073, 126.9135728),
    new kakao.maps.LatLng(37.489548, 126.9166515),
    new kakao.maps.LatLng(37.4902759, 126.9194523),
    new kakao.maps.LatLng(37.4899637, 126.924155),
    new kakao.maps.LatLng(37.4927983, 126.925577),
    new kakao.maps.LatLng(37.4949943, 126.9274611),
    new kakao.maps.LatLng(37.4932585, 126.9313461),
    new kakao.maps.LatLng(37.493189, 126.933849),
    new kakao.maps.LatLng(37.4919697, 126.9365336),
    new kakao.maps.LatLng(37.4929037, 126.9399265),
    new kakao.maps.LatLng(37.4921435, 126.9426218),
    new kakao.maps.LatLng(37.494039, 126.9471828),
    new kakao.maps.LatLng(37.4922055, 126.9516974),
    new kakao.maps.LatLng(37.4906416, 126.9537273),
    new kakao.maps.LatLng(37.4919773, 126.9574784),
    new kakao.maps.LatLng(37.4936159, 126.9589433),
    new kakao.maps.LatLng(37.4928741, 126.9613777),
    new kakao.maps.LatLng(37.4908252, 126.9607812),
    new kakao.maps.LatLng(37.4886278, 126.9619669),
    new kakao.maps.LatLng(37.4851775, 126.9619872),
    new kakao.maps.LatLng(37.4835752, 126.96107),
    new kakao.maps.LatLng(37.4798186, 126.9644275),
    new kakao.maps.LatLng(37.4789597, 126.9663255),
    new kakao.maps.LatLng(37.4753765, 126.9705226),
    new kakao.maps.LatLng(37.476201, 126.9742856),
    new kakao.maps.LatLng(37.4770573, 126.9816808),
    new kakao.maps.LatLng(37.4969936, 126.9829297),
    new kakao.maps.LatLng(37.499859, 126.9853872),
    new kakao.maps.LatLng(37.5026966, 126.9805363),
    new kakao.maps.LatLng(37.5065363, 126.9804067)
];

        var dongjakPolygonC = new kakao.maps.Polygon({
            path: dongjakPolygonCPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.8,
            strokeWeight: 1,
            strokeColor: '#E61E2B',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

// 관악구 다각형 생성(22비율)
var gwanakPolygonCPath = [ new kakao.maps.LatLng(37.4770573, 126.9816808), new kakao.maps.LatLng(37.476201, 126.9742856), new kakao.maps.LatLng(37.4753765, 126.9705226), new kakao.maps.LatLng(37.4789597, 126.9663255), new kakao.maps.LatLng(37.4798186, 126.9644275), new kakao.maps.LatLng(37.4835752, 126.96107), new kakao.maps.LatLng(37.4851775, 126.9619872), new kakao.maps.LatLng(37.4886278, 126.9619669), new kakao.maps.LatLng(37.4908252, 126.9607812), new kakao.maps.LatLng(37.4928741, 126.9613777), new kakao.maps.LatLng(37.4936159, 126.9589433), new kakao.maps.LatLng(37.4919773, 126.9574784), new kakao.maps.LatLng(37.4906416, 126.9537273), new kakao.maps.LatLng(37.4922055, 126.9516974), new kakao.maps.LatLng(37.494039, 126.9471828), new kakao.maps.LatLng(37.4921435, 126.9426218), new kakao.maps.LatLng(37.4929037, 126.9399265), new kakao.maps.LatLng(37.4919697, 126.9365336), new kakao.maps.LatLng(37.493189, 126.933849), new kakao.maps.LatLng(37.4932585, 126.9313461), new kakao.maps.LatLng(37.4949943, 126.9274611), new kakao.maps.LatLng(37.4927983, 126.925577), new kakao.maps.LatLng(37.4899637, 126.924155), new kakao.maps.LatLng(37.4902759, 126.9194523), new kakao.maps.LatLng(37.489548, 126.9166515), new kakao.maps.LatLng(37.4880073, 126.9135728), new kakao.maps.LatLng(37.4865116, 126.911921), new kakao.maps.LatLng(37.4849606, 126.9060977), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4811733, 126.900064), new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4483842, 126.9301661), new kakao.maps.LatLng(37.445463, 126.9305669), new kakao.maps.LatLng(37.4417395, 126.9366582), new kakao.maps.LatLng(37.4402029, 126.9378509), new kakao.maps.LatLng(37.4373807, 126.9377535), new kakao.maps.LatLng(37.4357034, 126.9402441), new kakao.maps.LatLng(37.4373944, 126.9414554), new kakao.maps.LatLng(37.4370754, 126.9451252), new kakao.maps.LatLng(37.4387126, 126.9483629), new kakao.maps.LatLng(37.4382501, 126.9492839), new kakao.maps.LatLng(37.4392385, 126.9523939), new kakao.maps.LatLng(37.4387351, 126.9551493), new kakao.maps.LatLng(37.4391229, 126.9589137), new kakao.maps.LatLng(37.4404007, 126.9600556), new kakao.maps.LatLng(37.4402806, 126.9629426), new kakao.maps.LatLng(37.4420397, 126.9646338), new kakao.maps.LatLng(37.4462673, 126.9642894), new kakao.maps.LatLng(37.4483804, 126.9676626), new kakao.maps.LatLng(37.4494526, 126.9705691), new kakao.maps.LatLng(37.4516571, 126.9718463), new kakao.maps.LatLng(37.454323, 126.9746584), new kakao.maps.LatLng(37.4556507, 126.978552), new kakao.maps.LatLng(37.4558313, 126.9824203), new kakao.maps.LatLng(37.4568271, 126.9828879), new kakao.maps.LatLng(37.4572124, 126.9866124), new kakao.maps.LatLng(37.4581534, 126.9886043), new kakao.maps.LatLng(37.4600297, 126.9875747), new kakao.maps.LatLng(37.4639986, 126.988344), new kakao.maps.LatLng(37.4676122, 126.9873023), new kakao.maps.LatLng(37.4698246, 126.9845159), new kakao.maps.LatLng(37.4737189, 126.9821725), new kakao.maps.LatLng(37.4770573, 126.9816808) ];

var gwanakPolygonC = new kakao.maps.Polygon({
    path: gwanakPolygonCPath,
    fillColor: '#009EDF',
    fillOpacity: 0.8,
    strokeWeight: 1,
    strokeColor: '#009EDF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 서초구 다각형 생성(22비율)
var seochoPolygonCPath = [
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.5234361, 127.0064445),
new kakao.maps.LatLng(37.5194968, 127.0007883),
new kakao.maps.LatLng(37.5131024, 126.9906716),
new kakao.maps.LatLng(37.5065431, 126.9855327),
new kakao.maps.LatLng(37.5065363, 126.9804067),
new kakao.maps.LatLng(37.5026966, 126.9805363),
new kakao.maps.LatLng(37.499859, 126.9853872),
new kakao.maps.LatLng(37.4969936, 126.9829297),
new kakao.maps.LatLng(37.4770573, 126.9816808),
new kakao.maps.LatLng(37.4737189, 126.9821725),
new kakao.maps.LatLng(37.4698246, 126.9845159),
new kakao.maps.LatLng(37.4676122, 126.9873023),
new kakao.maps.LatLng(37.4639986, 126.988344),
new kakao.maps.LatLng(37.4600297, 126.9875747),
new kakao.maps.LatLng(37.4581534, 126.9886043),
new kakao.maps.LatLng(37.4614959, 126.9933541),
new kakao.maps.LatLng(37.4618734, 126.9967683),
new kakao.maps.LatLng(37.464215, 126.9972632),
new kakao.maps.LatLng(37.4666083, 126.9962307),
new kakao.maps.LatLng(37.4671797, 126.9969853),
new kakao.maps.LatLng(37.4671246, 127.0027346),
new kakao.maps.LatLng(37.4657636, 127.0049273),
new kakao.maps.LatLng(37.4640347, 127.0045148),
new kakao.maps.LatLng(37.4578423, 127.0086622),
new kakao.maps.LatLng(37.4554428, 127.010818),
new kakao.maps.LatLng(37.4548611, 127.0145094),
new kakao.maps.LatLng(37.4561351, 127.017545),
new kakao.maps.LatLng(37.4556938, 127.0192823),
new kakao.maps.LatLng(37.4572538, 127.022851),
new kakao.maps.LatLng(37.4574817, 127.0252753),
new kakao.maps.LatLng(37.4596417, 127.0265719),
new kakao.maps.LatLng(37.4633413, 127.0296306),
new kakao.maps.LatLng(37.4653746, 127.0295269),
new kakao.maps.LatLng(37.4656262, 127.0311954),
new kakao.maps.LatLng(37.4641547, 127.0346931),
new kakao.maps.LatLng(37.4612371, 127.0337319),
new kakao.maps.LatLng(37.4601754, 127.0349239),
new kakao.maps.LatLng(37.4578668, 127.0350694),
new kakao.maps.LatLng(37.455203, 127.0371709),
new kakao.maps.LatLng(37.4526095, 127.0347723),
new kakao.maps.LatLng(37.4514669, 127.0364748),
new kakao.maps.LatLng(37.4494531, 127.037741),
new kakao.maps.LatLng(37.4464509, 127.0372545),
new kakao.maps.LatLng(37.4451803, 127.0382301),
new kakao.maps.LatLng(37.4432667, 127.0374826),
new kakao.maps.LatLng(37.4410155, 127.0352603),
new kakao.maps.LatLng(37.4391373, 127.0356865),
new kakao.maps.LatLng(37.4383913, 127.0371471),
new kakao.maps.LatLng(37.4383412, 127.0401422),
new kakao.maps.LatLng(37.4335915, 127.0463942),
new kakao.maps.LatLng(37.4307906, 127.0473967),
new kakao.maps.LatLng(37.4303374, 127.0493227),
new kakao.maps.LatLng(37.4284561, 127.0520464),
new kakao.maps.LatLng(37.4301499, 127.0578618),
new kakao.maps.LatLng(37.4301216, 127.0608665),
new kakao.maps.LatLng(37.4290228, 127.0656551),
new kakao.maps.LatLng(37.4307189, 127.0683088),
new kakao.maps.LatLng(37.4308177, 127.0712064),
new kakao.maps.LatLng(37.4324169, 127.0705709),
new kakao.maps.LatLng(37.4358635, 127.0714392),
new kakao.maps.LatLng(37.4374234, 127.0738798),
new kakao.maps.LatLng(37.4388568, 127.0720075),
new kakao.maps.LatLng(37.4415239, 127.0716257),
new kakao.maps.LatLng(37.442133, 127.0761442),
new kakao.maps.LatLng(37.4410297, 127.0803008),
new kakao.maps.LatLng(37.4413384, 127.0821566),
new kakao.maps.LatLng(37.4439083, 127.083954),
new kakao.maps.LatLng(37.4442491, 127.0865305),
new kakao.maps.LatLng(37.4454138, 127.0882762),
new kakao.maps.LatLng(37.4486278, 127.0883265),
new kakao.maps.LatLng(37.4527827, 127.0909588),
new kakao.maps.LatLng(37.4536339, 127.0927253),
new kakao.maps.LatLng(37.4558885, 127.0935402),
new kakao.maps.LatLng(37.4565198, 127.095769),
new kakao.maps.LatLng(37.4562188, 127.0990955),
new kakao.maps.LatLng(37.4585341, 127.101167)
];

var seochoPolygonC = new kakao.maps.Polygon({
    path: seochoPolygonCPath,
    fillColor: '#7D160F',
    fillOpacity: 0.8,
    strokeWeight: 1,
    strokeColor: '#7D160F',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강남구 다각형 생성(22비율)
var gangnamPolygonCPath = [
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5286757, 127.0551335),
new kakao.maps.LatLng(37.5342726, 127.0460023),
new kakao.maps.LatLng(37.5358577, 127.0396637),
new kakao.maps.LatLng(37.5358238, 127.0211723),
new kakao.maps.LatLng(37.5342595, 127.0177593),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.4600566, 127.1039435),
new kakao.maps.LatLng(37.4621594, 127.1043465),
new kakao.maps.LatLng(37.4624345, 127.1064566),
new kakao.maps.LatLng(37.4616446, 127.1118201),
new kakao.maps.LatLng(37.4598893, 127.1134332),
new kakao.maps.LatLng(37.458634, 127.116896),
new kakao.maps.LatLng(37.4622006, 127.1174754),
new kakao.maps.LatLng(37.464372, 127.12144),
new kakao.maps.LatLng(37.4665205, 127.1242057)
];

var gangnamPolygonC = new kakao.maps.Polygon({
    path: gangnamPolygonCPath,
    fillColor: '#7D160F',
    fillOpacity: 0.8,
    strokeWeight: 1,
    strokeColor: '#7D160F',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 송파구 다각형 생성(22비율)
var songpaPolygonCPath = [
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5414079, 127.1082818),
new kakao.maps.LatLng(37.5270069, 127.090161),
new kakao.maps.LatLng(37.524759, 127.0856328),
new kakao.maps.LatLng(37.5229485, 127.0799746),
new kakao.maps.LatLng(37.522514, 127.0769544),
new kakao.maps.LatLng(37.523872, 127.0686631),
new kakao.maps.LatLng(37.5268818, 127.0607945),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4684191, 127.1270342),
new kakao.maps.LatLng(37.4677511, 127.1301405),
new kakao.maps.LatLng(37.4683941, 127.1327994),
new kakao.maps.LatLng(37.4697986, 127.1319826),
new kakao.maps.LatLng(37.4715382, 127.1328449),
new kakao.maps.LatLng(37.4746269, 127.1328558),
new kakao.maps.LatLng(37.4742406, 127.1354681),
new kakao.maps.LatLng(37.4739308, 127.1435264),
new kakao.maps.LatLng(37.4773315, 127.1443703),
new kakao.maps.LatLng(37.4772222, 127.1471451),
new kakao.maps.LatLng(37.4815898, 127.1474588),
new kakao.maps.LatLng(37.4840436, 127.1486828),
new kakao.maps.LatLng(37.4862358, 127.1521778),
new kakao.maps.LatLng(37.489672, 127.1585233),
new kakao.maps.LatLng(37.492048, 127.1584792),
new kakao.maps.LatLng(37.4943902, 127.1600312),
new kakao.maps.LatLng(37.4968237, 127.1597796),
new kakao.maps.LatLng(37.4995369, 127.1613552),
new kakao.maps.LatLng(37.5031794, 127.1577291),
new kakao.maps.LatLng(37.5018946, 127.1565548),
new kakao.maps.LatLng(37.5029854, 127.1521336),
new kakao.maps.LatLng(37.5046783, 127.1502631),
new kakao.maps.LatLng(37.5032338, 127.1477163),
new kakao.maps.LatLng(37.5054583, 127.1411493),
new kakao.maps.LatLng(37.5067087, 127.1415163),
new kakao.maps.LatLng(37.5085171, 127.139952),
new kakao.maps.LatLng(37.5123608, 127.1413929),
new kakao.maps.LatLng(37.5126573, 127.1435398),
new kakao.maps.LatLng(37.5156419, 127.1421313),
new kakao.maps.LatLng(37.5155915, 127.1446078),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var songpaPolygonC = new kakao.maps.Polygon({
    path: songpaPolygonCPath,
    fillColor: '#D20D14',
    fillOpacity: 0.8,
    strokeWeight: 1,
    strokeColor: '#D20D14',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강동구 다각형 생성(22비율)
var gangdongPolygonCPath =[
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.5196245, 127.1447856),
new kakao.maps.LatLng(37.5219397, 127.1457414),
new kakao.maps.LatLng(37.5221448, 127.1478181),
new kakao.maps.LatLng(37.5263728, 127.1504017),
new kakao.maps.LatLng(37.5285295, 127.1526867),
new kakao.maps.LatLng(37.5319199, 127.1539334),
new kakao.maps.LatLng(37.533683, 127.1536063),
new kakao.maps.LatLng(37.5392702, 127.1576512),
new kakao.maps.LatLng(37.5411651, 127.1598933),
new kakao.maps.LatLng(37.5449999, 127.1631595),
new kakao.maps.LatLng(37.5442561, 127.1666417),
new kakao.maps.LatLng(37.5455346, 127.1721068),
new kakao.maps.LatLng(37.5452104, 127.1757181),
new kakao.maps.LatLng(37.5466816, 127.1793088),
new kakao.maps.LatLng(37.5463443, 127.1828251),
new kakao.maps.LatLng(37.5518204, 127.1829114),
new kakao.maps.LatLng(37.5528619, 127.1813807),
new kakao.maps.LatLng(37.5609928, 127.1819994),
new kakao.maps.LatLng(37.5654958, 127.179585),
new kakao.maps.LatLng(37.5689182, 127.1792158),
new kakao.maps.LatLng(37.5722139, 127.1777375),
new kakao.maps.LatLng(37.5740993, 127.17614),
new kakao.maps.LatLng(37.5783633, 127.1754421),
new kakao.maps.LatLng(37.5792655, 127.1768832),
new kakao.maps.LatLng(37.5812008, 127.1771547),
new kakao.maps.LatLng(37.5797349, 127.1738711),
new kakao.maps.LatLng(37.5786946, 127.1671595),
new kakao.maps.LatLng(37.5764649, 127.1629721),
new kakao.maps.LatLng(37.5704037, 127.1536011),
new kakao.maps.LatLng(37.5681865, 127.1493618),
new kakao.maps.LatLng(37.5682007, 127.138063),
new kakao.maps.LatLng(37.567884, 127.135692),
new kakao.maps.LatLng(37.565944, 127.1290179),
new kakao.maps.LatLng(37.5633331, 127.1234369),
new kakao.maps.LatLng(37.5592439, 127.1176932),
new kakao.maps.LatLng(37.5568724, 127.1153231),
new kakao.maps.LatLng(37.5543662, 127.1143095),
new kakao.maps.LatLng(37.5504987, 127.1115571),
new kakao.maps.LatLng(37.5469267, 127.1114708),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var gangdongPolygonC = new kakao.maps.Polygon({
    path: gangdongPolygonCPath,
    fillColor: '#E85239',
    fillOpacity: 0.8,
    strokeWeight: 1,
    strokeColor: '#E85239',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

                 // (22연령) 용산구 다각형 생성
                 var yongsanPolygonDPath = [
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.54413326436179, 127.00898460651953),
            new kakao.maps.LatLng(37.539639030116945, 127.00959054834321),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.52290225898471, 127.00614038053493),
            new kakao.maps.LatLng(37.51309192794448, 126.99070240960813),
            new kakao.maps.LatLng(37.50654651085339, 126.98553683648308),
            new kakao.maps.LatLng(37.50702053393398, 126.97524914998174),
            new kakao.maps.LatLng(37.51751820477105, 126.94988506562748),
            new kakao.maps.LatLng(37.52702918583156, 126.94987870367682),
            new kakao.maps.LatLng(37.534519656862926, 126.94481851935942),
            new kakao.maps.LatLng(37.537500243531994, 126.95335659960566),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.5541513366375, 126.9657135934734),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994)
        ];

        var yongsanPolygonD = new kakao.maps.Polygon({
            path: yongsanPolygonDPath,
            fillColor: '#A61914',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        // 동대문구 다각형 생성(22연령)        
        var dongdaemunPolygonDPath = [
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496),
            new kakao.maps.LatLng(37.60107201319839, 127.07287376670605),
            new kakao.maps.LatLng(37.59724304056685, 127.06949105186925),
            new kakao.maps.LatLng(37.58953367466315, 127.07030363208528),
            new kakao.maps.LatLng(37.58651213184981, 127.07264218709383),
            new kakao.maps.LatLng(37.5849555116177, 127.07216063016078),
            new kakao.maps.LatLng(37.58026781100598, 127.07619547037923),
            new kakao.maps.LatLng(37.571869232268774, 127.0782018408153),
            new kakao.maps.LatLng(37.559961773835425, 127.07239004251258),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.572878529071055, 127.04263554582458),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.57838361223621, 127.0232348231103),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5956815721534, 127.04062845365279),
            new kakao.maps.LatLng(37.5969637344377, 127.04302522879048),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496)
        ];

        var dongdaemunPolygonD = new kakao.maps.Polygon({
            path: dongdaemunPolygonDPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성동구 다각형 생성(22연령)
        var seungdongPolygonDPath = [
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.5594131360664, 127.07373408220053),
            new kakao.maps.LatLng(37.52832388381049, 127.05621773388143),
            new kakao.maps.LatLng(37.53423885672233, 127.04604398310076),
            new kakao.maps.LatLng(37.53582328355087, 127.03979942567628),
            new kakao.maps.LatLng(37.53581367627865, 127.0211714455564),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53938672166098, 127.00993448922989),
            new kakao.maps.LatLng(37.54157804358092, 127.00879872996808),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706)
        ];

        var seungdongPolygonD = new kakao.maps.Polygon({
            path: seungdongPolygonDPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 서대문구 다각형 생성(22연령)
        var seodaemunPolygonDPath = [
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003),
            new kakao.maps.LatLng(37.5992407011344, 126.95499403097206),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.5575156365052, 126.95991288916548),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.57599550420081, 126.902091747923),
            new kakao.maps.LatLng(37.587223103650295, 126.91284666446226),
            new kakao.maps.LatLng(37.58541570520177, 126.91531241017965),
            new kakao.maps.LatLng(37.585870567159255, 126.91638068573187),
            new kakao.maps.LatLng(37.583095195853055, 126.9159399866114),
            new kakao.maps.LatLng(37.583459593417196, 126.92175886498167),
            new kakao.maps.LatLng(37.587104600730505, 126.92388813813815),
            new kakao.maps.LatLng(37.588386594820484, 126.92800815682232),
            new kakao.maps.LatLng(37.59157595859555, 126.92776504133688),
            new kakao.maps.LatLng(37.59455434247408, 126.93027139545339),
            new kakao.maps.LatLng(37.59869748704149, 126.94088480070904),
            new kakao.maps.LatLng(37.60065830191363, 126.9414041615336),
            new kakao.maps.LatLng(37.60305781086164, 126.93995273804141),
            new kakao.maps.LatLng(37.610598531321436, 126.95037536795142),
            new kakao.maps.LatLng(37.6083605525023, 126.95056259057313),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003)
        ];

        var seodaemunPolygonD = new kakao.maps.Polygon({
            path: seodaemunPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 종로구 다각형 생성(22연령)
        var jongnoPolygonDPath = [
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046),
            new kakao.maps.LatLng(37.632194205253654, 126.97609588529602),
            new kakao.maps.LatLng(37.629026103322374, 126.97496405167149),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.60401657024552, 126.98665951539246),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.5788668917658, 127.02140099081309),
            new kakao.maps.LatLng(37.578034045208426, 127.02313962015988),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.5681357695346, 126.99014772014593),
            new kakao.maps.LatLng(37.569315246023024, 126.9732046364419),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.59875701675023, 126.95306020161668),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.60912809443569, 126.95032198271032),
            new kakao.maps.LatLng(37.615539700280216, 126.95072546923387),
            new kakao.maps.LatLng(37.62433621196653, 126.94900237336302),
            new kakao.maps.LatLng(37.62642708817027, 126.95037844036497),
            new kakao.maps.LatLng(37.629590994617104, 126.95881385457929),
            new kakao.maps.LatLng(37.629794440379136, 126.96376660599225),
            new kakao.maps.LatLng(37.632373740990175, 126.97302793692637),
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046)
        ];

        var jongnoPolygonD = new kakao.maps.Polygon({
            path: jongnoPolygonDPath,
            fillColor: '#F18077',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중구 다각형 생성(22연령)
        var jungPolygonDPath = [
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55487749311664, 126.97240854546743),
            new kakao.maps.LatLng(37.5548766923893, 126.9691718124876),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.55498984534305, 126.96173858545431),
            new kakao.maps.LatLng(37.55695455613004, 126.96343068837372),
            new kakao.maps.LatLng(37.5590262922649, 126.9616731414449),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.569485309984174, 126.97637402412326),
            new kakao.maps.LatLng(37.56810323716611, 126.98905202099309),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.572022763755164, 127.0223363152772),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56973041414113, 127.0234585247501),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894)
        ];

        var jungPolygonD = new kakao.maps.Polygon({
            path: jungPolygonDPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 광진구 다각형 생성(22연령)
        var gwangjinPolygonDPath = [
    new kakao.maps.LatLng(37.5568724, 127.1153231),
    new kakao.maps.LatLng(37.5585233, 127.113965),
    new kakao.maps.LatLng(37.5590006, 127.112297),
    new kakao.maps.LatLng(37.5585538, 127.1095286),
    new kakao.maps.LatLng(37.5564601, 127.1063932),
    new kakao.maps.LatLng(37.5595269, 127.1019134),
    new kakao.maps.LatLng(37.5616054, 127.1012509),
    new kakao.maps.LatLng(37.5643129, 127.1023143),
    new kakao.maps.LatLng(37.5701103, 127.1035059),
    new kakao.maps.LatLng(37.5714514, 127.104295),
    new kakao.maps.LatLng(37.5724694, 127.1017021),
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.5679178, 127.0768757),
    new kakao.maps.LatLng(37.5645904, 127.0740989),
    new kakao.maps.LatLng(37.5599603, 127.0723852),
    new kakao.maps.LatLng(37.559414, 127.0737358),
    new kakao.maps.LatLng(37.5393084, 127.0623676),
    new kakao.maps.LatLng(37.539291, 127.0623585),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5268818, 127.0607945),
    new kakao.maps.LatLng(37.523872, 127.0686631),
    new kakao.maps.LatLng(37.522514, 127.0769544),
    new kakao.maps.LatLng(37.5229485, 127.0799746),
    new kakao.maps.LatLng(37.524759, 127.0856328),
    new kakao.maps.LatLng(37.5270069, 127.090161),
    new kakao.maps.LatLng(37.5414079, 127.1082818),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5469267, 127.1114708),
    new kakao.maps.LatLng(37.5504987, 127.1115571),
    new kakao.maps.LatLng(37.5543662, 127.1143095),
    new kakao.maps.LatLng(37.5568724, 127.1153231)
];  
        var gwangjinPolygonD = new kakao.maps.Polygon({
            path: gwangjinPolygonDPath,
            fillColor: '#F18077',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중랑구 다각형 생성(22연령)
        var jungnangPolygonDPath = [
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.5760708, 127.1011435),
    new kakao.maps.LatLng(37.578907, 127.1030254),
    new kakao.maps.LatLng(37.5805343, 127.103429),
    new kakao.maps.LatLng(37.5833044, 127.109002),
    new kakao.maps.LatLng(37.5891647, 127.1106433),
    new kakao.maps.LatLng(37.5932091, 127.1131972),
    new kakao.maps.LatLng(37.5940164, 127.1166645),
    new kakao.maps.LatLng(37.5954971, 127.1168775),
    new kakao.maps.LatLng(37.599521, 127.1140639),
    new kakao.maps.LatLng(37.6021085, 127.1157227),
    new kakao.maps.LatLng(37.6046024, 127.118047),
    new kakao.maps.LatLng(37.607613, 127.1184769),
    new kakao.maps.LatLng(37.6088335, 127.1166833),
    new kakao.maps.LatLng(37.6118276, 127.1174901),
    new kakao.maps.LatLng(37.6160155, 127.1166717),
    new kakao.maps.LatLng(37.6178884, 127.1171467),
    new kakao.maps.LatLng(37.6195377, 127.115021),
    new kakao.maps.LatLng(37.6210546, 127.110519),
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6153366, 127.0701774),
    new kakao.maps.LatLng(37.6153196, 127.0702079),
    new kakao.maps.LatLng(37.6135142, 127.0717529),
    new kakao.maps.LatLng(37.6070224, 127.0711169),
    new kakao.maps.LatLng(37.6046424, 127.0715334),
    new kakao.maps.LatLng(37.6013304, 127.0728729),
    new kakao.maps.LatLng(37.600246, 127.0724977),
    new kakao.maps.LatLng(37.5972431, 127.069494),
    new kakao.maps.LatLng(37.5951242, 127.0694344),
    new kakao.maps.LatLng(37.5919078, 127.0707184),
    new kakao.maps.LatLng(37.5899586, 127.070228),
    new kakao.maps.LatLng(37.5865116, 127.0726438),
    new kakao.maps.LatLng(37.5849569, 127.0721613),
    new kakao.maps.LatLng(37.5793357, 127.076458),
    new kakao.maps.LatLng(37.5729206, 127.0772314),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5737318, 127.1008637)
];

        var jungnangPolygonD = new kakao.maps.Polygon({
            path: jungnangPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성북구 다각형 생성(22연령)
        var seongbukPolygonDPath = [
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235),
            new kakao.maps.LatLng(37.631446839436855, 126.99372381657889),
            new kakao.maps.LatLng(37.626192451322005, 126.99927047335905),
            new kakao.maps.LatLng(37.62382095469671, 127.00488450145781),
            new kakao.maps.LatLng(37.624026217174986, 127.00788862747375),
            new kakao.maps.LatLng(37.6205124078061, 127.00724034082933),
            new kakao.maps.LatLng(37.61679651952433, 127.01014412786792),
            new kakao.maps.LatLng(37.61472018601129, 127.01451127202589),
            new kakao.maps.LatLng(37.614629670135216, 127.01757841621624),
            new kakao.maps.LatLng(37.61137091590441, 127.02219857751122),
            new kakao.maps.LatLng(37.612692696824915, 127.02642583551054),
            new kakao.maps.LatLng(37.612367438936786, 127.03018593770908),
            new kakao.maps.LatLng(37.60896889076571, 127.0302525167858),
            new kakao.maps.LatLng(37.61279787695882, 127.03730791358603),
            new kakao.maps.LatLng(37.62426467261789, 127.04973339977498),
            new kakao.maps.LatLng(37.61449950127667, 127.06174181124696),
            new kakao.maps.LatLng(37.61561580859776, 127.06985247014711),
            new kakao.maps.LatLng(37.61351359068103, 127.07170798866412),
            new kakao.maps.LatLng(37.60762512162974, 127.07105453180604),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.59644879095525, 127.04184728392097),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.57782865303167, 127.02296295333255),
            new kakao.maps.LatLng(37.57889204835333, 127.02179043639809),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.60451393107786, 126.98678626394351),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.62980449548538, 126.97468284124939),
            new kakao.maps.LatLng(37.633657663246694, 126.97740053878216),
            new kakao.maps.LatLng(37.63476479485093, 126.98154674721893),
            new kakao.maps.LatLng(37.63780700422825, 126.9849494717052),
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235)
        ];

        var seongbukPolygonD = new kakao.maps.Polygon({
            path: seongbukPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강북구 다각형 생성(22연령)
        var gangbukPolygonDPath = [
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6850889, 127.0045265),
    new kakao.maps.LatLng(37.6834224, 126.9973582),
    new kakao.maps.LatLng(37.678828, 126.9929755),
    new kakao.maps.LatLng(37.6757199, 126.9931995),
    new kakao.maps.LatLng(37.672422, 126.9942076),
    new kakao.maps.LatLng(37.6678322, 126.993576),
    new kakao.maps.LatLng(37.6670301, 126.9941291),
    new kakao.maps.LatLng(37.6652317, 126.9922245),
    new kakao.maps.LatLng(37.6643912, 126.9882682),
    new kakao.maps.LatLng(37.6606003, 126.9872768),
    new kakao.maps.LatLng(37.6589432, 126.9860205),
    new kakao.maps.LatLng(37.6570035, 126.9830101),
    new kakao.maps.LatLng(37.6560387, 126.9796581),
    new kakao.maps.LatLng(37.6548152, 126.9799441),
    new kakao.maps.LatLng(37.6505404, 126.9824953),
    new kakao.maps.LatLng(37.64961, 126.9839369),
    new kakao.maps.LatLng(37.6457101, 126.9850955),
    new kakao.maps.LatLng(37.6436716, 126.9832554),
    new kakao.maps.LatLng(37.6400446, 126.9856762),
    new kakao.maps.LatLng(37.6363484, 126.9841726),
    new kakao.maps.LatLng(37.6340757, 126.9894095),
    new kakao.maps.LatLng(37.6302496, 126.9953935),
    new kakao.maps.LatLng(37.6262023, 126.999273),
    new kakao.maps.LatLng(37.625951, 127.0000402),
    new kakao.maps.LatLng(37.6259335, 127.0000628),
    new kakao.maps.LatLng(37.6242258, 127.0038971),
    new kakao.maps.LatLng(37.6240272, 127.0078883),
    new kakao.maps.LatLng(37.6208272, 127.0072158),
    new kakao.maps.LatLng(37.618622, 127.0085),
    new kakao.maps.LatLng(37.6162859, 127.0109519),
    new kakao.maps.LatLng(37.6146854, 127.0144744),
    new kakao.maps.LatLng(37.6146161, 127.0175368),
    new kakao.maps.LatLng(37.6113717, 127.0221965),
    new kakao.maps.LatLng(37.6126938, 127.0264334),
    new kakao.maps.LatLng(37.6123662, 127.0301844),
    new kakao.maps.LatLng(37.6089762, 127.0302524),
    new kakao.maps.LatLng(37.6129618, 127.0375131),
    new kakao.maps.LatLng(37.6157606, 127.0399847),
    new kakao.maps.LatLng(37.6186436, 127.0439485),
    new kakao.maps.LatLng(37.6226012, 127.0468685),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6843696, 127.0086619)
];

        var gangbukPolygonD = new kakao.maps.Polygon({
            path: gangbukPolygonDPath,
            fillColor: '#0074BD',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 도봉구 다각형 생성(22연령)
        var dobongPolygonDPath = [
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6879759, 127.0498208),
    new kakao.maps.LatLng(37.6908702, 127.0499658),
    new kakao.maps.LatLng(37.6940664, 127.0486327),
    new kakao.maps.LatLng(37.6923802, 127.0456492),
    new kakao.maps.LatLng(37.693687, 127.043083),
    new kakao.maps.LatLng(37.6952354, 127.0430909),
    new kakao.maps.LatLng(37.6952919, 127.0411383),
    new kakao.maps.LatLng(37.6926381, 127.0368093),
    new kakao.maps.LatLng(37.6918448, 127.0324625),
    new kakao.maps.LatLng(37.6930733, 127.0310969),
    new kakao.maps.LatLng(37.6962653, 127.0297701),
    new kakao.maps.LatLng(37.6992843, 127.0293125),
    new kakao.maps.LatLng(37.7009462, 127.02771),
    new kakao.maps.LatLng(37.6995947, 127.0253836),
    new kakao.maps.LatLng(37.6997207, 127.0221482),
    new kakao.maps.LatLng(37.7010174, 127.0198271),
    new kakao.maps.LatLng(37.7014553, 127.0154151),
    new kakao.maps.LatLng(37.6988007, 127.0138784),
    new kakao.maps.LatLng(37.6973775, 127.0121243),
    new kakao.maps.LatLng(37.6966991, 127.0096662),
    new kakao.maps.LatLng(37.6933154, 127.0097568),
    new kakao.maps.LatLng(37.6915772, 127.007678),
    new kakao.maps.LatLng(37.6900533, 127.0083369),
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6858137, 127.0518033)
];

        var dobongPolygonD = new kakao.maps.Polygon({
            path: dobongPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 노원구 다각형 생성(22연령)
        var nowonPolygonDPath = [
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6216472, 127.1040704),
    new kakao.maps.LatLng(37.6275838, 127.1059087),
    new kakao.maps.LatLng(37.6293016, 127.1088847),
    new kakao.maps.LatLng(37.6315033, 127.1116324),
    new kakao.maps.LatLng(37.6326429, 127.1122035),
    new kakao.maps.LatLng(37.6364891, 127.1124833),
    new kakao.maps.LatLng(37.6391262, 127.1105493),
    new kakao.maps.LatLng(37.6398412, 127.1120504),
    new kakao.maps.LatLng(37.6425246, 127.1108099),
    new kakao.maps.LatLng(37.6426948, 127.1093228),
    new kakao.maps.LatLng(37.6451721, 127.1067673),
    new kakao.maps.LatLng(37.6452258, 127.1028086),
    new kakao.maps.LatLng(37.6439649, 127.0975589),
    new kakao.maps.LatLng(37.6445705, 127.09457),
    new kakao.maps.LatLng(37.6496973, 127.0924745),
    new kakao.maps.LatLng(37.6524386, 127.0940495),
    new kakao.maps.LatLng(37.6537758, 127.0930673),
    new kakao.maps.LatLng(37.6593346, 127.0912069),
    new kakao.maps.LatLng(37.6632988, 127.0941422),
    new kakao.maps.LatLng(37.6675788, 127.095017),
    new kakao.maps.LatLng(37.6687685, 127.0962455),
    new kakao.maps.LatLng(37.6727011, 127.0957715),
    new kakao.maps.LatLng(37.673564, 127.0946559),
    new kakao.maps.LatLng(37.6767064, 127.0938558),
    new kakao.maps.LatLng(37.6786397, 127.0919859),
    new kakao.maps.LatLng(37.6814411, 127.0929524),
    new kakao.maps.LatLng(37.6855375, 127.0964162),
    new kakao.maps.LatLng(37.689071, 127.095996),
    new kakao.maps.LatLng(37.6899664, 127.0930367),
    new kakao.maps.LatLng(37.6895704, 127.0905519),
    new kakao.maps.LatLng(37.6899122, 127.0865306),
    new kakao.maps.LatLng(37.6917823, 127.083905),
    new kakao.maps.LatLng(37.694269, 127.0838433),
    new kakao.maps.LatLng(37.6961376, 127.0811047),
    new kakao.maps.LatLng(37.6959864, 127.0781963),
    new kakao.maps.LatLng(37.6951465, 127.0748951),
    new kakao.maps.LatLng(37.6937786, 127.0727908),
    new kakao.maps.LatLng(37.6939832, 127.0686396),
    new kakao.maps.LatLng(37.6949371, 127.0634232),
    new kakao.maps.LatLng(37.6930035, 127.0624128),
    new kakao.maps.LatLng(37.6902838, 127.0597139),
    new kakao.maps.LatLng(37.6892048, 127.0551791),
    new kakao.maps.LatLng(37.6870667, 127.0518042),
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6197959, 127.0544081),
    new kakao.maps.LatLng(37.6174813, 127.0574206),
    new kakao.maps.LatLng(37.6142587, 127.0632852),
    new kakao.maps.LatLng(37.6157243, 127.0697122),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.6203794, 127.105654)
];

        var nowonPolygonD = new kakao.maps.Polygon({
            path: nowonPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 은평구 다각형 생성(22연령)
        var eunpyeongPolygonDPath = [
    new kakao.maps.LatLng(37.6295893, 126.9588137),
    new kakao.maps.LatLng(37.62973, 126.9597977),
    new kakao.maps.LatLng(37.6332338, 126.9634013),
    new kakao.maps.LatLng(37.6357828, 126.9626334),
    new kakao.maps.LatLng(37.6421387, 126.9593275),
    new kakao.maps.LatLng(37.6467834, 126.959027),
    new kakao.maps.LatLng(37.6480477, 126.9578392),
    new kakao.maps.LatLng(37.6528372, 126.9571078),
    new kakao.maps.LatLng(37.6546009, 126.9543453),
    new kakao.maps.LatLng(37.6549496, 126.9513757),
    new kakao.maps.LatLng(37.6571298, 126.9478961),
    new kakao.maps.LatLng(37.6592154, 126.9475649),
    new kakao.maps.LatLng(37.6577222, 126.9421),
    new kakao.maps.LatLng(37.6566359, 126.9401282),
    new kakao.maps.LatLng(37.6523011, 126.9371587),
    new kakao.maps.LatLng(37.6511999, 126.9357024),
    new kakao.maps.LatLng(37.6500481, 126.9296991),
    new kakao.maps.LatLng(37.6461063, 126.9241229),
    new kakao.maps.LatLng(37.6447557, 126.9137208),
    new kakao.maps.LatLng(37.6476455, 126.9095352),
    new kakao.maps.LatLng(37.6486884, 126.905964),
    new kakao.maps.LatLng(37.6462898, 126.9077049),
    new kakao.maps.LatLng(37.6442586, 126.9122604),
    new kakao.maps.LatLng(37.6385095, 126.9100918),
    new kakao.maps.LatLng(37.6353165, 126.9108542),
    new kakao.maps.LatLng(37.633398, 126.9070962),
    new kakao.maps.LatLng(37.6308672, 126.9072938),
    new kakao.maps.LatLng(37.6293276, 126.9087697),
    new kakao.maps.LatLng(37.6262657, 126.9086108),
    new kakao.maps.LatLng(37.6244956, 126.9066268),
    new kakao.maps.LatLng(37.6219415, 126.9071175),
    new kakao.maps.LatLng(37.6207039, 126.9056125),
    new kakao.maps.LatLng(37.6190745, 126.9052311),
    new kakao.maps.LatLng(37.6188394, 126.903361),
    new kakao.maps.LatLng(37.6157535, 126.9018223),
    new kakao.maps.LatLng(37.6140692, 126.9017342),
    new kakao.maps.LatLng(37.6111913, 126.9003043),
    new kakao.maps.LatLng(37.6037417, 126.9021083),
    new kakao.maps.LatLng(37.6020402, 126.8999819),
    new kakao.maps.LatLng(37.5993665, 126.9013224),
    new kakao.maps.LatLng(37.5973371, 126.9010115),
    new kakao.maps.LatLng(37.5951135, 126.9018381),
    new kakao.maps.LatLng(37.5926784, 126.8989613),
    new kakao.maps.LatLng(37.589938, 126.8997501),
    new kakao.maps.LatLng(37.5885666, 126.896859),
    new kakao.maps.LatLng(37.5890755, 126.8932905),
    new kakao.maps.LatLng(37.5885221, 126.8922355),
    new kakao.maps.LatLng(37.5885328, 126.8871589),
    new kakao.maps.LatLng(37.5895376, 126.8858088),
    new kakao.maps.LatLng(37.593639, 126.885004),
    new kakao.maps.LatLng(37.5907926, 126.8820561),
    new kakao.maps.LatLng(37.5907588, 126.882095),
    new kakao.maps.LatLng(37.588347, 126.8845533),
    new kakao.maps.LatLng(37.5876412, 126.8852568),
    new kakao.maps.LatLng(37.5870924, 126.8858291),
    new kakao.maps.LatLng(37.5860266, 126.8871243),
    new kakao.maps.LatLng(37.5858059, 126.8874045),
    new kakao.maps.LatLng(37.5815606, 126.8937787),
    new kakao.maps.LatLng(37.5794888, 126.8969354),
    new kakao.maps.LatLng(37.5782229, 126.898808),
    new kakao.maps.LatLng(37.5765458, 126.901833),
    new kakao.maps.LatLng(37.5787907, 126.9044431),
    new kakao.maps.LatLng(37.5803263, 126.9060741),
    new kakao.maps.LatLng(37.58547, 126.9115429),
    new kakao.maps.LatLng(37.5865298, 126.9124768),
    new kakao.maps.LatLng(37.5868917, 126.9126854),
    new kakao.maps.LatLng(37.5870633, 126.9127725),
    new kakao.maps.LatLng(37.5862014, 126.9151912),
    new kakao.maps.LatLng(37.5860447, 126.9155519),
    new kakao.maps.LatLng(37.5853667, 126.9160692),
    new kakao.maps.LatLng(37.5853601, 126.9160646),
    new kakao.maps.LatLng(37.5843543, 126.9156798),
    new kakao.maps.LatLng(37.5837821, 126.9157485),
    new kakao.maps.LatLng(37.5831718, 126.9164206),
    new kakao.maps.LatLng(37.58325, 126.9178162),
    new kakao.maps.LatLng(37.5829392, 126.920859),
    new kakao.maps.LatLng(37.5838591, 126.9218276),
    new kakao.maps.LatLng(37.5846767, 126.9218555),
    new kakao.maps.LatLng(37.5852834, 126.9223929),
    new kakao.maps.LatLng(37.5856304, 126.9228635),
    new kakao.maps.LatLng(37.5869714, 126.923861),
    new kakao.maps.LatLng(37.5871207, 126.9240038),
    new kakao.maps.LatLng(37.5872166, 126.9246107),
    new kakao.maps.LatLng(37.5872168, 126.9252644),
    new kakao.maps.LatLng(37.5883854, 126.928009),
    new kakao.maps.LatLng(37.5911032, 126.927947),
    new kakao.maps.LatLng(37.5915762, 126.9277682),
    new kakao.maps.LatLng(37.5945528, 126.9302704),
    new kakao.maps.LatLng(37.5962984, 126.9327954),
    new kakao.maps.LatLng(37.5974786, 126.9364086),
    new kakao.maps.LatLng(37.5976207, 126.9382703),
    new kakao.maps.LatLng(37.5987329, 126.9408662),
    new kakao.maps.LatLng(37.6006774, 126.9413766),
    new kakao.maps.LatLng(37.6013511, 126.9407255),
    new kakao.maps.LatLng(37.6049576, 126.9421378),
    new kakao.maps.LatLng(37.6086085, 126.9482139),
    new kakao.maps.LatLng(37.609399, 126.9489364),
    new kakao.maps.LatLng(37.6138494, 126.9507966),
    new kakao.maps.LatLng(37.6155379, 126.9507242),
    new kakao.maps.LatLng(37.6199205, 126.9499112),
    new kakao.maps.LatLng(37.6207316, 126.9499381),
    new kakao.maps.LatLng(37.6209324, 126.9499158),
    new kakao.maps.LatLng(37.6232616, 126.9488984),
    new kakao.maps.LatLng(37.626418, 126.9504537),
    new kakao.maps.LatLng(37.6265452, 126.9516053),
    new kakao.maps.LatLng(37.628731, 126.956889),
    new kakao.maps.LatLng(37.6295893, 126.9588137)
];

        var eunpyeongPolygonD = new kakao.maps.Polygon({
            path: eunpyeongPolygonDPath,
            fillColor: '#0074BD',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 마포구 다각형 생성(22연령)
        var mapoPolygonDPath = [
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.55675317809392, 126.93190919632814),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.557241466445234, 126.95913438471307),
            new kakao.maps.LatLng(37.55908394430372, 126.96163689468189),
            new kakao.maps.LatLng(37.55820141918588, 126.96305432966605),
            new kakao.maps.LatLng(37.554784413504734, 126.9617251098019),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.539468942052544, 126.955731506394),
            new kakao.maps.LatLng(37.536292068277106, 126.95128907260018),
            new kakao.maps.LatLng(37.53569162926515, 126.94627494388307),
            new kakao.maps.LatLng(37.53377712226906, 126.94458373402794),
            new kakao.maps.LatLng(37.54135238063506, 126.93031191951576),
            new kakao.maps.LatLng(37.539036674424615, 126.9271006565075),
            new kakao.maps.LatLng(37.54143034750605, 126.9224138272872),
            new kakao.maps.LatLng(37.54141748538761, 126.90483000187002),
            new kakao.maps.LatLng(37.548015078285694, 126.89890097452322),
            new kakao.maps.LatLng(37.56300401736817, 126.86623824787709),
            new kakao.maps.LatLng(37.57178997971358, 126.85363039091744),
            new kakao.maps.LatLng(37.57379738998644, 126.85362646212587),
            new kakao.maps.LatLng(37.57747251471329, 126.864939928088),
            new kakao.maps.LatLng(37.5781913017327, 126.87625939970273),
            new kakao.maps.LatLng(37.57977132158497, 126.87767870371688),
            new kakao.maps.LatLng(37.584440882833654, 126.87653889183002),
            new kakao.maps.LatLng(37.59079311146897, 126.88205386700724),
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884)
        ];

        var mapoPolygonD = new kakao.maps.Polygon({
            path: mapoPolygonDPath,
            fillColor: '#F18077',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 양천구 다각형 생성(22연령)
        var yangcheonPolygonDPath = [
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5397562, 126.8216026),
    new kakao.maps.LatLng(37.5365431, 126.8224338),
    new kakao.maps.LatLng(37.5348887, 126.821878),
    new kakao.maps.LatLng(37.5299154, 126.8254181),
    new kakao.maps.LatLng(37.528389, 126.8279799),
    new kakao.maps.LatLng(37.5258342, 126.8281793),
    new kakao.maps.LatLng(37.5249238, 126.8264622),
    new kakao.maps.LatLng(37.5230079, 126.8251384),
    new kakao.maps.LatLng(37.5198753, 126.8255944),
    new kakao.maps.LatLng(37.516186, 126.8231123),
    new kakao.maps.LatLng(37.5130434, 126.8244262),
    new kakao.maps.LatLng(37.5090953, 126.8239041),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5187577, 126.8782517),
    new kakao.maps.LatLng(37.5203627, 126.879464),
    new kakao.maps.LatLng(37.5252536, 126.878749),
    new kakao.maps.LatLng(37.5259082, 126.8809399),
    new kakao.maps.LatLng(37.5287593, 126.8843314),
    new kakao.maps.LatLng(37.5301503, 126.8871006),
    new kakao.maps.LatLng(37.5301524, 126.8896671),
    new kakao.maps.LatLng(37.5319258, 126.8890681),
    new kakao.maps.LatLng(37.5351351, 126.8897886),
    new kakao.maps.LatLng(37.5397825, 126.8863138),
    new kakao.maps.LatLng(37.543321, 126.885088),
    new kakao.maps.LatLng(37.5481962, 126.880664),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.546944, 126.8745052)
];

        var yangcheonPolygonD = new kakao.maps.Polygon({
            path: yangcheonPolygonDPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강서구 다각형 생성(22연령)
        var gangseoPolygonDPath = [
    new kakao.maps.LatLng(37.5717904, 126.8536316),
    new kakao.maps.LatLng(37.5737991, 126.8536283),
    new kakao.maps.LatLng(37.5745142, 126.8510083),
    new kakao.maps.LatLng(37.5773942, 126.8467014),
    new kakao.maps.LatLng(37.5835872, 126.8327892),
    new kakao.maps.LatLng(37.588201, 126.8270511),
    new kakao.maps.LatLng(37.5900825, 126.8252892),
    new kakao.maps.LatLng(37.5912976, 126.822785),
    new kakao.maps.LatLng(37.5976193, 126.8139529),
    new kakao.maps.LatLng(37.5989607, 126.8113687),
    new kakao.maps.LatLng(37.604902, 126.8027567),
    new kakao.maps.LatLng(37.6024867, 126.7999484),
    new kakao.maps.LatLng(37.6013474, 126.7998667),
    new kakao.maps.LatLng(37.5998709, 126.7978909),
    new kakao.maps.LatLng(37.597712, 126.797114),
    new kakao.maps.LatLng(37.5947537, 126.797721),
    new kakao.maps.LatLng(37.5936525, 126.798726),
    new kakao.maps.LatLng(37.5913058, 126.7988344),
    new kakao.maps.LatLng(37.589326, 126.8012524),
    new kakao.maps.LatLng(37.5878099, 126.8007605),
    new kakao.maps.LatLng(37.5880729, 126.7987679),
    new kakao.maps.LatLng(37.583364, 126.7956796),
    new kakao.maps.LatLng(37.5797103, 126.7924063),
    new kakao.maps.LatLng(37.5805208, 126.7907535),
    new kakao.maps.LatLng(37.5777706, 126.790599),
    new kakao.maps.LatLng(37.5777198, 126.7893694),
    new kakao.maps.LatLng(37.5755709, 126.787642),
    new kakao.maps.LatLng(37.5735993, 126.7824424),
    new kakao.maps.LatLng(37.5692071, 126.7816643),
    new kakao.maps.LatLng(37.5672821, 126.7789707),
    new kakao.maps.LatLng(37.5670966, 126.776366),
    new kakao.maps.LatLng(37.5658733, 126.7751607),
    new kakao.maps.LatLng(37.5637152, 126.7771261),
    new kakao.maps.LatLng(37.5618635, 126.7761087),
    new kakao.maps.LatLng(37.5572273, 126.7698955),
    new kakao.maps.LatLng(37.5554503, 126.7645763),
    new kakao.maps.LatLng(37.5539545, 126.7676412),
    new kakao.maps.LatLng(37.551962, 126.7674713),
    new kakao.maps.LatLng(37.5515813, 126.7693259),
    new kakao.maps.LatLng(37.548316, 126.7717031),
    new kakao.maps.LatLng(37.5489742, 126.7752973),
    new kakao.maps.LatLng(37.54671, 126.7775751),
    new kakao.maps.LatLng(37.5460749, 126.7818371),
    new kakao.maps.LatLng(37.545997, 126.7869552),
    new kakao.maps.LatLng(37.5438485, 126.7907616),
    new kakao.maps.LatLng(37.541761, 126.7921302),
    new kakao.maps.LatLng(37.541372, 126.7949442),
    new kakao.maps.LatLng(37.5395572, 126.7938932),
    new kakao.maps.LatLng(37.5373674, 126.7939734),
    new kakao.maps.LatLng(37.5367714, 126.7961149),
    new kakao.maps.LatLng(37.5378446, 126.7994886),
    new kakao.maps.LatLng(37.5403453, 126.7988931),
    new kakao.maps.LatLng(37.5408808, 126.8008976),
    new kakao.maps.LatLng(37.5426716, 126.8016672),
    new kakao.maps.LatLng(37.5436059, 126.8068721),
    new kakao.maps.LatLng(37.5407765, 126.8125684),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5484626, 126.8804437),
    new kakao.maps.LatLng(37.5494053, 126.8798959),
    new kakao.maps.LatLng(37.5497628, 126.8796001),
    new kakao.maps.LatLng(37.5499377, 126.8794778),
    new kakao.maps.LatLng(37.5500282, 126.8794146),
    new kakao.maps.LatLng(37.550412, 126.8791236),
    new kakao.maps.LatLng(37.5507488, 126.8788459),
    new kakao.maps.LatLng(37.5511263, 126.8787108),
    new kakao.maps.LatLng(37.5515205, 126.8781985),
    new kakao.maps.LatLng(37.5519352, 126.8780413),
    new kakao.maps.LatLng(37.5523189, 126.8780313),
    new kakao.maps.LatLng(37.5525651, 126.8780226),
    new kakao.maps.LatLng(37.5527979, 126.8780142),
    new kakao.maps.LatLng(37.5529934, 126.8780067),
    new kakao.maps.LatLng(37.5531701, 126.8779519),
    new kakao.maps.LatLng(37.5532133, 126.8779456),
    new kakao.maps.LatLng(37.5534501, 126.8779539),
    new kakao.maps.LatLng(37.5535245, 126.8780551),
    new kakao.maps.LatLng(37.553546, 126.8781144),
    new kakao.maps.LatLng(37.5535815, 126.8782443),
    new kakao.maps.LatLng(37.5533372, 126.878835),
    new kakao.maps.LatLng(37.5532765, 126.8789601),
    new kakao.maps.LatLng(37.5531512, 126.8792171),
    new kakao.maps.LatLng(37.5537026, 126.879224),
    new kakao.maps.LatLng(37.554747, 126.879237),
    new kakao.maps.LatLng(37.5550643, 126.8794927),
    new kakao.maps.LatLng(37.555305, 126.879688),
    new kakao.maps.LatLng(37.556224, 126.8804278),
    new kakao.maps.LatLng(37.5562828, 126.8804743),
    new kakao.maps.LatLng(37.5565904, 126.8798677),
    new kakao.maps.LatLng(37.5566999, 126.8796536),
    new kakao.maps.LatLng(37.5569932, 126.8790797),
    new kakao.maps.LatLng(37.5571835, 126.8787108),
    new kakao.maps.LatLng(37.5577477, 126.8776168),
    new kakao.maps.LatLng(37.5580956, 126.8769422),
    new kakao.maps.LatLng(37.5582839, 126.8765751),
    new kakao.maps.LatLng(37.5589502, 126.8752775),
    new kakao.maps.LatLng(37.5591563, 126.8748767),
    new kakao.maps.LatLng(37.5595945, 126.874025),
    new kakao.maps.LatLng(37.5596946, 126.8738248),
    new kakao.maps.LatLng(37.5601596, 126.8728588),
    new kakao.maps.LatLng(37.5605276, 126.8720972),
    new kakao.maps.LatLng(37.5609333, 126.8712519),
    new kakao.maps.LatLng(37.5615358, 126.8699951),
    new kakao.maps.LatLng(37.5619632, 126.8691064),
    new kakao.maps.LatLng(37.5621959, 126.868634),
    new kakao.maps.LatLng(37.5627029, 126.8677403),
    new kakao.maps.LatLng(37.5629894, 126.8672261),
    new kakao.maps.LatLng(37.5632825, 126.8666958),
    new kakao.maps.LatLng(37.5637559, 126.8658888),
    new kakao.maps.LatLng(37.5640521, 126.8654083),
    new kakao.maps.LatLng(37.5644624, 126.8647347),
    new kakao.maps.LatLng(37.5647185, 126.8643124),
    new kakao.maps.LatLng(37.5649731, 126.8639165),
    new kakao.maps.LatLng(37.5650512, 126.8637912),
    new kakao.maps.LatLng(37.5652642, 126.8634888),
    new kakao.maps.LatLng(37.5653859, 126.8633098),
    new kakao.maps.LatLng(37.5654471, 126.8632313),
    new kakao.maps.LatLng(37.5655495, 126.8630904),
    new kakao.maps.LatLng(37.5657186, 126.8628754),
    new kakao.maps.LatLng(37.5660443, 126.8624873),
    new kakao.maps.LatLng(37.5663031, 126.8621474),
    new kakao.maps.LatLng(37.5663376, 126.8621034),
    new kakao.maps.LatLng(37.5664484, 126.8619718),
    new kakao.maps.LatLng(37.5667462, 126.861637),
    new kakao.maps.LatLng(37.5672618, 126.8610683),
    new kakao.maps.LatLng(37.5675217, 126.8607424),
    new kakao.maps.LatLng(37.5676648, 126.8605839),
    new kakao.maps.LatLng(37.5679501, 126.8602879),
    new kakao.maps.LatLng(37.5682635, 126.8599471),
    new kakao.maps.LatLng(37.5686039, 126.8595982),
    new kakao.maps.LatLng(37.5688681, 126.8592962),
    new kakao.maps.LatLng(37.5693278, 126.8588345),
    new kakao.maps.LatLng(37.5695699, 126.8585727),
    new kakao.maps.LatLng(37.5700741, 126.8580604),
    new kakao.maps.LatLng(37.5702804, 126.8578288),
    new kakao.maps.LatLng(37.5704464, 126.8576497),
    new kakao.maps.LatLng(37.5705987, 126.8574919),
    new kakao.maps.LatLng(37.5708578, 126.8572342),
    new kakao.maps.LatLng(37.5710034, 126.8571121),
    new kakao.maps.LatLng(37.5712288, 126.8569134),
    new kakao.maps.LatLng(37.5715422, 126.8566245),
    new kakao.maps.LatLng(37.5717665, 126.8564237),
    new kakao.maps.LatLng(37.5717904, 126.8536316)
];

        var gangseoPolygonD = new kakao.maps.Polygon({
            path: gangseoPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 구로구 다각형 생성(22연령)
        var guroPolygonDPath = [
    new kakao.maps.LatLng(37.4849988, 126.9031946),
    new kakao.maps.LatLng(37.4869351, 126.8981442),
    new kakao.maps.LatLng(37.4893387, 126.896124),
    new kakao.maps.LatLng(37.5033326, 126.8926737),
    new kakao.maps.LatLng(37.5050117, 126.8939767),
    new kakao.maps.LatLng(37.5103503, 126.8917119),
    new kakao.maps.LatLng(37.5132264, 126.8875197),
    new kakao.maps.LatLng(37.5138494, 126.8844331),
    new kakao.maps.LatLng(37.5164199, 126.881729),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5076346, 126.8222152),
    new kakao.maps.LatLng(37.5056852, 126.8225503),
    new kakao.maps.LatLng(37.5022364, 126.821611),
    new kakao.maps.LatLng(37.5006401, 126.8194028),
    new kakao.maps.LatLng(37.4993555, 126.8196714),
    new kakao.maps.LatLng(37.4977435, 126.8161301),
    new kakao.maps.LatLng(37.4982134, 126.8141214),
    new kakao.maps.LatLng(37.4964818, 126.8129811),
    new kakao.maps.LatLng(37.4931969, 126.814573),
    new kakao.maps.LatLng(37.4915531, 126.817904),
    new kakao.maps.LatLng(37.4899794, 126.822762),
    new kakao.maps.LatLng(37.4877351, 126.8235061),
    new kakao.maps.LatLng(37.4854809, 126.8192969),
    new kakao.maps.LatLng(37.4816405, 126.8199827),
    new kakao.maps.LatLng(37.4791625, 126.8189971),
    new kakao.maps.LatLng(37.4763621, 126.8152952),
    new kakao.maps.LatLng(37.4747205, 126.8146459),
    new kakao.maps.LatLng(37.4732881, 126.817076),
    new kakao.maps.LatLng(37.4741192, 126.8187239),
    new kakao.maps.LatLng(37.4763553, 126.8195989),
    new kakao.maps.LatLng(37.4759897, 126.8278719),
    new kakao.maps.LatLng(37.4776512, 126.8317475),
    new kakao.maps.LatLng(37.4767532, 126.8339281),
    new kakao.maps.LatLng(37.4744809, 126.8359294),
    new kakao.maps.LatLng(37.475392, 126.8383005),
    new kakao.maps.LatLng(37.4746479, 126.8410321),
    new kakao.maps.LatLng(37.4749715, 126.8427814),
    new kakao.maps.LatLng(37.4738124, 126.8453603),
    new kakao.maps.LatLng(37.480012, 126.8459113),
    new kakao.maps.LatLng(37.48191, 126.8470155),
    new kakao.maps.LatLng(37.481827, 126.8527424),
    new kakao.maps.LatLng(37.4854067, 126.8555066),
    new kakao.maps.LatLng(37.4860846, 126.8579708),
    new kakao.maps.LatLng(37.4899682, 126.8613841),
    new kakao.maps.LatLng(37.4915699, 126.8654623),
    new kakao.maps.LatLng(37.49426, 126.8668088),
    new kakao.maps.LatLng(37.4951278, 126.8683565),
    new kakao.maps.LatLng(37.4940956, 126.8697092),
    new kakao.maps.LatLng(37.4916613, 126.8693466),
    new kakao.maps.LatLng(37.4895402, 126.8704101),
    new kakao.maps.LatLng(37.4906414, 126.8723345),
    new kakao.maps.LatLng(37.4882584, 126.8730843),
    new kakao.maps.LatLng(37.4885708, 126.8767901),
    new kakao.maps.LatLng(37.4853671, 126.8745638),
    new kakao.maps.LatLng(37.4866723, 126.8784581),
    new kakao.maps.LatLng(37.4855632, 126.8813537),
    new kakao.maps.LatLng(37.4823496, 126.886155),
    new kakao.maps.LatLng(37.4804414, 126.8877295),
    new kakao.maps.LatLng(37.4793897, 126.8898815),
    new kakao.maps.LatLng(37.4783336, 126.8964731),
    new kakao.maps.LatLng(37.4789401, 126.8989434),
    new kakao.maps.LatLng(37.4811733, 126.900064),
    new kakao.maps.LatLng(37.4849988, 126.9031946)
];

        var guroPolygonD = new kakao.maps.Polygon({
            path: guroPolygonDPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
     
        // 금천구 다각형 생성(22연령)
        var geumcheonPolygonDPath = [ new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4783336, 126.8964731), new kakao.maps.LatLng(37.4793897, 126.8898815), new kakao.maps.LatLng(37.4804414, 126.8877295), new kakao.maps.LatLng(37.4823496, 126.886155), new kakao.maps.LatLng(37.4855632, 126.8813537), new kakao.maps.LatLng(37.4866723, 126.8784581), new kakao.maps.LatLng(37.4853671, 126.8745638), new kakao.maps.LatLng(37.4852298, 126.8718245), new kakao.maps.LatLng(37.4836436, 126.8728822), new kakao.maps.LatLng(37.4771039, 126.8759855), new kakao.maps.LatLng(37.4738278, 126.8780112), new kakao.maps.LatLng(37.4694169, 126.8815927), new kakao.maps.LatLng(37.4684591, 126.881631), new kakao.maps.LatLng(37.4665184, 126.8842988), new kakao.maps.LatLng(37.4643925, 126.8827454), new kakao.maps.LatLng(37.4627255, 126.884317), new kakao.maps.LatLng(37.4627551, 126.8861117), new kakao.maps.LatLng(37.4575101, 126.8858806), new kakao.maps.LatLng(37.4561777, 126.8863993), new kakao.maps.LatLng(37.4544844, 126.8892662), new kakao.maps.LatLng(37.4524961, 126.8903312), new kakao.maps.LatLng(37.451995, 126.8927328), new kakao.maps.LatLng(37.4527181, 126.8939824), new kakao.maps.LatLng(37.4484134, 126.8959156), new kakao.maps.LatLng(37.4466982, 126.8946497), new kakao.maps.LatLng(37.4454288, 126.8972601), new kakao.maps.LatLng(37.4369929, 126.9008673), new kakao.maps.LatLng(37.4358535, 126.902834), new kakao.maps.LatLng(37.4340675, 126.9029873), new kakao.maps.LatLng(37.4338646, 126.9094057), new kakao.maps.LatLng(37.4361712, 126.9113332), new kakao.maps.LatLng(37.4385546, 126.912294), new kakao.maps.LatLng(37.4400154, 126.9161336), new kakao.maps.LatLng(37.439825, 126.9192897), new kakao.maps.LatLng(37.444041, 126.9227625), new kakao.maps.LatLng(37.4457729, 126.923253), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4789401, 126.8989434) ];

        var geumcheonPolygonD = new kakao.maps.Polygon({
            path: geumcheonPolygonDPath,
            fillColor: '#0074BD',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

                // 영등포구 다각형 생성(22비율)
        var yeongdeungpoPolygonDPath = [ new kakao.maps.LatLng(37.5339056, 126.9446791), new kakao.maps.LatLng(37.5378354, 126.938558), new kakao.maps.LatLng(37.5405306, 126.9328982), new kakao.maps.LatLng(37.5413625, 126.9303377), new kakao.maps.LatLng(37.5390762, 126.9276653), new kakao.maps.LatLng(37.5397435, 126.9248228), new kakao.maps.LatLng(37.5414296, 126.922414), new kakao.maps.LatLng(37.5414165, 126.9048307), new kakao.maps.LatLng(37.5480079, 126.898943), new kakao.maps.LatLng(37.5494341, 126.8946416), new kakao.maps.LatLng(37.5523, 126.8881084), new kakao.maps.LatLng(37.5558475, 126.88131), new kakao.maps.LatLng(37.556224, 126.8804278), new kakao.maps.LatLng(37.555305, 126.879688), new kakao.maps.LatLng(37.5550643, 126.8794927), new kakao.maps.LatLng(37.554747, 126.879237), new kakao.maps.LatLng(37.5537026, 126.879224), new kakao.maps.LatLng(37.5531512, 126.8792171), new kakao.maps.LatLng(37.5532765, 126.8789601), new kakao.maps.LatLng(37.5533372, 126.878835), new kakao.maps.LatLng(37.5535815, 126.8782443), new kakao.maps.LatLng(37.553546, 126.8781144), new kakao.maps.LatLng(37.5535245, 126.8780551), new kakao.maps.LatLng(37.5534501, 126.8779539), new kakao.maps.LatLng(37.5532133, 126.8779456), new kakao.maps.LatLng(37.5531701, 126.8779519), new kakao.maps.LatLng(37.5529934, 126.8780067), new kakao.maps.LatLng(37.5527979, 126.8780142), new kakao.maps.LatLng(37.5525651, 126.8780226), new kakao.maps.LatLng(37.5523189, 126.8780313), new kakao.maps.LatLng(37.5519352, 126.8780413), new kakao.maps.LatLng(37.5515205, 126.8781985), new kakao.maps.LatLng(37.5511263, 126.8785301), new kakao.maps.LatLng(37.5507488, 126.8788459), new kakao.maps.LatLng(37.550412, 126.8791236), new kakao.maps.LatLng(37.5500282, 126.8794146), new kakao.maps.LatLng(37.5499377, 126.8794778), new kakao.maps.LatLng(37.5497628, 126.8796001), new kakao.maps.LatLng(37.5494053, 126.8798959), new kakao.maps.LatLng(37.5484626, 126.8804437), new kakao.maps.LatLng(37.5481962, 126.880664), new kakao.maps.LatLng(37.543321, 126.885088), new kakao.maps.LatLng(37.5397825, 126.8863138), new kakao.maps.LatLng(37.5351351, 126.8897886), new kakao.maps.LatLng(37.5319258, 126.8890681), new kakao.maps.LatLng(37.5301524, 126.8896671), new kakao.maps.LatLng(37.5301503, 126.8871006), new kakao.maps.LatLng(37.5287593, 126.8843314), new kakao.maps.LatLng(37.5259082, 126.8809399), new kakao.maps.LatLng(37.5252536, 126.878749), new kakao.maps.LatLng(37.5203627, 126.879464), new kakao.maps.LatLng(37.5187577, 126.8782517), new kakao.maps.LatLng(37.5178764, 126.8791653), new kakao.maps.LatLng(37.5164199, 126.881729), new kakao.maps.LatLng(37.5138494, 126.8844331), new kakao.maps.LatLng(37.5132264, 126.8875197), new kakao.maps.LatLng(37.5103503, 126.8917119), new kakao.maps.LatLng(37.5050117, 126.8939767), new kakao.maps.LatLng(37.5033326, 126.8926737), new kakao.maps.LatLng(37.4893387, 126.896124), new kakao.maps.LatLng(37.4869351, 126.8981442), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4938221, 126.9104722), new kakao.maps.LatLng(37.4964189, 126.9129118), new kakao.maps.LatLng(37.4975997, 126.9194077), new kakao.maps.LatLng(37.5125265, 126.9253894), new kakao.maps.LatLng(37.5127969, 126.9267906), new kakao.maps.LatLng(37.5155543, 126.9268588), new kakao.maps.LatLng(37.5155752, 126.9323857), new kakao.maps.LatLng(37.5160787, 126.9392792), new kakao.maps.LatLng(37.5175262, 126.9498866), new kakao.maps.LatLng(37.5270289, 126.94988), new kakao.maps.LatLng(37.5339056, 126.9446791) ];

        var yeongdeungpoPolygonD = new kakao.maps.Polygon({
            path: yeongdeungpoPolygonDPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        
                // 동작구 다각형 생성(22연령)
                var dongjakPolygonDPath = [
    new kakao.maps.LatLng(37.5065363, 126.9804067),
    new kakao.maps.LatLng(37.5070128, 126.9752589),
    new kakao.maps.LatLng(37.5108166, 126.9649636),
    new kakao.maps.LatLng(37.5135025, 126.9612002),
    new kakao.maps.LatLng(37.516065, 126.9547037),
    new kakao.maps.LatLng(37.5175262, 126.9498866),
    new kakao.maps.LatLng(37.5160787, 126.9392792),
    new kakao.maps.LatLng(37.5155752, 126.9323857),
    new kakao.maps.LatLng(37.5155543, 126.9268588),
    new kakao.maps.LatLng(37.5127969, 126.9267906),
    new kakao.maps.LatLng(37.5125265, 126.9253894),
    new kakao.maps.LatLng(37.4975997, 126.9194077),
    new kakao.maps.LatLng(37.4964189, 126.9129118),
    new kakao.maps.LatLng(37.4938221, 126.9104722),
    new kakao.maps.LatLng(37.4850028, 126.9031989),
    new kakao.maps.LatLng(37.4849606, 126.9060977),
    new kakao.maps.LatLng(37.4865116, 126.911921),
    new kakao.maps.LatLng(37.4880073, 126.9135728),
    new kakao.maps.LatLng(37.489548, 126.9166515),
    new kakao.maps.LatLng(37.4902759, 126.9194523),
    new kakao.maps.LatLng(37.4899637, 126.924155),
    new kakao.maps.LatLng(37.4927983, 126.925577),
    new kakao.maps.LatLng(37.4949943, 126.9274611),
    new kakao.maps.LatLng(37.4932585, 126.9313461),
    new kakao.maps.LatLng(37.493189, 126.933849),
    new kakao.maps.LatLng(37.4919697, 126.9365336),
    new kakao.maps.LatLng(37.4929037, 126.9399265),
    new kakao.maps.LatLng(37.4921435, 126.9426218),
    new kakao.maps.LatLng(37.494039, 126.9471828),
    new kakao.maps.LatLng(37.4922055, 126.9516974),
    new kakao.maps.LatLng(37.4906416, 126.9537273),
    new kakao.maps.LatLng(37.4919773, 126.9574784),
    new kakao.maps.LatLng(37.4936159, 126.9589433),
    new kakao.maps.LatLng(37.4928741, 126.9613777),
    new kakao.maps.LatLng(37.4908252, 126.9607812),
    new kakao.maps.LatLng(37.4886278, 126.9619669),
    new kakao.maps.LatLng(37.4851775, 126.9619872),
    new kakao.maps.LatLng(37.4835752, 126.96107),
    new kakao.maps.LatLng(37.4798186, 126.9644275),
    new kakao.maps.LatLng(37.4789597, 126.9663255),
    new kakao.maps.LatLng(37.4753765, 126.9705226),
    new kakao.maps.LatLng(37.476201, 126.9742856),
    new kakao.maps.LatLng(37.4770573, 126.9816808),
    new kakao.maps.LatLng(37.4969936, 126.9829297),
    new kakao.maps.LatLng(37.499859, 126.9853872),
    new kakao.maps.LatLng(37.5026966, 126.9805363),
    new kakao.maps.LatLng(37.5065363, 126.9804067)
];

        var dongjakPolygonD = new kakao.maps.Polygon({
            path: dongjakPolygonDPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

// 관악구 다각형 생성(22연령)
var gwanakPolygonDPath = [ new kakao.maps.LatLng(37.4770573, 126.9816808), new kakao.maps.LatLng(37.476201, 126.9742856), new kakao.maps.LatLng(37.4753765, 126.9705226), new kakao.maps.LatLng(37.4789597, 126.9663255), new kakao.maps.LatLng(37.4798186, 126.9644275), new kakao.maps.LatLng(37.4835752, 126.96107), new kakao.maps.LatLng(37.4851775, 126.9619872), new kakao.maps.LatLng(37.4886278, 126.9619669), new kakao.maps.LatLng(37.4908252, 126.9607812), new kakao.maps.LatLng(37.4928741, 126.9613777), new kakao.maps.LatLng(37.4936159, 126.9589433), new kakao.maps.LatLng(37.4919773, 126.9574784), new kakao.maps.LatLng(37.4906416, 126.9537273), new kakao.maps.LatLng(37.4922055, 126.9516974), new kakao.maps.LatLng(37.494039, 126.9471828), new kakao.maps.LatLng(37.4921435, 126.9426218), new kakao.maps.LatLng(37.4929037, 126.9399265), new kakao.maps.LatLng(37.4919697, 126.9365336), new kakao.maps.LatLng(37.493189, 126.933849), new kakao.maps.LatLng(37.4932585, 126.9313461), new kakao.maps.LatLng(37.4949943, 126.9274611), new kakao.maps.LatLng(37.4927983, 126.925577), new kakao.maps.LatLng(37.4899637, 126.924155), new kakao.maps.LatLng(37.4902759, 126.9194523), new kakao.maps.LatLng(37.489548, 126.9166515), new kakao.maps.LatLng(37.4880073, 126.9135728), new kakao.maps.LatLng(37.4865116, 126.911921), new kakao.maps.LatLng(37.4849606, 126.9060977), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4811733, 126.900064), new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4483842, 126.9301661), new kakao.maps.LatLng(37.445463, 126.9305669), new kakao.maps.LatLng(37.4417395, 126.9366582), new kakao.maps.LatLng(37.4402029, 126.9378509), new kakao.maps.LatLng(37.4373807, 126.9377535), new kakao.maps.LatLng(37.4357034, 126.9402441), new kakao.maps.LatLng(37.4373944, 126.9414554), new kakao.maps.LatLng(37.4370754, 126.9451252), new kakao.maps.LatLng(37.4387126, 126.9483629), new kakao.maps.LatLng(37.4382501, 126.9492839), new kakao.maps.LatLng(37.4392385, 126.9523939), new kakao.maps.LatLng(37.4387351, 126.9551493), new kakao.maps.LatLng(37.4391229, 126.9589137), new kakao.maps.LatLng(37.4404007, 126.9600556), new kakao.maps.LatLng(37.4402806, 126.9629426), new kakao.maps.LatLng(37.4420397, 126.9646338), new kakao.maps.LatLng(37.4462673, 126.9642894), new kakao.maps.LatLng(37.4483804, 126.9676626), new kakao.maps.LatLng(37.4494526, 126.9705691), new kakao.maps.LatLng(37.4516571, 126.9718463), new kakao.maps.LatLng(37.454323, 126.9746584), new kakao.maps.LatLng(37.4556507, 126.978552), new kakao.maps.LatLng(37.4558313, 126.9824203), new kakao.maps.LatLng(37.4568271, 126.9828879), new kakao.maps.LatLng(37.4572124, 126.9866124), new kakao.maps.LatLng(37.4581534, 126.9886043), new kakao.maps.LatLng(37.4600297, 126.9875747), new kakao.maps.LatLng(37.4639986, 126.988344), new kakao.maps.LatLng(37.4676122, 126.9873023), new kakao.maps.LatLng(37.4698246, 126.9845159), new kakao.maps.LatLng(37.4737189, 126.9821725), new kakao.maps.LatLng(37.4770573, 126.9816808) ];

var gwanakPolygonD = new kakao.maps.Polygon({
    path: gwanakPolygonDPath,
    fillColor: '#009EDF',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 서초구 다각형 생성(22연령)
var seochoPolygonDPath = [
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.5234361, 127.0064445),
new kakao.maps.LatLng(37.5194968, 127.0007883),
new kakao.maps.LatLng(37.5131024, 126.9906716),
new kakao.maps.LatLng(37.5065431, 126.9855327),
new kakao.maps.LatLng(37.5065363, 126.9804067),
new kakao.maps.LatLng(37.5026966, 126.9805363),
new kakao.maps.LatLng(37.499859, 126.9853872),
new kakao.maps.LatLng(37.4969936, 126.9829297),
new kakao.maps.LatLng(37.4770573, 126.9816808),
new kakao.maps.LatLng(37.4737189, 126.9821725),
new kakao.maps.LatLng(37.4698246, 126.9845159),
new kakao.maps.LatLng(37.4676122, 126.9873023),
new kakao.maps.LatLng(37.4639986, 126.988344),
new kakao.maps.LatLng(37.4600297, 126.9875747),
new kakao.maps.LatLng(37.4581534, 126.9886043),
new kakao.maps.LatLng(37.4614959, 126.9933541),
new kakao.maps.LatLng(37.4618734, 126.9967683),
new kakao.maps.LatLng(37.464215, 126.9972632),
new kakao.maps.LatLng(37.4666083, 126.9962307),
new kakao.maps.LatLng(37.4671797, 126.9969853),
new kakao.maps.LatLng(37.4671246, 127.0027346),
new kakao.maps.LatLng(37.4657636, 127.0049273),
new kakao.maps.LatLng(37.4640347, 127.0045148),
new kakao.maps.LatLng(37.4578423, 127.0086622),
new kakao.maps.LatLng(37.4554428, 127.010818),
new kakao.maps.LatLng(37.4548611, 127.0145094),
new kakao.maps.LatLng(37.4561351, 127.017545),
new kakao.maps.LatLng(37.4556938, 127.0192823),
new kakao.maps.LatLng(37.4572538, 127.022851),
new kakao.maps.LatLng(37.4574817, 127.0252753),
new kakao.maps.LatLng(37.4596417, 127.0265719),
new kakao.maps.LatLng(37.4633413, 127.0296306),
new kakao.maps.LatLng(37.4653746, 127.0295269),
new kakao.maps.LatLng(37.4656262, 127.0311954),
new kakao.maps.LatLng(37.4641547, 127.0346931),
new kakao.maps.LatLng(37.4612371, 127.0337319),
new kakao.maps.LatLng(37.4601754, 127.0349239),
new kakao.maps.LatLng(37.4578668, 127.0350694),
new kakao.maps.LatLng(37.455203, 127.0371709),
new kakao.maps.LatLng(37.4526095, 127.0347723),
new kakao.maps.LatLng(37.4514669, 127.0364748),
new kakao.maps.LatLng(37.4494531, 127.037741),
new kakao.maps.LatLng(37.4464509, 127.0372545),
new kakao.maps.LatLng(37.4451803, 127.0382301),
new kakao.maps.LatLng(37.4432667, 127.0374826),
new kakao.maps.LatLng(37.4410155, 127.0352603),
new kakao.maps.LatLng(37.4391373, 127.0356865),
new kakao.maps.LatLng(37.4383913, 127.0371471),
new kakao.maps.LatLng(37.4383412, 127.0401422),
new kakao.maps.LatLng(37.4335915, 127.0463942),
new kakao.maps.LatLng(37.4307906, 127.0473967),
new kakao.maps.LatLng(37.4303374, 127.0493227),
new kakao.maps.LatLng(37.4284561, 127.0520464),
new kakao.maps.LatLng(37.4301499, 127.0578618),
new kakao.maps.LatLng(37.4301216, 127.0608665),
new kakao.maps.LatLng(37.4290228, 127.0656551),
new kakao.maps.LatLng(37.4307189, 127.0683088),
new kakao.maps.LatLng(37.4308177, 127.0712064),
new kakao.maps.LatLng(37.4324169, 127.0705709),
new kakao.maps.LatLng(37.4358635, 127.0714392),
new kakao.maps.LatLng(37.4374234, 127.0738798),
new kakao.maps.LatLng(37.4388568, 127.0720075),
new kakao.maps.LatLng(37.4415239, 127.0716257),
new kakao.maps.LatLng(37.442133, 127.0761442),
new kakao.maps.LatLng(37.4410297, 127.0803008),
new kakao.maps.LatLng(37.4413384, 127.0821566),
new kakao.maps.LatLng(37.4439083, 127.083954),
new kakao.maps.LatLng(37.4442491, 127.0865305),
new kakao.maps.LatLng(37.4454138, 127.0882762),
new kakao.maps.LatLng(37.4486278, 127.0883265),
new kakao.maps.LatLng(37.4527827, 127.0909588),
new kakao.maps.LatLng(37.4536339, 127.0927253),
new kakao.maps.LatLng(37.4558885, 127.0935402),
new kakao.maps.LatLng(37.4565198, 127.095769),
new kakao.maps.LatLng(37.4562188, 127.0990955),
new kakao.maps.LatLng(37.4585341, 127.101167)
];

var seochoPolygonD = new kakao.maps.Polygon({
    path: seochoPolygonDPath,
    fillColor: '#7D160F',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강남구 다각형 생성(22연령)
var gangnamPolygonDPath = [
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5286757, 127.0551335),
new kakao.maps.LatLng(37.5342726, 127.0460023),
new kakao.maps.LatLng(37.5358577, 127.0396637),
new kakao.maps.LatLng(37.5358238, 127.0211723),
new kakao.maps.LatLng(37.5342595, 127.0177593),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.4600566, 127.1039435),
new kakao.maps.LatLng(37.4621594, 127.1043465),
new kakao.maps.LatLng(37.4624345, 127.1064566),
new kakao.maps.LatLng(37.4616446, 127.1118201),
new kakao.maps.LatLng(37.4598893, 127.1134332),
new kakao.maps.LatLng(37.458634, 127.116896),
new kakao.maps.LatLng(37.4622006, 127.1174754),
new kakao.maps.LatLng(37.464372, 127.12144),
new kakao.maps.LatLng(37.4665205, 127.1242057)
];

var gangnamPolygonD = new kakao.maps.Polygon({
    path: gangnamPolygonDPath,
    fillColor: '#7D160F',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 송파구 다각형 생성(22연령)
var songpaPolygonDPath = [
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5414079, 127.1082818),
new kakao.maps.LatLng(37.5270069, 127.090161),
new kakao.maps.LatLng(37.524759, 127.0856328),
new kakao.maps.LatLng(37.5229485, 127.0799746),
new kakao.maps.LatLng(37.522514, 127.0769544),
new kakao.maps.LatLng(37.523872, 127.0686631),
new kakao.maps.LatLng(37.5268818, 127.0607945),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4684191, 127.1270342),
new kakao.maps.LatLng(37.4677511, 127.1301405),
new kakao.maps.LatLng(37.4683941, 127.1327994),
new kakao.maps.LatLng(37.4697986, 127.1319826),
new kakao.maps.LatLng(37.4715382, 127.1328449),
new kakao.maps.LatLng(37.4746269, 127.1328558),
new kakao.maps.LatLng(37.4742406, 127.1354681),
new kakao.maps.LatLng(37.4739308, 127.1435264),
new kakao.maps.LatLng(37.4773315, 127.1443703),
new kakao.maps.LatLng(37.4772222, 127.1471451),
new kakao.maps.LatLng(37.4815898, 127.1474588),
new kakao.maps.LatLng(37.4840436, 127.1486828),
new kakao.maps.LatLng(37.4862358, 127.1521778),
new kakao.maps.LatLng(37.489672, 127.1585233),
new kakao.maps.LatLng(37.492048, 127.1584792),
new kakao.maps.LatLng(37.4943902, 127.1600312),
new kakao.maps.LatLng(37.4968237, 127.1597796),
new kakao.maps.LatLng(37.4995369, 127.1613552),
new kakao.maps.LatLng(37.5031794, 127.1577291),
new kakao.maps.LatLng(37.5018946, 127.1565548),
new kakao.maps.LatLng(37.5029854, 127.1521336),
new kakao.maps.LatLng(37.5046783, 127.1502631),
new kakao.maps.LatLng(37.5032338, 127.1477163),
new kakao.maps.LatLng(37.5054583, 127.1411493),
new kakao.maps.LatLng(37.5067087, 127.1415163),
new kakao.maps.LatLng(37.5085171, 127.139952),
new kakao.maps.LatLng(37.5123608, 127.1413929),
new kakao.maps.LatLng(37.5126573, 127.1435398),
new kakao.maps.LatLng(37.5156419, 127.1421313),
new kakao.maps.LatLng(37.5155915, 127.1446078),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var songpaPolygonD = new kakao.maps.Polygon({
    path: songpaPolygonDPath,
    fillColor: '#D20D14',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강동구 다각형 생성(22연령)
var gangdongPolygonDPath =[
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.5196245, 127.1447856),
new kakao.maps.LatLng(37.5219397, 127.1457414),
new kakao.maps.LatLng(37.5221448, 127.1478181),
new kakao.maps.LatLng(37.5263728, 127.1504017),
new kakao.maps.LatLng(37.5285295, 127.1526867),
new kakao.maps.LatLng(37.5319199, 127.1539334),
new kakao.maps.LatLng(37.533683, 127.1536063),
new kakao.maps.LatLng(37.5392702, 127.1576512),
new kakao.maps.LatLng(37.5411651, 127.1598933),
new kakao.maps.LatLng(37.5449999, 127.1631595),
new kakao.maps.LatLng(37.5442561, 127.1666417),
new kakao.maps.LatLng(37.5455346, 127.1721068),
new kakao.maps.LatLng(37.5452104, 127.1757181),
new kakao.maps.LatLng(37.5466816, 127.1793088),
new kakao.maps.LatLng(37.5463443, 127.1828251),
new kakao.maps.LatLng(37.5518204, 127.1829114),
new kakao.maps.LatLng(37.5528619, 127.1813807),
new kakao.maps.LatLng(37.5609928, 127.1819994),
new kakao.maps.LatLng(37.5654958, 127.179585),
new kakao.maps.LatLng(37.5689182, 127.1792158),
new kakao.maps.LatLng(37.5722139, 127.1777375),
new kakao.maps.LatLng(37.5740993, 127.17614),
new kakao.maps.LatLng(37.5783633, 127.1754421),
new kakao.maps.LatLng(37.5792655, 127.1768832),
new kakao.maps.LatLng(37.5812008, 127.1771547),
new kakao.maps.LatLng(37.5797349, 127.1738711),
new kakao.maps.LatLng(37.5786946, 127.1671595),
new kakao.maps.LatLng(37.5764649, 127.1629721),
new kakao.maps.LatLng(37.5704037, 127.1536011),
new kakao.maps.LatLng(37.5681865, 127.1493618),
new kakao.maps.LatLng(37.5682007, 127.138063),
new kakao.maps.LatLng(37.567884, 127.135692),
new kakao.maps.LatLng(37.565944, 127.1290179),
new kakao.maps.LatLng(37.5633331, 127.1234369),
new kakao.maps.LatLng(37.5592439, 127.1176932),
new kakao.maps.LatLng(37.5568724, 127.1153231),
new kakao.maps.LatLng(37.5543662, 127.1143095),
new kakao.maps.LatLng(37.5504987, 127.1115571),
new kakao.maps.LatLng(37.5469267, 127.1114708),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var gangdongPolygonD = new kakao.maps.Polygon({
    path: gangdongPolygonDPath,
    fillColor: '#E85239',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

                 // (22수준) 용산구 다각형 생성
                 var yongsanPolygonEPath = [
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.54413326436179, 127.00898460651953),
            new kakao.maps.LatLng(37.539639030116945, 127.00959054834321),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.52290225898471, 127.00614038053493),
            new kakao.maps.LatLng(37.51309192794448, 126.99070240960813),
            new kakao.maps.LatLng(37.50654651085339, 126.98553683648308),
            new kakao.maps.LatLng(37.50702053393398, 126.97524914998174),
            new kakao.maps.LatLng(37.51751820477105, 126.94988506562748),
            new kakao.maps.LatLng(37.52702918583156, 126.94987870367682),
            new kakao.maps.LatLng(37.534519656862926, 126.94481851935942),
            new kakao.maps.LatLng(37.537500243531994, 126.95335659960566),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.5541513366375, 126.9657135934734),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.5548768201904, 126.96966524449994)
        ];

        var yongsanPolygonE = new kakao.maps.Polygon({
            path: yongsanPolygonEPath,
            fillColor: '#A61914',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        // 동대문구 다각형 생성(22수준)        
        var dongdaemunPolygonEPath = [
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496),
            new kakao.maps.LatLng(37.60107201319839, 127.07287376670605),
            new kakao.maps.LatLng(37.59724304056685, 127.06949105186925),
            new kakao.maps.LatLng(37.58953367466315, 127.07030363208528),
            new kakao.maps.LatLng(37.58651213184981, 127.07264218709383),
            new kakao.maps.LatLng(37.5849555116177, 127.07216063016078),
            new kakao.maps.LatLng(37.58026781100598, 127.07619547037923),
            new kakao.maps.LatLng(37.571869232268774, 127.0782018408153),
            new kakao.maps.LatLng(37.559961773835425, 127.07239004251258),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.572878529071055, 127.04263554582458),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.57838361223621, 127.0232348231103),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5956815721534, 127.04062845365279),
            new kakao.maps.LatLng(37.5969637344377, 127.04302522879048),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.607062869017085, 127.07111288773496)
        ];

        var dongdaemunPolygonE = new kakao.maps.Polygon({
            path: dongdaemunPolygonEPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성동구 다각형 생성(22수준)
        var seungdongPolygonEPath = [
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706),
            new kakao.maps.LatLng(37.57038253579033, 127.04794980454399),
            new kakao.maps.LatLng(37.56231553903832, 127.05876047165025),
            new kakao.maps.LatLng(37.5594131360664, 127.07373408220053),
            new kakao.maps.LatLng(37.52832388381049, 127.05621773388143),
            new kakao.maps.LatLng(37.53423885672233, 127.04604398310076),
            new kakao.maps.LatLng(37.53582328355087, 127.03979942567628),
            new kakao.maps.LatLng(37.53581367627865, 127.0211714455564),
            new kakao.maps.LatLng(37.53378887274516, 127.01719284893274),
            new kakao.maps.LatLng(37.537681185520256, 127.01726163044557),
            new kakao.maps.LatLng(37.53938672166098, 127.00993448922989),
            new kakao.maps.LatLng(37.54157804358092, 127.00879872996808),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56978273516453, 127.03099733100001),
            new kakao.maps.LatLng(37.57302061077518, 127.0381755492195),
            new kakao.maps.LatLng(37.57275246810175, 127.04241813085706)
        ];

        var seungdongPolygonE = new kakao.maps.Polygon({
            path: seungdongPolygonEPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 서대문구 다각형 생성(22수준)
        var seodaemunPolygonEPath = [
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003),
            new kakao.maps.LatLng(37.5992407011344, 126.95499403097206),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.5575156365052, 126.95991288916548),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.57599550420081, 126.902091747923),
            new kakao.maps.LatLng(37.587223103650295, 126.91284666446226),
            new kakao.maps.LatLng(37.58541570520177, 126.91531241017965),
            new kakao.maps.LatLng(37.585870567159255, 126.91638068573187),
            new kakao.maps.LatLng(37.583095195853055, 126.9159399866114),
            new kakao.maps.LatLng(37.583459593417196, 126.92175886498167),
            new kakao.maps.LatLng(37.587104600730505, 126.92388813813815),
            new kakao.maps.LatLng(37.588386594820484, 126.92800815682232),
            new kakao.maps.LatLng(37.59157595859555, 126.92776504133688),
            new kakao.maps.LatLng(37.59455434247408, 126.93027139545339),
            new kakao.maps.LatLng(37.59869748704149, 126.94088480070904),
            new kakao.maps.LatLng(37.60065830191363, 126.9414041615336),
            new kakao.maps.LatLng(37.60305781086164, 126.93995273804141),
            new kakao.maps.LatLng(37.610598531321436, 126.95037536795142),
            new kakao.maps.LatLng(37.6083605525023, 126.95056259057313),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.59851932019209, 126.95347706883003)
        ];

        var seodaemunPolygonE = new kakao.maps.Polygon({
            path: seodaemunPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 종로구 다각형 생성(22수준)
        var jongnoPolygonEPath = [
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046),
            new kakao.maps.LatLng(37.632194205253654, 126.97609588529602),
            new kakao.maps.LatLng(37.629026103322374, 126.97496405167149),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.60401657024552, 126.98665951539246),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.5788668917658, 127.02140099081309),
            new kakao.maps.LatLng(37.578034045208426, 127.02313962015988),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.5681357695346, 126.99014772014593),
            new kakao.maps.LatLng(37.569315246023024, 126.9732046364419),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.57874076105342, 126.95354824618335),
            new kakao.maps.LatLng(37.581020184166476, 126.95812059678624),
            new kakao.maps.LatLng(37.59354736740056, 126.95750665936443),
            new kakao.maps.LatLng(37.595061575856455, 126.9590412421402),
            new kakao.maps.LatLng(37.59833350100327, 126.9576941779143),
            new kakao.maps.LatLng(37.59875701675023, 126.95306020161668),
            new kakao.maps.LatLng(37.602476031211225, 126.95237386792348),
            new kakao.maps.LatLng(37.60507154496655, 126.95404376087069),
            new kakao.maps.LatLng(37.60912809443569, 126.95032198271032),
            new kakao.maps.LatLng(37.615539700280216, 126.95072546923387),
            new kakao.maps.LatLng(37.62433621196653, 126.94900237336302),
            new kakao.maps.LatLng(37.62642708817027, 126.95037844036497),
            new kakao.maps.LatLng(37.629590994617104, 126.95881385457929),
            new kakao.maps.LatLng(37.629794440379136, 126.96376660599225),
            new kakao.maps.LatLng(37.632373740990175, 126.97302793692637),
            new kakao.maps.LatLng(37.631840777111364, 126.9749313865046)
        ];

        var jongnoPolygonE = new kakao.maps.Polygon({
            path: jongnoPolygonEPath,
            fillColor: '#F18077',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중구 다각형 생성(22수준)
        var jungPolygonEPath = [
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894),
            new kakao.maps.LatLng(37.54385947805103, 127.00727818360471),
            new kakao.maps.LatLng(37.546169758665414, 127.00499711608721),
            new kakao.maps.LatLng(37.54820235864802, 127.0061334023129),
            new kakao.maps.LatLng(37.550159406110104, 127.00436818301327),
            new kakao.maps.LatLng(37.549694559809545, 126.99832516302801),
            new kakao.maps.LatLng(37.54722934282707, 126.995229135048),
            new kakao.maps.LatLng(37.55368689494708, 126.98541456064552),
            new kakao.maps.LatLng(37.55320655210504, 126.97874667968763),
            new kakao.maps.LatLng(37.55522076659584, 126.97654602427454),
            new kakao.maps.LatLng(37.55308718044556, 126.97642899633566),
            new kakao.maps.LatLng(37.55487749311664, 126.97240854546743),
            new kakao.maps.LatLng(37.5548766923893, 126.9691718124876),
            new kakao.maps.LatLng(37.55566236579088, 126.9691850696746),
            new kakao.maps.LatLng(37.55155543391863, 126.96233786542686),
            new kakao.maps.LatLng(37.55498984534305, 126.96173858545431),
            new kakao.maps.LatLng(37.55695455613004, 126.96343068837372),
            new kakao.maps.LatLng(37.5590262922649, 126.9616731414449),
            new kakao.maps.LatLng(37.56197662569172, 126.96946316364357),
            new kakao.maps.LatLng(37.56582132960869, 126.96669525397355),
            new kakao.maps.LatLng(37.56824746386509, 126.96909838710842),
            new kakao.maps.LatLng(37.569485309984174, 126.97637402412326),
            new kakao.maps.LatLng(37.56810323716611, 126.98905202099309),
            new kakao.maps.LatLng(37.56961739576364, 127.00225936812329),
            new kakao.maps.LatLng(37.56966688588187, 127.0152677241078),
            new kakao.maps.LatLng(37.572022763755164, 127.0223363152772),
            new kakao.maps.LatLng(37.57190723475508, 127.02337770475695),
            new kakao.maps.LatLng(37.56973041414113, 127.0234585247501),
            new kakao.maps.LatLng(37.565200182350495, 127.02358387477513),
            new kakao.maps.LatLng(37.56505173515675, 127.02678930885806),
            new kakao.maps.LatLng(37.563390358462826, 127.02652159646888),
            new kakao.maps.LatLng(37.5607276739534, 127.02339232029838),
            new kakao.maps.LatLng(37.55779412537163, 127.0228934248264),
            new kakao.maps.LatLng(37.556850715898484, 127.01807638779917),
            new kakao.maps.LatLng(37.55264513061776, 127.01620129137214),
            new kakao.maps.LatLng(37.547466935106435, 127.00931996404753),
            new kakao.maps.LatLng(37.54502351209897, 127.00815187343248),
            new kakao.maps.LatLng(37.544062989758594, 127.00854659142894)
        ];

        var jungPolygonE = new kakao.maps.Polygon({
            path: jungPolygonEPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 광진구 다각형 생성(22수준)
        var gwangjinPolygonEPath = [
    new kakao.maps.LatLng(37.5568724, 127.1153231),
    new kakao.maps.LatLng(37.5585233, 127.113965),
    new kakao.maps.LatLng(37.5590006, 127.112297),
    new kakao.maps.LatLng(37.5585538, 127.1095286),
    new kakao.maps.LatLng(37.5564601, 127.1063932),
    new kakao.maps.LatLng(37.5595269, 127.1019134),
    new kakao.maps.LatLng(37.5616054, 127.1012509),
    new kakao.maps.LatLng(37.5643129, 127.1023143),
    new kakao.maps.LatLng(37.5701103, 127.1035059),
    new kakao.maps.LatLng(37.5714514, 127.104295),
    new kakao.maps.LatLng(37.5724694, 127.1017021),
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.5679178, 127.0768757),
    new kakao.maps.LatLng(37.5645904, 127.0740989),
    new kakao.maps.LatLng(37.5599603, 127.0723852),
    new kakao.maps.LatLng(37.559414, 127.0737358),
    new kakao.maps.LatLng(37.5393084, 127.0623676),
    new kakao.maps.LatLng(37.539291, 127.0623585),
    new kakao.maps.LatLng(37.5283299, 127.0562249),
    new kakao.maps.LatLng(37.5268818, 127.0607945),
    new kakao.maps.LatLng(37.523872, 127.0686631),
    new kakao.maps.LatLng(37.522514, 127.0769544),
    new kakao.maps.LatLng(37.5229485, 127.0799746),
    new kakao.maps.LatLng(37.524759, 127.0856328),
    new kakao.maps.LatLng(37.5270069, 127.090161),
    new kakao.maps.LatLng(37.5414079, 127.1082818),
    new kakao.maps.LatLng(37.5431669, 127.1092397),
    new kakao.maps.LatLng(37.5469267, 127.1114708),
    new kakao.maps.LatLng(37.5504987, 127.1115571),
    new kakao.maps.LatLng(37.5543662, 127.1143095),
    new kakao.maps.LatLng(37.5568724, 127.1153231)
];  
        var gwangjinPolygonE = new kakao.maps.Polygon({
            path: gwangjinPolygonEPath,
            fillColor: '#F18077',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 중랑구 다각형 생성(22수준)
        var jungnangPolygonEPath = [
    new kakao.maps.LatLng(37.5737318, 127.1008637),
    new kakao.maps.LatLng(37.5760708, 127.1011435),
    new kakao.maps.LatLng(37.578907, 127.1030254),
    new kakao.maps.LatLng(37.5805343, 127.103429),
    new kakao.maps.LatLng(37.5833044, 127.109002),
    new kakao.maps.LatLng(37.5891647, 127.1106433),
    new kakao.maps.LatLng(37.5932091, 127.1131972),
    new kakao.maps.LatLng(37.5940164, 127.1166645),
    new kakao.maps.LatLng(37.5954971, 127.1168775),
    new kakao.maps.LatLng(37.599521, 127.1140639),
    new kakao.maps.LatLng(37.6021085, 127.1157227),
    new kakao.maps.LatLng(37.6046024, 127.118047),
    new kakao.maps.LatLng(37.607613, 127.1184769),
    new kakao.maps.LatLng(37.6088335, 127.1166833),
    new kakao.maps.LatLng(37.6118276, 127.1174901),
    new kakao.maps.LatLng(37.6160155, 127.1166717),
    new kakao.maps.LatLng(37.6178884, 127.1171467),
    new kakao.maps.LatLng(37.6195377, 127.115021),
    new kakao.maps.LatLng(37.6210546, 127.110519),
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6153366, 127.0701774),
    new kakao.maps.LatLng(37.6153196, 127.0702079),
    new kakao.maps.LatLng(37.6135142, 127.0717529),
    new kakao.maps.LatLng(37.6070224, 127.0711169),
    new kakao.maps.LatLng(37.6046424, 127.0715334),
    new kakao.maps.LatLng(37.6013304, 127.0728729),
    new kakao.maps.LatLng(37.600246, 127.0724977),
    new kakao.maps.LatLng(37.5972431, 127.069494),
    new kakao.maps.LatLng(37.5951242, 127.0694344),
    new kakao.maps.LatLng(37.5919078, 127.0707184),
    new kakao.maps.LatLng(37.5899586, 127.070228),
    new kakao.maps.LatLng(37.5865116, 127.0726438),
    new kakao.maps.LatLng(37.5849569, 127.0721613),
    new kakao.maps.LatLng(37.5793357, 127.076458),
    new kakao.maps.LatLng(37.5729206, 127.0772314),
    new kakao.maps.LatLng(37.5718695, 127.0782016),
    new kakao.maps.LatLng(37.57137, 127.0833286),
    new kakao.maps.LatLng(37.5696986, 127.0904951),
    new kakao.maps.LatLng(37.57061, 127.0956175),
    new kakao.maps.LatLng(37.5737318, 127.1008637)
];

        var jungnangPolygonE = new kakao.maps.Polygon({
            path: jungnangPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 성북구 다각형 생성(22수준)
        var seongbukPolygonEPath = [
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235),
            new kakao.maps.LatLng(37.631446839436855, 126.99372381657889),
            new kakao.maps.LatLng(37.626192451322005, 126.99927047335905),
            new kakao.maps.LatLng(37.62382095469671, 127.00488450145781),
            new kakao.maps.LatLng(37.624026217174986, 127.00788862747375),
            new kakao.maps.LatLng(37.6205124078061, 127.00724034082933),
            new kakao.maps.LatLng(37.61679651952433, 127.01014412786792),
            new kakao.maps.LatLng(37.61472018601129, 127.01451127202589),
            new kakao.maps.LatLng(37.614629670135216, 127.01757841621624),
            new kakao.maps.LatLng(37.61137091590441, 127.02219857751122),
            new kakao.maps.LatLng(37.612692696824915, 127.02642583551054),
            new kakao.maps.LatLng(37.612367438936786, 127.03018593770908),
            new kakao.maps.LatLng(37.60896889076571, 127.0302525167858),
            new kakao.maps.LatLng(37.61279787695882, 127.03730791358603),
            new kakao.maps.LatLng(37.62426467261789, 127.04973339977498),
            new kakao.maps.LatLng(37.61449950127667, 127.06174181124696),
            new kakao.maps.LatLng(37.61561580859776, 127.06985247014711),
            new kakao.maps.LatLng(37.61351359068103, 127.07170798866412),
            new kakao.maps.LatLng(37.60762512162974, 127.07105453180604),
            new kakao.maps.LatLng(37.605121767227374, 127.06219611364686),
            new kakao.maps.LatLng(37.6010580545608, 127.05917142337097),
            new kakao.maps.LatLng(37.60132672748398, 127.05508130598699),
            new kakao.maps.LatLng(37.600149587503246, 127.05209540476308),
            new kakao.maps.LatLng(37.60117358544485, 127.05101351973708),
            new kakao.maps.LatLng(37.59617641777492, 127.04734129391157),
            new kakao.maps.LatLng(37.59644879095525, 127.04184728392097),
            new kakao.maps.LatLng(37.59126734230753, 127.03875553445558),
            new kakao.maps.LatLng(37.5911852565689, 127.03621919708065),
            new kakao.maps.LatLng(37.58894739851823, 127.03553876830637),
            new kakao.maps.LatLng(37.58268174514337, 127.02953994610249),
            new kakao.maps.LatLng(37.57782865303167, 127.02296295333255),
            new kakao.maps.LatLng(37.57889204835333, 127.02179043639809),
            new kakao.maps.LatLng(37.57758802896556, 127.01812215416163),
            new kakao.maps.LatLng(37.581693162424465, 127.01673289259993),
            new kakao.maps.LatLng(37.582338528091164, 127.01483104096094),
            new kakao.maps.LatLng(37.58025588757531, 127.01058748333907),
            new kakao.maps.LatLng(37.58047228501006, 127.00863575242668),
            new kakao.maps.LatLng(37.58235007703611, 127.00677925856456),
            new kakao.maps.LatLng(37.586091007146834, 127.00667090686603),
            new kakao.maps.LatLng(37.58922302426079, 127.00228260552726),
            new kakao.maps.LatLng(37.592300831997434, 127.0009511248032),
            new kakao.maps.LatLng(37.59126960661375, 126.98919808879788),
            new kakao.maps.LatLng(37.59447673441787, 126.98544283754865),
            new kakao.maps.LatLng(37.59790270809407, 126.97672287261275),
            new kakao.maps.LatLng(37.60099164566844, 126.97852019816328),
            new kakao.maps.LatLng(37.60451393107786, 126.98678626394351),
            new kakao.maps.LatLng(37.611364924201304, 126.98565700183143),
            new kakao.maps.LatLng(37.613985109550605, 126.98658977758268),
            new kakao.maps.LatLng(37.6177725051378, 126.9837302191854),
            new kakao.maps.LatLng(37.6211493968146, 126.98365245774505),
            new kakao.maps.LatLng(37.626378096236195, 126.97960492198952),
            new kakao.maps.LatLng(37.6285585388996, 126.97992605309885),
            new kakao.maps.LatLng(37.62980449548538, 126.97468284124939),
            new kakao.maps.LatLng(37.633657663246694, 126.97740053878216),
            new kakao.maps.LatLng(37.63476479485093, 126.98154674721893),
            new kakao.maps.LatLng(37.63780700422825, 126.9849494717052),
            new kakao.maps.LatLng(37.63654916557213, 126.98446028560235)
        ];

        var seongbukPolygonE = new kakao.maps.Polygon({
            path: seongbukPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강북구 다각형 생성(22수준)
        var gangbukPolygonEPath = [
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6850889, 127.0045265),
    new kakao.maps.LatLng(37.6834224, 126.9973582),
    new kakao.maps.LatLng(37.678828, 126.9929755),
    new kakao.maps.LatLng(37.6757199, 126.9931995),
    new kakao.maps.LatLng(37.672422, 126.9942076),
    new kakao.maps.LatLng(37.6678322, 126.993576),
    new kakao.maps.LatLng(37.6670301, 126.9941291),
    new kakao.maps.LatLng(37.6652317, 126.9922245),
    new kakao.maps.LatLng(37.6643912, 126.9882682),
    new kakao.maps.LatLng(37.6606003, 126.9872768),
    new kakao.maps.LatLng(37.6589432, 126.9860205),
    new kakao.maps.LatLng(37.6570035, 126.9830101),
    new kakao.maps.LatLng(37.6560387, 126.9796581),
    new kakao.maps.LatLng(37.6548152, 126.9799441),
    new kakao.maps.LatLng(37.6505404, 126.9824953),
    new kakao.maps.LatLng(37.64961, 126.9839369),
    new kakao.maps.LatLng(37.6457101, 126.9850955),
    new kakao.maps.LatLng(37.6436716, 126.9832554),
    new kakao.maps.LatLng(37.6400446, 126.9856762),
    new kakao.maps.LatLng(37.6363484, 126.9841726),
    new kakao.maps.LatLng(37.6340757, 126.9894095),
    new kakao.maps.LatLng(37.6302496, 126.9953935),
    new kakao.maps.LatLng(37.6262023, 126.999273),
    new kakao.maps.LatLng(37.625951, 127.0000402),
    new kakao.maps.LatLng(37.6259335, 127.0000628),
    new kakao.maps.LatLng(37.6242258, 127.0038971),
    new kakao.maps.LatLng(37.6240272, 127.0078883),
    new kakao.maps.LatLng(37.6208272, 127.0072158),
    new kakao.maps.LatLng(37.618622, 127.0085),
    new kakao.maps.LatLng(37.6162859, 127.0109519),
    new kakao.maps.LatLng(37.6146854, 127.0144744),
    new kakao.maps.LatLng(37.6146161, 127.0175368),
    new kakao.maps.LatLng(37.6113717, 127.0221965),
    new kakao.maps.LatLng(37.6126938, 127.0264334),
    new kakao.maps.LatLng(37.6123662, 127.0301844),
    new kakao.maps.LatLng(37.6089762, 127.0302524),
    new kakao.maps.LatLng(37.6129618, 127.0375131),
    new kakao.maps.LatLng(37.6157606, 127.0399847),
    new kakao.maps.LatLng(37.6186436, 127.0439485),
    new kakao.maps.LatLng(37.6226012, 127.0468685),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6843696, 127.0086619)
];

        var gangbukPolygonE = new kakao.maps.Polygon({
            path: gangbukPolygonEPath,
            fillColor: '#0074BD',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 도봉구 다각형 생성(22수준)
        var dobongPolygonEPath = [
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6879759, 127.0498208),
    new kakao.maps.LatLng(37.6908702, 127.0499658),
    new kakao.maps.LatLng(37.6940664, 127.0486327),
    new kakao.maps.LatLng(37.6923802, 127.0456492),
    new kakao.maps.LatLng(37.693687, 127.043083),
    new kakao.maps.LatLng(37.6952354, 127.0430909),
    new kakao.maps.LatLng(37.6952919, 127.0411383),
    new kakao.maps.LatLng(37.6926381, 127.0368093),
    new kakao.maps.LatLng(37.6918448, 127.0324625),
    new kakao.maps.LatLng(37.6930733, 127.0310969),
    new kakao.maps.LatLng(37.6962653, 127.0297701),
    new kakao.maps.LatLng(37.6992843, 127.0293125),
    new kakao.maps.LatLng(37.7009462, 127.02771),
    new kakao.maps.LatLng(37.6995947, 127.0253836),
    new kakao.maps.LatLng(37.6997207, 127.0221482),
    new kakao.maps.LatLng(37.7010174, 127.0198271),
    new kakao.maps.LatLng(37.7014553, 127.0154151),
    new kakao.maps.LatLng(37.6988007, 127.0138784),
    new kakao.maps.LatLng(37.6973775, 127.0121243),
    new kakao.maps.LatLng(37.6966991, 127.0096662),
    new kakao.maps.LatLng(37.6933154, 127.0097568),
    new kakao.maps.LatLng(37.6915772, 127.007678),
    new kakao.maps.LatLng(37.6900533, 127.0083369),
    new kakao.maps.LatLng(37.6843696, 127.0086619),
    new kakao.maps.LatLng(37.6832297, 127.0084194),
    new kakao.maps.LatLng(37.6795727, 127.0094166),
    new kakao.maps.LatLng(37.6791064, 127.0121435),
    new kakao.maps.LatLng(37.6778834, 127.0133075),
    new kakao.maps.LatLng(37.6752339, 127.0139401),
    new kakao.maps.LatLng(37.6739397, 127.0162318),
    new kakao.maps.LatLng(37.6701703, 127.0185016),
    new kakao.maps.LatLng(37.6688885, 127.018415),
    new kakao.maps.LatLng(37.6670033, 127.0157717),
    new kakao.maps.LatLng(37.6640397, 127.0153227),
    new kakao.maps.LatLng(37.6620513, 127.0167892),
    new kakao.maps.LatLng(37.6613559, 127.0146113),
    new kakao.maps.LatLng(37.6521597, 127.0124508),
    new kakao.maps.LatLng(37.650262, 127.0143181),
    new kakao.maps.LatLng(37.6497986, 127.0145468),
    new kakao.maps.LatLng(37.6486531, 127.0173122),
    new kakao.maps.LatLng(37.6490887, 127.020169),
    new kakao.maps.LatLng(37.647342, 127.0246873),
    new kakao.maps.LatLng(37.64572, 127.0258925),
    new kakao.maps.LatLng(37.6439704, 127.0291138),
    new kakao.maps.LatLng(37.6428682, 127.0308557),
    new kakao.maps.LatLng(37.6418332, 127.0324195),
    new kakao.maps.LatLng(37.637783, 127.0345662),
    new kakao.maps.LatLng(37.6360388, 127.0378191),
    new kakao.maps.LatLng(37.6342579, 127.0381418),
    new kakao.maps.LatLng(37.6321994, 127.0397646),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6858137, 127.0518033)
];

        var dobongPolygonE = new kakao.maps.Polygon({
            path: dobongPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 노원구 다각형 생성(22수준)
        var nowonPolygonEPath = [
    new kakao.maps.LatLng(37.6203794, 127.105654),
    new kakao.maps.LatLng(37.6216472, 127.1040704),
    new kakao.maps.LatLng(37.6275838, 127.1059087),
    new kakao.maps.LatLng(37.6293016, 127.1088847),
    new kakao.maps.LatLng(37.6315033, 127.1116324),
    new kakao.maps.LatLng(37.6326429, 127.1122035),
    new kakao.maps.LatLng(37.6364891, 127.1124833),
    new kakao.maps.LatLng(37.6391262, 127.1105493),
    new kakao.maps.LatLng(37.6398412, 127.1120504),
    new kakao.maps.LatLng(37.6425246, 127.1108099),
    new kakao.maps.LatLng(37.6426948, 127.1093228),
    new kakao.maps.LatLng(37.6451721, 127.1067673),
    new kakao.maps.LatLng(37.6452258, 127.1028086),
    new kakao.maps.LatLng(37.6439649, 127.0975589),
    new kakao.maps.LatLng(37.6445705, 127.09457),
    new kakao.maps.LatLng(37.6496973, 127.0924745),
    new kakao.maps.LatLng(37.6524386, 127.0940495),
    new kakao.maps.LatLng(37.6537758, 127.0930673),
    new kakao.maps.LatLng(37.6593346, 127.0912069),
    new kakao.maps.LatLng(37.6632988, 127.0941422),
    new kakao.maps.LatLng(37.6675788, 127.095017),
    new kakao.maps.LatLng(37.6687685, 127.0962455),
    new kakao.maps.LatLng(37.6727011, 127.0957715),
    new kakao.maps.LatLng(37.673564, 127.0946559),
    new kakao.maps.LatLng(37.6767064, 127.0938558),
    new kakao.maps.LatLng(37.6786397, 127.0919859),
    new kakao.maps.LatLng(37.6814411, 127.0929524),
    new kakao.maps.LatLng(37.6855375, 127.0964162),
    new kakao.maps.LatLng(37.689071, 127.095996),
    new kakao.maps.LatLng(37.6899664, 127.0930367),
    new kakao.maps.LatLng(37.6895704, 127.0905519),
    new kakao.maps.LatLng(37.6899122, 127.0865306),
    new kakao.maps.LatLng(37.6917823, 127.083905),
    new kakao.maps.LatLng(37.694269, 127.0838433),
    new kakao.maps.LatLng(37.6961376, 127.0811047),
    new kakao.maps.LatLng(37.6959864, 127.0781963),
    new kakao.maps.LatLng(37.6951465, 127.0748951),
    new kakao.maps.LatLng(37.6937786, 127.0727908),
    new kakao.maps.LatLng(37.6939832, 127.0686396),
    new kakao.maps.LatLng(37.6949371, 127.0634232),
    new kakao.maps.LatLng(37.6930035, 127.0624128),
    new kakao.maps.LatLng(37.6902838, 127.0597139),
    new kakao.maps.LatLng(37.6892048, 127.0551791),
    new kakao.maps.LatLng(37.6870667, 127.0518042),
    new kakao.maps.LatLng(37.6858137, 127.0518033),
    new kakao.maps.LatLng(37.6826012, 127.0518011),
    new kakao.maps.LatLng(37.6767311, 127.0497393),
    new kakao.maps.LatLng(37.6751822, 127.0488648),
    new kakao.maps.LatLng(37.6704967, 127.0481909),
    new kakao.maps.LatLng(37.6675842, 127.0489304),
    new kakao.maps.LatLng(37.6647972, 127.0508841),
    new kakao.maps.LatLng(37.6607039, 127.0514248),
    new kakao.maps.LatLng(37.6575052, 127.0534169),
    new kakao.maps.LatLng(37.6544827, 127.0540548),
    new kakao.maps.LatLng(37.650577, 127.0539551),
    new kakao.maps.LatLng(37.6482407, 127.0554397),
    new kakao.maps.LatLng(37.6459578, 127.0559296),
    new kakao.maps.LatLng(37.6401348, 127.0547312),
    new kakao.maps.LatLng(37.6416736, 127.0529713),
    new kakao.maps.LatLng(37.644815, 127.0513531),
    new kakao.maps.LatLng(37.6421453, 127.0490643),
    new kakao.maps.LatLng(37.6411175, 127.0465943),
    new kakao.maps.LatLng(37.6397023, 127.0467836),
    new kakao.maps.LatLng(37.6366899, 127.0450403),
    new kakao.maps.LatLng(37.6335766, 127.0440007),
    new kakao.maps.LatLng(37.6314633, 127.0416645),
    new kakao.maps.LatLng(37.6304207, 127.0425297),
    new kakao.maps.LatLng(37.6287491, 127.0443395),
    new kakao.maps.LatLng(37.6285904, 127.0447093),
    new kakao.maps.LatLng(37.6271236, 127.0476043),
    new kakao.maps.LatLng(37.624261, 127.0497308),
    new kakao.maps.LatLng(37.6197959, 127.0544081),
    new kakao.maps.LatLng(37.6174813, 127.0574206),
    new kakao.maps.LatLng(37.6142587, 127.0632852),
    new kakao.maps.LatLng(37.6157243, 127.0697122),
    new kakao.maps.LatLng(37.6154072, 127.0700951),
    new kakao.maps.LatLng(37.6164027, 127.0713855),
    new kakao.maps.LatLng(37.6171605, 127.0755336),
    new kakao.maps.LatLng(37.6191408, 127.0814034),
    new kakao.maps.LatLng(37.6202925, 127.0860726),
    new kakao.maps.LatLng(37.6196469, 127.0894525),
    new kakao.maps.LatLng(37.6180026, 127.0932157),
    new kakao.maps.LatLng(37.620394, 127.0988169),
    new kakao.maps.LatLng(37.6200246, 127.1016925),
    new kakao.maps.LatLng(37.6203794, 127.105654)
];

        var nowonPolygonE = new kakao.maps.Polygon({
            path: nowonPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 은평구 다각형 생성(22수준)
        var eunpyeongPolygonEPath = [
    new kakao.maps.LatLng(37.6295893, 126.9588137),
    new kakao.maps.LatLng(37.62973, 126.9597977),
    new kakao.maps.LatLng(37.6332338, 126.9634013),
    new kakao.maps.LatLng(37.6357828, 126.9626334),
    new kakao.maps.LatLng(37.6421387, 126.9593275),
    new kakao.maps.LatLng(37.6467834, 126.959027),
    new kakao.maps.LatLng(37.6480477, 126.9578392),
    new kakao.maps.LatLng(37.6528372, 126.9571078),
    new kakao.maps.LatLng(37.6546009, 126.9543453),
    new kakao.maps.LatLng(37.6549496, 126.9513757),
    new kakao.maps.LatLng(37.6571298, 126.9478961),
    new kakao.maps.LatLng(37.6592154, 126.9475649),
    new kakao.maps.LatLng(37.6577222, 126.9421),
    new kakao.maps.LatLng(37.6566359, 126.9401282),
    new kakao.maps.LatLng(37.6523011, 126.9371587),
    new kakao.maps.LatLng(37.6511999, 126.9357024),
    new kakao.maps.LatLng(37.6500481, 126.9296991),
    new kakao.maps.LatLng(37.6461063, 126.9241229),
    new kakao.maps.LatLng(37.6447557, 126.9137208),
    new kakao.maps.LatLng(37.6476455, 126.9095352),
    new kakao.maps.LatLng(37.6486884, 126.905964),
    new kakao.maps.LatLng(37.6462898, 126.9077049),
    new kakao.maps.LatLng(37.6442586, 126.9122604),
    new kakao.maps.LatLng(37.6385095, 126.9100918),
    new kakao.maps.LatLng(37.6353165, 126.9108542),
    new kakao.maps.LatLng(37.633398, 126.9070962),
    new kakao.maps.LatLng(37.6308672, 126.9072938),
    new kakao.maps.LatLng(37.6293276, 126.9087697),
    new kakao.maps.LatLng(37.6262657, 126.9086108),
    new kakao.maps.LatLng(37.6244956, 126.9066268),
    new kakao.maps.LatLng(37.6219415, 126.9071175),
    new kakao.maps.LatLng(37.6207039, 126.9056125),
    new kakao.maps.LatLng(37.6190745, 126.9052311),
    new kakao.maps.LatLng(37.6188394, 126.903361),
    new kakao.maps.LatLng(37.6157535, 126.9018223),
    new kakao.maps.LatLng(37.6140692, 126.9017342),
    new kakao.maps.LatLng(37.6111913, 126.9003043),
    new kakao.maps.LatLng(37.6037417, 126.9021083),
    new kakao.maps.LatLng(37.6020402, 126.8999819),
    new kakao.maps.LatLng(37.5993665, 126.9013224),
    new kakao.maps.LatLng(37.5973371, 126.9010115),
    new kakao.maps.LatLng(37.5951135, 126.9018381),
    new kakao.maps.LatLng(37.5926784, 126.8989613),
    new kakao.maps.LatLng(37.589938, 126.8997501),
    new kakao.maps.LatLng(37.5885666, 126.896859),
    new kakao.maps.LatLng(37.5890755, 126.8932905),
    new kakao.maps.LatLng(37.5885221, 126.8922355),
    new kakao.maps.LatLng(37.5885328, 126.8871589),
    new kakao.maps.LatLng(37.5895376, 126.8858088),
    new kakao.maps.LatLng(37.593639, 126.885004),
    new kakao.maps.LatLng(37.5907926, 126.8820561),
    new kakao.maps.LatLng(37.5907588, 126.882095),
    new kakao.maps.LatLng(37.588347, 126.8845533),
    new kakao.maps.LatLng(37.5876412, 126.8852568),
    new kakao.maps.LatLng(37.5870924, 126.8858291),
    new kakao.maps.LatLng(37.5860266, 126.8871243),
    new kakao.maps.LatLng(37.5858059, 126.8874045),
    new kakao.maps.LatLng(37.5815606, 126.8937787),
    new kakao.maps.LatLng(37.5794888, 126.8969354),
    new kakao.maps.LatLng(37.5782229, 126.898808),
    new kakao.maps.LatLng(37.5765458, 126.901833),
    new kakao.maps.LatLng(37.5787907, 126.9044431),
    new kakao.maps.LatLng(37.5803263, 126.9060741),
    new kakao.maps.LatLng(37.58547, 126.9115429),
    new kakao.maps.LatLng(37.5865298, 126.9124768),
    new kakao.maps.LatLng(37.5868917, 126.9126854),
    new kakao.maps.LatLng(37.5870633, 126.9127725),
    new kakao.maps.LatLng(37.5862014, 126.9151912),
    new kakao.maps.LatLng(37.5860447, 126.9155519),
    new kakao.maps.LatLng(37.5853667, 126.9160692),
    new kakao.maps.LatLng(37.5853601, 126.9160646),
    new kakao.maps.LatLng(37.5843543, 126.9156798),
    new kakao.maps.LatLng(37.5837821, 126.9157485),
    new kakao.maps.LatLng(37.5831718, 126.9164206),
    new kakao.maps.LatLng(37.58325, 126.9178162),
    new kakao.maps.LatLng(37.5829392, 126.920859),
    new kakao.maps.LatLng(37.5838591, 126.9218276),
    new kakao.maps.LatLng(37.5846767, 126.9218555),
    new kakao.maps.LatLng(37.5852834, 126.9223929),
    new kakao.maps.LatLng(37.5856304, 126.9228635),
    new kakao.maps.LatLng(37.5869714, 126.923861),
    new kakao.maps.LatLng(37.5871207, 126.9240038),
    new kakao.maps.LatLng(37.5872166, 126.9246107),
    new kakao.maps.LatLng(37.5872168, 126.9252644),
    new kakao.maps.LatLng(37.5883854, 126.928009),
    new kakao.maps.LatLng(37.5911032, 126.927947),
    new kakao.maps.LatLng(37.5915762, 126.9277682),
    new kakao.maps.LatLng(37.5945528, 126.9302704),
    new kakao.maps.LatLng(37.5962984, 126.9327954),
    new kakao.maps.LatLng(37.5974786, 126.9364086),
    new kakao.maps.LatLng(37.5976207, 126.9382703),
    new kakao.maps.LatLng(37.5987329, 126.9408662),
    new kakao.maps.LatLng(37.6006774, 126.9413766),
    new kakao.maps.LatLng(37.6013511, 126.9407255),
    new kakao.maps.LatLng(37.6049576, 126.9421378),
    new kakao.maps.LatLng(37.6086085, 126.9482139),
    new kakao.maps.LatLng(37.609399, 126.9489364),
    new kakao.maps.LatLng(37.6138494, 126.9507966),
    new kakao.maps.LatLng(37.6155379, 126.9507242),
    new kakao.maps.LatLng(37.6199205, 126.9499112),
    new kakao.maps.LatLng(37.6207316, 126.9499381),
    new kakao.maps.LatLng(37.6209324, 126.9499158),
    new kakao.maps.LatLng(37.6232616, 126.9488984),
    new kakao.maps.LatLng(37.626418, 126.9504537),
    new kakao.maps.LatLng(37.6265452, 126.9516053),
    new kakao.maps.LatLng(37.628731, 126.956889),
    new kakao.maps.LatLng(37.6295893, 126.9588137)
];

        var eunpyeongPolygonE = new kakao.maps.Polygon({
            path: eunpyeongPolygonEPath,
            fillColor: '#0074BD',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 마포구 다각형 생성(22수준)
        var mapoPolygonEPath = [
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884),
            new kakao.maps.LatLng(37.57082994377989, 126.9098094620638),
            new kakao.maps.LatLng(37.56510367293256, 126.92601582346325),
            new kakao.maps.LatLng(37.5633319104926, 126.92828128083327),
            new kakao.maps.LatLng(37.55884751347576, 126.92659242918415),
            new kakao.maps.LatLng(37.55675317809392, 126.93190919632814),
            new kakao.maps.LatLng(37.555098093384, 126.93685861757348),
            new kakao.maps.LatLng(37.55654562007193, 126.9413708153468),
            new kakao.maps.LatLng(37.557241466445234, 126.95913438471307),
            new kakao.maps.LatLng(37.55908394430372, 126.96163689468189),
            new kakao.maps.LatLng(37.55820141918588, 126.96305432966605),
            new kakao.maps.LatLng(37.554784413504734, 126.9617251098019),
            new kakao.maps.LatLng(37.548791603525764, 126.96371984820232),
            new kakao.maps.LatLng(37.54546318600178, 126.95790512689311),
            new kakao.maps.LatLng(37.54231338779177, 126.95817394011969),
            new kakao.maps.LatLng(37.539468942052544, 126.955731506394),
            new kakao.maps.LatLng(37.536292068277106, 126.95128907260018),
            new kakao.maps.LatLng(37.53569162926515, 126.94627494388307),
            new kakao.maps.LatLng(37.53377712226906, 126.94458373402794),
            new kakao.maps.LatLng(37.54135238063506, 126.93031191951576),
            new kakao.maps.LatLng(37.539036674424615, 126.9271006565075),
            new kakao.maps.LatLng(37.54143034750605, 126.9224138272872),
            new kakao.maps.LatLng(37.54141748538761, 126.90483000187002),
            new kakao.maps.LatLng(37.548015078285694, 126.89890097452322),
            new kakao.maps.LatLng(37.56300401736817, 126.86623824787709),
            new kakao.maps.LatLng(37.57178997971358, 126.85363039091744),
            new kakao.maps.LatLng(37.57379738998644, 126.85362646212587),
            new kakao.maps.LatLng(37.57747251471329, 126.864939928088),
            new kakao.maps.LatLng(37.5781913017327, 126.87625939970273),
            new kakao.maps.LatLng(37.57977132158497, 126.87767870371688),
            new kakao.maps.LatLng(37.584440882833654, 126.87653889183002),
            new kakao.maps.LatLng(37.59079311146897, 126.88205386700724),
            new kakao.maps.LatLng(37.584651324803644, 126.88883849288884)
        ];

        var mapoPolygonE = new kakao.maps.Polygon({
            path: mapoPolygonEPath,
            fillColor: '#F18077',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 양천구 다각형 생성(22수준)
        var yangcheonPolygonEPath = [
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5397562, 126.8216026),
    new kakao.maps.LatLng(37.5365431, 126.8224338),
    new kakao.maps.LatLng(37.5348887, 126.821878),
    new kakao.maps.LatLng(37.5299154, 126.8254181),
    new kakao.maps.LatLng(37.528389, 126.8279799),
    new kakao.maps.LatLng(37.5258342, 126.8281793),
    new kakao.maps.LatLng(37.5249238, 126.8264622),
    new kakao.maps.LatLng(37.5230079, 126.8251384),
    new kakao.maps.LatLng(37.5198753, 126.8255944),
    new kakao.maps.LatLng(37.516186, 126.8231123),
    new kakao.maps.LatLng(37.5130434, 126.8244262),
    new kakao.maps.LatLng(37.5090953, 126.8239041),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5187577, 126.8782517),
    new kakao.maps.LatLng(37.5203627, 126.879464),
    new kakao.maps.LatLng(37.5252536, 126.878749),
    new kakao.maps.LatLng(37.5259082, 126.8809399),
    new kakao.maps.LatLng(37.5287593, 126.8843314),
    new kakao.maps.LatLng(37.5301503, 126.8871006),
    new kakao.maps.LatLng(37.5301524, 126.8896671),
    new kakao.maps.LatLng(37.5319258, 126.8890681),
    new kakao.maps.LatLng(37.5351351, 126.8897886),
    new kakao.maps.LatLng(37.5397825, 126.8863138),
    new kakao.maps.LatLng(37.543321, 126.885088),
    new kakao.maps.LatLng(37.5481962, 126.880664),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.546944, 126.8745052)
];

        var yangcheonPolygonE = new kakao.maps.Polygon({
            path: yangcheonPolygonEPath,
            fillColor: '#E85239',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 강서구 다각형 생성(22수준)
        var gangseoPolygonEPath = [
    new kakao.maps.LatLng(37.5717904, 126.8536316),
    new kakao.maps.LatLng(37.5737991, 126.8536283),
    new kakao.maps.LatLng(37.5745142, 126.8510083),
    new kakao.maps.LatLng(37.5773942, 126.8467014),
    new kakao.maps.LatLng(37.5835872, 126.8327892),
    new kakao.maps.LatLng(37.588201, 126.8270511),
    new kakao.maps.LatLng(37.5900825, 126.8252892),
    new kakao.maps.LatLng(37.5912976, 126.822785),
    new kakao.maps.LatLng(37.5976193, 126.8139529),
    new kakao.maps.LatLng(37.5989607, 126.8113687),
    new kakao.maps.LatLng(37.604902, 126.8027567),
    new kakao.maps.LatLng(37.6024867, 126.7999484),
    new kakao.maps.LatLng(37.6013474, 126.7998667),
    new kakao.maps.LatLng(37.5998709, 126.7978909),
    new kakao.maps.LatLng(37.597712, 126.797114),
    new kakao.maps.LatLng(37.5947537, 126.797721),
    new kakao.maps.LatLng(37.5936525, 126.798726),
    new kakao.maps.LatLng(37.5913058, 126.7988344),
    new kakao.maps.LatLng(37.589326, 126.8012524),
    new kakao.maps.LatLng(37.5878099, 126.8007605),
    new kakao.maps.LatLng(37.5880729, 126.7987679),
    new kakao.maps.LatLng(37.583364, 126.7956796),
    new kakao.maps.LatLng(37.5797103, 126.7924063),
    new kakao.maps.LatLng(37.5805208, 126.7907535),
    new kakao.maps.LatLng(37.5777706, 126.790599),
    new kakao.maps.LatLng(37.5777198, 126.7893694),
    new kakao.maps.LatLng(37.5755709, 126.787642),
    new kakao.maps.LatLng(37.5735993, 126.7824424),
    new kakao.maps.LatLng(37.5692071, 126.7816643),
    new kakao.maps.LatLng(37.5672821, 126.7789707),
    new kakao.maps.LatLng(37.5670966, 126.776366),
    new kakao.maps.LatLng(37.5658733, 126.7751607),
    new kakao.maps.LatLng(37.5637152, 126.7771261),
    new kakao.maps.LatLng(37.5618635, 126.7761087),
    new kakao.maps.LatLng(37.5572273, 126.7698955),
    new kakao.maps.LatLng(37.5554503, 126.7645763),
    new kakao.maps.LatLng(37.5539545, 126.7676412),
    new kakao.maps.LatLng(37.551962, 126.7674713),
    new kakao.maps.LatLng(37.5515813, 126.7693259),
    new kakao.maps.LatLng(37.548316, 126.7717031),
    new kakao.maps.LatLng(37.5489742, 126.7752973),
    new kakao.maps.LatLng(37.54671, 126.7775751),
    new kakao.maps.LatLng(37.5460749, 126.7818371),
    new kakao.maps.LatLng(37.545997, 126.7869552),
    new kakao.maps.LatLng(37.5438485, 126.7907616),
    new kakao.maps.LatLng(37.541761, 126.7921302),
    new kakao.maps.LatLng(37.541372, 126.7949442),
    new kakao.maps.LatLng(37.5395572, 126.7938932),
    new kakao.maps.LatLng(37.5373674, 126.7939734),
    new kakao.maps.LatLng(37.5367714, 126.7961149),
    new kakao.maps.LatLng(37.5378446, 126.7994886),
    new kakao.maps.LatLng(37.5403453, 126.7988931),
    new kakao.maps.LatLng(37.5408808, 126.8008976),
    new kakao.maps.LatLng(37.5426716, 126.8016672),
    new kakao.maps.LatLng(37.5436059, 126.8068721),
    new kakao.maps.LatLng(37.5407765, 126.8125684),
    new kakao.maps.LatLng(37.5407111, 126.8222929),
    new kakao.maps.LatLng(37.5409014, 126.8228048),
    new kakao.maps.LatLng(37.5412836, 126.823927),
    new kakao.maps.LatLng(37.541608, 126.8253797),
    new kakao.maps.LatLng(37.5420442, 126.8253183),
    new kakao.maps.LatLng(37.5429246, 126.8260434),
    new kakao.maps.LatLng(37.5432691, 126.8261239),
    new kakao.maps.LatLng(37.5442556, 126.82571),
    new kakao.maps.LatLng(37.5448401, 126.8259776),
    new kakao.maps.LatLng(37.5452423, 126.8263153),
    new kakao.maps.LatLng(37.5458322, 126.8267936),
    new kakao.maps.LatLng(37.5459658, 126.8269592),
    new kakao.maps.LatLng(37.5465477, 126.8270323),
    new kakao.maps.LatLng(37.5466336, 126.827072),
    new kakao.maps.LatLng(37.5467393, 126.8271548),
    new kakao.maps.LatLng(37.5468995, 126.8274147),
    new kakao.maps.LatLng(37.547067, 126.8274061),
    new kakao.maps.LatLng(37.547512, 126.8274803),
    new kakao.maps.LatLng(37.5475335, 126.8278882),
    new kakao.maps.LatLng(37.5477078, 126.8297488),
    new kakao.maps.LatLng(37.5471712, 126.8298457),
    new kakao.maps.LatLng(37.5470957, 126.8298773),
    new kakao.maps.LatLng(37.5465553, 126.8299603),
    new kakao.maps.LatLng(37.5464585, 126.8300404),
    new kakao.maps.LatLng(37.5454869, 126.8304425),
    new kakao.maps.LatLng(37.5449417, 126.8301353),
    new kakao.maps.LatLng(37.5448428, 126.8301074),
    new kakao.maps.LatLng(37.5444384, 126.8298648),
    new kakao.maps.LatLng(37.5442661, 126.829741),
    new kakao.maps.LatLng(37.5437356, 126.8297124),
    new kakao.maps.LatLng(37.5429566, 126.8300652),
    new kakao.maps.LatLng(37.5416981, 126.8299877),
    new kakao.maps.LatLng(37.541597, 126.8300954),
    new kakao.maps.LatLng(37.5415677, 126.8301502),
    new kakao.maps.LatLng(37.5417594, 126.8305438),
    new kakao.maps.LatLng(37.5418001, 126.8327368),
    new kakao.maps.LatLng(37.541825, 126.8329298),
    new kakao.maps.LatLng(37.5418494, 126.8331024),
    new kakao.maps.LatLng(37.5417648, 126.8331291),
    new kakao.maps.LatLng(37.5412833, 126.8332805),
    new kakao.maps.LatLng(37.5411418, 126.833325),
    new kakao.maps.LatLng(37.5410921, 126.8333406),
    new kakao.maps.LatLng(37.5404357, 126.8335472),
    new kakao.maps.LatLng(37.5402035, 126.8336201),
    new kakao.maps.LatLng(37.5398421, 126.8337338),
    new kakao.maps.LatLng(37.5390677, 126.8342121),
    new kakao.maps.LatLng(37.5389691, 126.834273),
    new kakao.maps.LatLng(37.5384812, 126.8345743),
    new kakao.maps.LatLng(37.5384657, 126.8345839),
    new kakao.maps.LatLng(37.538424, 126.8346097),
    new kakao.maps.LatLng(37.5380573, 126.8348361),
    new kakao.maps.LatLng(37.5379003, 126.8349331),
    new kakao.maps.LatLng(37.5375324, 126.8351603),
    new kakao.maps.LatLng(37.5372299, 126.8352081),
    new kakao.maps.LatLng(37.5368778, 126.8351569),
    new kakao.maps.LatLng(37.5367291, 126.835111),
    new kakao.maps.LatLng(37.5366527, 126.8349285),
    new kakao.maps.LatLng(37.5353703, 126.835067),
    new kakao.maps.LatLng(37.5300504, 126.8383102),
    new kakao.maps.LatLng(37.5289981, 126.8389525),
    new kakao.maps.LatLng(37.5287247, 126.8391224),
    new kakao.maps.LatLng(37.5282529, 126.8394028),
    new kakao.maps.LatLng(37.527944, 126.8395891),
    new kakao.maps.LatLng(37.5265918, 126.8404174),
    new kakao.maps.LatLng(37.52692, 126.8430795),
    new kakao.maps.LatLng(37.5270262, 126.8437042),
    new kakao.maps.LatLng(37.5271471, 126.8444126),
    new kakao.maps.LatLng(37.5272845, 126.8452497),
    new kakao.maps.LatLng(37.5274687, 126.8463275),
    new kakao.maps.LatLng(37.5275087, 126.846564),
    new kakao.maps.LatLng(37.5275829, 126.8470023),
    new kakao.maps.LatLng(37.527622, 126.8472345),
    new kakao.maps.LatLng(37.5276928, 126.8476526),
    new kakao.maps.LatLng(37.5277643, 126.8480769),
    new kakao.maps.LatLng(37.5278198, 126.8484067),
    new kakao.maps.LatLng(37.5278969, 126.8488708),
    new kakao.maps.LatLng(37.5278983, 126.8488792),
    new kakao.maps.LatLng(37.5279588, 126.849363),
    new kakao.maps.LatLng(37.5281165, 126.8506108),
    new kakao.maps.LatLng(37.5281399, 126.8507971),
    new kakao.maps.LatLng(37.5283945, 126.8528451),
    new kakao.maps.LatLng(37.528571, 126.8542457),
    new kakao.maps.LatLng(37.5286377, 126.8547752),
    new kakao.maps.LatLng(37.5287664, 126.8558004),
    new kakao.maps.LatLng(37.528983, 126.8575701),
    new kakao.maps.LatLng(37.5290202, 126.8578705),
    new kakao.maps.LatLng(37.529154, 126.8589465),
    new kakao.maps.LatLng(37.5293093, 126.8601804),
    new kakao.maps.LatLng(37.5294795, 126.8615346),
    new kakao.maps.LatLng(37.5295183, 126.861848),
    new kakao.maps.LatLng(37.5295654, 126.8622149),
    new kakao.maps.LatLng(37.5297863, 126.8639768),
    new kakao.maps.LatLng(37.5298801, 126.8639668),
    new kakao.maps.LatLng(37.5301478, 126.863945),
    new kakao.maps.LatLng(37.5305579, 126.8639142),
    new kakao.maps.LatLng(37.5322183, 126.8637685),
    new kakao.maps.LatLng(37.5355213, 126.863484),
    new kakao.maps.LatLng(37.5356346, 126.8634738),
    new kakao.maps.LatLng(37.5361946, 126.8634416),
    new kakao.maps.LatLng(37.536285, 126.8634472),
    new kakao.maps.LatLng(37.5379425, 126.8635834),
    new kakao.maps.LatLng(37.5392288, 126.8636895),
    new kakao.maps.LatLng(37.5405532, 126.8637901),
    new kakao.maps.LatLng(37.5410951, 126.8636705),
    new kakao.maps.LatLng(37.5412422, 126.8635987),
    new kakao.maps.LatLng(37.5417175, 126.8635221),
    new kakao.maps.LatLng(37.5427144, 126.8627877),
    new kakao.maps.LatLng(37.5439341, 126.8621644),
    new kakao.maps.LatLng(37.5441519, 126.8621217),
    new kakao.maps.LatLng(37.5455338, 126.8624409),
    new kakao.maps.LatLng(37.5466271, 126.862786),
    new kakao.maps.LatLng(37.5498905, 126.8638094),
    new kakao.maps.LatLng(37.5503859, 126.8639673),
    new kakao.maps.LatLng(37.550463, 126.8639918),
    new kakao.maps.LatLng(37.5508151, 126.8641017),
    new kakao.maps.LatLng(37.551152, 126.8642069),
    new kakao.maps.LatLng(37.5510086, 126.8649908),
    new kakao.maps.LatLng(37.5509042, 126.8652213),
    new kakao.maps.LatLng(37.550393, 126.8662089),
    new kakao.maps.LatLng(37.549417, 126.8678213),
    new kakao.maps.LatLng(37.5477476, 126.8706196),
    new kakao.maps.LatLng(37.5476836, 126.8707513),
    new kakao.maps.LatLng(37.5473421, 126.8715962),
    new kakao.maps.LatLng(37.547277, 126.871801),
    new kakao.maps.LatLng(37.5471148, 126.8724301),
    new kakao.maps.LatLng(37.5470038, 126.8730766),
    new kakao.maps.LatLng(37.546945, 126.8737338),
    new kakao.maps.LatLng(37.546944, 126.8745052),
    new kakao.maps.LatLng(37.5469668, 126.8750155),
    new kakao.maps.LatLng(37.5470361, 126.8765633),
    new kakao.maps.LatLng(37.5481585, 126.8801087),
    new kakao.maps.LatLng(37.5482095, 126.8803803),
    new kakao.maps.LatLng(37.5484626, 126.8804437),
    new kakao.maps.LatLng(37.5494053, 126.8798959),
    new kakao.maps.LatLng(37.5497628, 126.8796001),
    new kakao.maps.LatLng(37.5499377, 126.8794778),
    new kakao.maps.LatLng(37.5500282, 126.8794146),
    new kakao.maps.LatLng(37.550412, 126.8791236),
    new kakao.maps.LatLng(37.5507488, 126.8788459),
    new kakao.maps.LatLng(37.5511263, 126.8787108),
    new kakao.maps.LatLng(37.5515205, 126.8781985),
    new kakao.maps.LatLng(37.5519352, 126.8780413),
    new kakao.maps.LatLng(37.5523189, 126.8780313),
    new kakao.maps.LatLng(37.5525651, 126.8780226),
    new kakao.maps.LatLng(37.5527979, 126.8780142),
    new kakao.maps.LatLng(37.5529934, 126.8780067),
    new kakao.maps.LatLng(37.5531701, 126.8779519),
    new kakao.maps.LatLng(37.5532133, 126.8779456),
    new kakao.maps.LatLng(37.5534501, 126.8779539),
    new kakao.maps.LatLng(37.5535245, 126.8780551),
    new kakao.maps.LatLng(37.553546, 126.8781144),
    new kakao.maps.LatLng(37.5535815, 126.8782443),
    new kakao.maps.LatLng(37.5533372, 126.878835),
    new kakao.maps.LatLng(37.5532765, 126.8789601),
    new kakao.maps.LatLng(37.5531512, 126.8792171),
    new kakao.maps.LatLng(37.5537026, 126.879224),
    new kakao.maps.LatLng(37.554747, 126.879237),
    new kakao.maps.LatLng(37.5550643, 126.8794927),
    new kakao.maps.LatLng(37.555305, 126.879688),
    new kakao.maps.LatLng(37.556224, 126.8804278),
    new kakao.maps.LatLng(37.5562828, 126.8804743),
    new kakao.maps.LatLng(37.5565904, 126.8798677),
    new kakao.maps.LatLng(37.5566999, 126.8796536),
    new kakao.maps.LatLng(37.5569932, 126.8790797),
    new kakao.maps.LatLng(37.5571835, 126.8787108),
    new kakao.maps.LatLng(37.5577477, 126.8776168),
    new kakao.maps.LatLng(37.5580956, 126.8769422),
    new kakao.maps.LatLng(37.5582839, 126.8765751),
    new kakao.maps.LatLng(37.5589502, 126.8752775),
    new kakao.maps.LatLng(37.5591563, 126.8748767),
    new kakao.maps.LatLng(37.5595945, 126.874025),
    new kakao.maps.LatLng(37.5596946, 126.8738248),
    new kakao.maps.LatLng(37.5601596, 126.8728588),
    new kakao.maps.LatLng(37.5605276, 126.8720972),
    new kakao.maps.LatLng(37.5609333, 126.8712519),
    new kakao.maps.LatLng(37.5615358, 126.8699951),
    new kakao.maps.LatLng(37.5619632, 126.8691064),
    new kakao.maps.LatLng(37.5621959, 126.868634),
    new kakao.maps.LatLng(37.5627029, 126.8677403),
    new kakao.maps.LatLng(37.5629894, 126.8672261),
    new kakao.maps.LatLng(37.5632825, 126.8666958),
    new kakao.maps.LatLng(37.5637559, 126.8658888),
    new kakao.maps.LatLng(37.5640521, 126.8654083),
    new kakao.maps.LatLng(37.5644624, 126.8647347),
    new kakao.maps.LatLng(37.5647185, 126.8643124),
    new kakao.maps.LatLng(37.5649731, 126.8639165),
    new kakao.maps.LatLng(37.5650512, 126.8637912),
    new kakao.maps.LatLng(37.5652642, 126.8634888),
    new kakao.maps.LatLng(37.5653859, 126.8633098),
    new kakao.maps.LatLng(37.5654471, 126.8632313),
    new kakao.maps.LatLng(37.5655495, 126.8630904),
    new kakao.maps.LatLng(37.5657186, 126.8628754),
    new kakao.maps.LatLng(37.5660443, 126.8624873),
    new kakao.maps.LatLng(37.5663031, 126.8621474),
    new kakao.maps.LatLng(37.5663376, 126.8621034),
    new kakao.maps.LatLng(37.5664484, 126.8619718),
    new kakao.maps.LatLng(37.5667462, 126.861637),
    new kakao.maps.LatLng(37.5672618, 126.8610683),
    new kakao.maps.LatLng(37.5675217, 126.8607424),
    new kakao.maps.LatLng(37.5676648, 126.8605839),
    new kakao.maps.LatLng(37.5679501, 126.8602879),
    new kakao.maps.LatLng(37.5682635, 126.8599471),
    new kakao.maps.LatLng(37.5686039, 126.8595982),
    new kakao.maps.LatLng(37.5688681, 126.8592962),
    new kakao.maps.LatLng(37.5693278, 126.8588345),
    new kakao.maps.LatLng(37.5695699, 126.8585727),
    new kakao.maps.LatLng(37.5700741, 126.8580604),
    new kakao.maps.LatLng(37.5702804, 126.8578288),
    new kakao.maps.LatLng(37.5704464, 126.8576497),
    new kakao.maps.LatLng(37.5705987, 126.8574919),
    new kakao.maps.LatLng(37.5708578, 126.8572342),
    new kakao.maps.LatLng(37.5710034, 126.8571121),
    new kakao.maps.LatLng(37.5712288, 126.8569134),
    new kakao.maps.LatLng(37.5715422, 126.8566245),
    new kakao.maps.LatLng(37.5717665, 126.8564237),
    new kakao.maps.LatLng(37.5717904, 126.8536316)
];

        var gangseoPolygonE = new kakao.maps.Polygon({
            path: gangseoPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

        // 구로구 다각형 생성(22수준)
        var guroPolygonEPath = [
    new kakao.maps.LatLng(37.4849988, 126.9031946),
    new kakao.maps.LatLng(37.4869351, 126.8981442),
    new kakao.maps.LatLng(37.4893387, 126.896124),
    new kakao.maps.LatLng(37.5033326, 126.8926737),
    new kakao.maps.LatLng(37.5050117, 126.8939767),
    new kakao.maps.LatLng(37.5103503, 126.8917119),
    new kakao.maps.LatLng(37.5132264, 126.8875197),
    new kakao.maps.LatLng(37.5138494, 126.8844331),
    new kakao.maps.LatLng(37.5164199, 126.881729),
    new kakao.maps.LatLng(37.5178764, 126.8791653),
    new kakao.maps.LatLng(37.5137411, 126.8772792),
    new kakao.maps.LatLng(37.5121917, 126.8757337),
    new kakao.maps.LatLng(37.5086763, 126.8739058),
    new kakao.maps.LatLng(37.5077134, 126.8750408),
    new kakao.maps.LatLng(37.504634, 126.8737244),
    new kakao.maps.LatLng(37.5041261, 126.8718643),
    new kakao.maps.LatLng(37.5058635, 126.8702183),
    new kakao.maps.LatLng(37.5048588, 126.8690098),
    new kakao.maps.LatLng(37.5058136, 126.8628478),
    new kakao.maps.LatLng(37.5065923, 126.8603353),
    new kakao.maps.LatLng(37.5099751, 126.8583141),
    new kakao.maps.LatLng(37.5092093, 126.855611),
    new kakao.maps.LatLng(37.510734, 126.8528445),
    new kakao.maps.LatLng(37.5101938, 126.8500454),
    new kakao.maps.LatLng(37.508931, 126.8486592),
    new kakao.maps.LatLng(37.5089676, 126.8462581),
    new kakao.maps.LatLng(37.506542, 126.8443628),
    new kakao.maps.LatLng(37.5055005, 126.8426373),
    new kakao.maps.LatLng(37.5060755, 126.8407238),
    new kakao.maps.LatLng(37.5044576, 126.83958),
    new kakao.maps.LatLng(37.5028165, 126.8353043),
    new kakao.maps.LatLng(37.5046793, 126.8320076),
    new kakao.maps.LatLng(37.5063132, 126.8306152),
    new kakao.maps.LatLng(37.5080714, 126.831063),
    new kakao.maps.LatLng(37.5088407, 126.8280927),
    new kakao.maps.LatLng(37.5083206, 126.8246943),
    new kakao.maps.LatLng(37.5076346, 126.8222152),
    new kakao.maps.LatLng(37.5056852, 126.8225503),
    new kakao.maps.LatLng(37.5022364, 126.821611),
    new kakao.maps.LatLng(37.5006401, 126.8194028),
    new kakao.maps.LatLng(37.4993555, 126.8196714),
    new kakao.maps.LatLng(37.4977435, 126.8161301),
    new kakao.maps.LatLng(37.4982134, 126.8141214),
    new kakao.maps.LatLng(37.4964818, 126.8129811),
    new kakao.maps.LatLng(37.4931969, 126.814573),
    new kakao.maps.LatLng(37.4915531, 126.817904),
    new kakao.maps.LatLng(37.4899794, 126.822762),
    new kakao.maps.LatLng(37.4877351, 126.8235061),
    new kakao.maps.LatLng(37.4854809, 126.8192969),
    new kakao.maps.LatLng(37.4816405, 126.8199827),
    new kakao.maps.LatLng(37.4791625, 126.8189971),
    new kakao.maps.LatLng(37.4763621, 126.8152952),
    new kakao.maps.LatLng(37.4747205, 126.8146459),
    new kakao.maps.LatLng(37.4732881, 126.817076),
    new kakao.maps.LatLng(37.4741192, 126.8187239),
    new kakao.maps.LatLng(37.4763553, 126.8195989),
    new kakao.maps.LatLng(37.4759897, 126.8278719),
    new kakao.maps.LatLng(37.4776512, 126.8317475),
    new kakao.maps.LatLng(37.4767532, 126.8339281),
    new kakao.maps.LatLng(37.4744809, 126.8359294),
    new kakao.maps.LatLng(37.475392, 126.8383005),
    new kakao.maps.LatLng(37.4746479, 126.8410321),
    new kakao.maps.LatLng(37.4749715, 126.8427814),
    new kakao.maps.LatLng(37.4738124, 126.8453603),
    new kakao.maps.LatLng(37.480012, 126.8459113),
    new kakao.maps.LatLng(37.48191, 126.8470155),
    new kakao.maps.LatLng(37.481827, 126.8527424),
    new kakao.maps.LatLng(37.4854067, 126.8555066),
    new kakao.maps.LatLng(37.4860846, 126.8579708),
    new kakao.maps.LatLng(37.4899682, 126.8613841),
    new kakao.maps.LatLng(37.4915699, 126.8654623),
    new kakao.maps.LatLng(37.49426, 126.8668088),
    new kakao.maps.LatLng(37.4951278, 126.8683565),
    new kakao.maps.LatLng(37.4940956, 126.8697092),
    new kakao.maps.LatLng(37.4916613, 126.8693466),
    new kakao.maps.LatLng(37.4895402, 126.8704101),
    new kakao.maps.LatLng(37.4906414, 126.8723345),
    new kakao.maps.LatLng(37.4882584, 126.8730843),
    new kakao.maps.LatLng(37.4885708, 126.8767901),
    new kakao.maps.LatLng(37.4853671, 126.8745638),
    new kakao.maps.LatLng(37.4866723, 126.8784581),
    new kakao.maps.LatLng(37.4855632, 126.8813537),
    new kakao.maps.LatLng(37.4823496, 126.886155),
    new kakao.maps.LatLng(37.4804414, 126.8877295),
    new kakao.maps.LatLng(37.4793897, 126.8898815),
    new kakao.maps.LatLng(37.4783336, 126.8964731),
    new kakao.maps.LatLng(37.4789401, 126.8989434),
    new kakao.maps.LatLng(37.4811733, 126.900064),
    new kakao.maps.LatLng(37.4849988, 126.9031946)
];

        var guroPolygonE = new kakao.maps.Polygon({
            path: guroPolygonEPath,
            fillColor: '#009EDF',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
     
        // 금천구 다각형 생성(22수준)
        var geumcheonPolygonEPath = [ new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4783336, 126.8964731), new kakao.maps.LatLng(37.4793897, 126.8898815), new kakao.maps.LatLng(37.4804414, 126.8877295), new kakao.maps.LatLng(37.4823496, 126.886155), new kakao.maps.LatLng(37.4855632, 126.8813537), new kakao.maps.LatLng(37.4866723, 126.8784581), new kakao.maps.LatLng(37.4853671, 126.8745638), new kakao.maps.LatLng(37.4852298, 126.8718245), new kakao.maps.LatLng(37.4836436, 126.8728822), new kakao.maps.LatLng(37.4771039, 126.8759855), new kakao.maps.LatLng(37.4738278, 126.8780112), new kakao.maps.LatLng(37.4694169, 126.8815927), new kakao.maps.LatLng(37.4684591, 126.881631), new kakao.maps.LatLng(37.4665184, 126.8842988), new kakao.maps.LatLng(37.4643925, 126.8827454), new kakao.maps.LatLng(37.4627255, 126.884317), new kakao.maps.LatLng(37.4627551, 126.8861117), new kakao.maps.LatLng(37.4575101, 126.8858806), new kakao.maps.LatLng(37.4561777, 126.8863993), new kakao.maps.LatLng(37.4544844, 126.8892662), new kakao.maps.LatLng(37.4524961, 126.8903312), new kakao.maps.LatLng(37.451995, 126.8927328), new kakao.maps.LatLng(37.4527181, 126.8939824), new kakao.maps.LatLng(37.4484134, 126.8959156), new kakao.maps.LatLng(37.4466982, 126.8946497), new kakao.maps.LatLng(37.4454288, 126.8972601), new kakao.maps.LatLng(37.4369929, 126.9008673), new kakao.maps.LatLng(37.4358535, 126.902834), new kakao.maps.LatLng(37.4340675, 126.9029873), new kakao.maps.LatLng(37.4338646, 126.9094057), new kakao.maps.LatLng(37.4361712, 126.9113332), new kakao.maps.LatLng(37.4385546, 126.912294), new kakao.maps.LatLng(37.4400154, 126.9161336), new kakao.maps.LatLng(37.439825, 126.9192897), new kakao.maps.LatLng(37.444041, 126.9227625), new kakao.maps.LatLng(37.4457729, 126.923253), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4789401, 126.8989434) ];

        var geumcheonPolygonE = new kakao.maps.Polygon({
            path: geumcheonPolygonEPath,
            fillColor: '#0074BD',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

                // 영등포구 다각형 생성(22비율)
        var yeongdeungpoPolygonEPath = [ new kakao.maps.LatLng(37.5339056, 126.9446791), new kakao.maps.LatLng(37.5378354, 126.938558), new kakao.maps.LatLng(37.5405306, 126.9328982), new kakao.maps.LatLng(37.5413625, 126.9303377), new kakao.maps.LatLng(37.5390762, 126.9276653), new kakao.maps.LatLng(37.5397435, 126.9248228), new kakao.maps.LatLng(37.5414296, 126.922414), new kakao.maps.LatLng(37.5414165, 126.9048307), new kakao.maps.LatLng(37.5480079, 126.898943), new kakao.maps.LatLng(37.5494341, 126.8946416), new kakao.maps.LatLng(37.5523, 126.8881084), new kakao.maps.LatLng(37.5558475, 126.88131), new kakao.maps.LatLng(37.556224, 126.8804278), new kakao.maps.LatLng(37.555305, 126.879688), new kakao.maps.LatLng(37.5550643, 126.8794927), new kakao.maps.LatLng(37.554747, 126.879237), new kakao.maps.LatLng(37.5537026, 126.879224), new kakao.maps.LatLng(37.5531512, 126.8792171), new kakao.maps.LatLng(37.5532765, 126.8789601), new kakao.maps.LatLng(37.5533372, 126.878835), new kakao.maps.LatLng(37.5535815, 126.8782443), new kakao.maps.LatLng(37.553546, 126.8781144), new kakao.maps.LatLng(37.5535245, 126.8780551), new kakao.maps.LatLng(37.5534501, 126.8779539), new kakao.maps.LatLng(37.5532133, 126.8779456), new kakao.maps.LatLng(37.5531701, 126.8779519), new kakao.maps.LatLng(37.5529934, 126.8780067), new kakao.maps.LatLng(37.5527979, 126.8780142), new kakao.maps.LatLng(37.5525651, 126.8780226), new kakao.maps.LatLng(37.5523189, 126.8780313), new kakao.maps.LatLng(37.5519352, 126.8780413), new kakao.maps.LatLng(37.5515205, 126.8781985), new kakao.maps.LatLng(37.5511263, 126.8785301), new kakao.maps.LatLng(37.5507488, 126.8788459), new kakao.maps.LatLng(37.550412, 126.8791236), new kakao.maps.LatLng(37.5500282, 126.8794146), new kakao.maps.LatLng(37.5499377, 126.8794778), new kakao.maps.LatLng(37.5497628, 126.8796001), new kakao.maps.LatLng(37.5494053, 126.8798959), new kakao.maps.LatLng(37.5484626, 126.8804437), new kakao.maps.LatLng(37.5481962, 126.880664), new kakao.maps.LatLng(37.543321, 126.885088), new kakao.maps.LatLng(37.5397825, 126.8863138), new kakao.maps.LatLng(37.5351351, 126.8897886), new kakao.maps.LatLng(37.5319258, 126.8890681), new kakao.maps.LatLng(37.5301524, 126.8896671), new kakao.maps.LatLng(37.5301503, 126.8871006), new kakao.maps.LatLng(37.5287593, 126.8843314), new kakao.maps.LatLng(37.5259082, 126.8809399), new kakao.maps.LatLng(37.5252536, 126.878749), new kakao.maps.LatLng(37.5203627, 126.879464), new kakao.maps.LatLng(37.5187577, 126.8782517), new kakao.maps.LatLng(37.5178764, 126.8791653), new kakao.maps.LatLng(37.5164199, 126.881729), new kakao.maps.LatLng(37.5138494, 126.8844331), new kakao.maps.LatLng(37.5132264, 126.8875197), new kakao.maps.LatLng(37.5103503, 126.8917119), new kakao.maps.LatLng(37.5050117, 126.8939767), new kakao.maps.LatLng(37.5033326, 126.8926737), new kakao.maps.LatLng(37.4893387, 126.896124), new kakao.maps.LatLng(37.4869351, 126.8981442), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4938221, 126.9104722), new kakao.maps.LatLng(37.4964189, 126.9129118), new kakao.maps.LatLng(37.4975997, 126.9194077), new kakao.maps.LatLng(37.5125265, 126.9253894), new kakao.maps.LatLng(37.5127969, 126.9267906), new kakao.maps.LatLng(37.5155543, 126.9268588), new kakao.maps.LatLng(37.5155752, 126.9323857), new kakao.maps.LatLng(37.5160787, 126.9392792), new kakao.maps.LatLng(37.5175262, 126.9498866), new kakao.maps.LatLng(37.5270289, 126.94988), new kakao.maps.LatLng(37.5339056, 126.9446791) ];

        var yeongdeungpoPolygonE = new kakao.maps.Polygon({
            path: yeongdeungpoPolygonEPath,
            fillColor: '#E85239',
            fillOpacity: 0.8,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });
        
                // 동작구 다각형 생성(22수준)
                var dongjakPolygonEPath = [
    new kakao.maps.LatLng(37.5065363, 126.9804067),
    new kakao.maps.LatLng(37.5070128, 126.9752589),
    new kakao.maps.LatLng(37.5108166, 126.9649636),
    new kakao.maps.LatLng(37.5135025, 126.9612002),
    new kakao.maps.LatLng(37.516065, 126.9547037),
    new kakao.maps.LatLng(37.5175262, 126.9498866),
    new kakao.maps.LatLng(37.5160787, 126.9392792),
    new kakao.maps.LatLng(37.5155752, 126.9323857),
    new kakao.maps.LatLng(37.5155543, 126.9268588),
    new kakao.maps.LatLng(37.5127969, 126.9267906),
    new kakao.maps.LatLng(37.5125265, 126.9253894),
    new kakao.maps.LatLng(37.4975997, 126.9194077),
    new kakao.maps.LatLng(37.4964189, 126.9129118),
    new kakao.maps.LatLng(37.4938221, 126.9104722),
    new kakao.maps.LatLng(37.4850028, 126.9031989),
    new kakao.maps.LatLng(37.4849606, 126.9060977),
    new kakao.maps.LatLng(37.4865116, 126.911921),
    new kakao.maps.LatLng(37.4880073, 126.9135728),
    new kakao.maps.LatLng(37.489548, 126.9166515),
    new kakao.maps.LatLng(37.4902759, 126.9194523),
    new kakao.maps.LatLng(37.4899637, 126.924155),
    new kakao.maps.LatLng(37.4927983, 126.925577),
    new kakao.maps.LatLng(37.4949943, 126.9274611),
    new kakao.maps.LatLng(37.4932585, 126.9313461),
    new kakao.maps.LatLng(37.493189, 126.933849),
    new kakao.maps.LatLng(37.4919697, 126.9365336),
    new kakao.maps.LatLng(37.4929037, 126.9399265),
    new kakao.maps.LatLng(37.4921435, 126.9426218),
    new kakao.maps.LatLng(37.494039, 126.9471828),
    new kakao.maps.LatLng(37.4922055, 126.9516974),
    new kakao.maps.LatLng(37.4906416, 126.9537273),
    new kakao.maps.LatLng(37.4919773, 126.9574784),
    new kakao.maps.LatLng(37.4936159, 126.9589433),
    new kakao.maps.LatLng(37.4928741, 126.9613777),
    new kakao.maps.LatLng(37.4908252, 126.9607812),
    new kakao.maps.LatLng(37.4886278, 126.9619669),
    new kakao.maps.LatLng(37.4851775, 126.9619872),
    new kakao.maps.LatLng(37.4835752, 126.96107),
    new kakao.maps.LatLng(37.4798186, 126.9644275),
    new kakao.maps.LatLng(37.4789597, 126.9663255),
    new kakao.maps.LatLng(37.4753765, 126.9705226),
    new kakao.maps.LatLng(37.476201, 126.9742856),
    new kakao.maps.LatLng(37.4770573, 126.9816808),
    new kakao.maps.LatLng(37.4969936, 126.9829297),
    new kakao.maps.LatLng(37.499859, 126.9853872),
    new kakao.maps.LatLng(37.5026966, 126.9805363),
    new kakao.maps.LatLng(37.5065363, 126.9804067)
];

        var dongjakPolygonE = new kakao.maps.Polygon({
            path: dongjakPolygonEPath,
            fillColor: '#E61E2B',
            fillOpacity: 0.5,
            strokeWeight: 2,
            strokeColor: '#FFFFFF',
            strokeOpacity: 0.9,
            strokeStyle: 'solid'
        });

// 관악구 다각형 생성(22수준)
var gwanakPolygonEPath = [ new kakao.maps.LatLng(37.4770573, 126.9816808), new kakao.maps.LatLng(37.476201, 126.9742856), new kakao.maps.LatLng(37.4753765, 126.9705226), new kakao.maps.LatLng(37.4789597, 126.9663255), new kakao.maps.LatLng(37.4798186, 126.9644275), new kakao.maps.LatLng(37.4835752, 126.96107), new kakao.maps.LatLng(37.4851775, 126.9619872), new kakao.maps.LatLng(37.4886278, 126.9619669), new kakao.maps.LatLng(37.4908252, 126.9607812), new kakao.maps.LatLng(37.4928741, 126.9613777), new kakao.maps.LatLng(37.4936159, 126.9589433), new kakao.maps.LatLng(37.4919773, 126.9574784), new kakao.maps.LatLng(37.4906416, 126.9537273), new kakao.maps.LatLng(37.4922055, 126.9516974), new kakao.maps.LatLng(37.494039, 126.9471828), new kakao.maps.LatLng(37.4921435, 126.9426218), new kakao.maps.LatLng(37.4929037, 126.9399265), new kakao.maps.LatLng(37.4919697, 126.9365336), new kakao.maps.LatLng(37.493189, 126.933849), new kakao.maps.LatLng(37.4932585, 126.9313461), new kakao.maps.LatLng(37.4949943, 126.9274611), new kakao.maps.LatLng(37.4927983, 126.925577), new kakao.maps.LatLng(37.4899637, 126.924155), new kakao.maps.LatLng(37.4902759, 126.9194523), new kakao.maps.LatLng(37.489548, 126.9166515), new kakao.maps.LatLng(37.4880073, 126.9135728), new kakao.maps.LatLng(37.4865116, 126.911921), new kakao.maps.LatLng(37.4849606, 126.9060977), new kakao.maps.LatLng(37.4850028, 126.9031989), new kakao.maps.LatLng(37.4849988, 126.9031946), new kakao.maps.LatLng(37.4811733, 126.900064), new kakao.maps.LatLng(37.4789401, 126.8989434), new kakao.maps.LatLng(37.4807661, 126.9097859), new kakao.maps.LatLng(37.4790835, 126.90863), new kakao.maps.LatLng(37.4780046, 126.909481), new kakao.maps.LatLng(37.477821, 126.911834), new kakao.maps.LatLng(37.4738628, 126.911043), new kakao.maps.LatLng(37.4726863, 126.9081997), new kakao.maps.LatLng(37.4658624, 126.9123481), new kakao.maps.LatLng(37.4616241, 126.9144014), new kakao.maps.LatLng(37.4579053, 126.91403), new kakao.maps.LatLng(37.4573126, 126.9149814), new kakao.maps.LatLng(37.4566274, 126.9221867), new kakao.maps.LatLng(37.4542163, 126.9233224), new kakao.maps.LatLng(37.4525375, 126.9262751), new kakao.maps.LatLng(37.4502126, 126.9283984), new kakao.maps.LatLng(37.4483842, 126.9301661), new kakao.maps.LatLng(37.445463, 126.9305669), new kakao.maps.LatLng(37.4417395, 126.9366582), new kakao.maps.LatLng(37.4402029, 126.9378509), new kakao.maps.LatLng(37.4373807, 126.9377535), new kakao.maps.LatLng(37.4357034, 126.9402441), new kakao.maps.LatLng(37.4373944, 126.9414554), new kakao.maps.LatLng(37.4370754, 126.9451252), new kakao.maps.LatLng(37.4387126, 126.9483629), new kakao.maps.LatLng(37.4382501, 126.9492839), new kakao.maps.LatLng(37.4392385, 126.9523939), new kakao.maps.LatLng(37.4387351, 126.9551493), new kakao.maps.LatLng(37.4391229, 126.9589137), new kakao.maps.LatLng(37.4404007, 126.9600556), new kakao.maps.LatLng(37.4402806, 126.9629426), new kakao.maps.LatLng(37.4420397, 126.9646338), new kakao.maps.LatLng(37.4462673, 126.9642894), new kakao.maps.LatLng(37.4483804, 126.9676626), new kakao.maps.LatLng(37.4494526, 126.9705691), new kakao.maps.LatLng(37.4516571, 126.9718463), new kakao.maps.LatLng(37.454323, 126.9746584), new kakao.maps.LatLng(37.4556507, 126.978552), new kakao.maps.LatLng(37.4558313, 126.9824203), new kakao.maps.LatLng(37.4568271, 126.9828879), new kakao.maps.LatLng(37.4572124, 126.9866124), new kakao.maps.LatLng(37.4581534, 126.9886043), new kakao.maps.LatLng(37.4600297, 126.9875747), new kakao.maps.LatLng(37.4639986, 126.988344), new kakao.maps.LatLng(37.4676122, 126.9873023), new kakao.maps.LatLng(37.4698246, 126.9845159), new kakao.maps.LatLng(37.4737189, 126.9821725), new kakao.maps.LatLng(37.4770573, 126.9816808) ];

var gwanakPolygonE = new kakao.maps.Polygon({
    path: gwanakPolygonDPath,
    fillColor: '#009EDF',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 서초구 다각형 생성(22수준)
var seochoPolygonEPath = [
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.5234361, 127.0064445),
new kakao.maps.LatLng(37.5194968, 127.0007883),
new kakao.maps.LatLng(37.5131024, 126.9906716),
new kakao.maps.LatLng(37.5065431, 126.9855327),
new kakao.maps.LatLng(37.5065363, 126.9804067),
new kakao.maps.LatLng(37.5026966, 126.9805363),
new kakao.maps.LatLng(37.499859, 126.9853872),
new kakao.maps.LatLng(37.4969936, 126.9829297),
new kakao.maps.LatLng(37.4770573, 126.9816808),
new kakao.maps.LatLng(37.4737189, 126.9821725),
new kakao.maps.LatLng(37.4698246, 126.9845159),
new kakao.maps.LatLng(37.4676122, 126.9873023),
new kakao.maps.LatLng(37.4639986, 126.988344),
new kakao.maps.LatLng(37.4600297, 126.9875747),
new kakao.maps.LatLng(37.4581534, 126.9886043),
new kakao.maps.LatLng(37.4614959, 126.9933541),
new kakao.maps.LatLng(37.4618734, 126.9967683),
new kakao.maps.LatLng(37.464215, 126.9972632),
new kakao.maps.LatLng(37.4666083, 126.9962307),
new kakao.maps.LatLng(37.4671797, 126.9969853),
new kakao.maps.LatLng(37.4671246, 127.0027346),
new kakao.maps.LatLng(37.4657636, 127.0049273),
new kakao.maps.LatLng(37.4640347, 127.0045148),
new kakao.maps.LatLng(37.4578423, 127.0086622),
new kakao.maps.LatLng(37.4554428, 127.010818),
new kakao.maps.LatLng(37.4548611, 127.0145094),
new kakao.maps.LatLng(37.4561351, 127.017545),
new kakao.maps.LatLng(37.4556938, 127.0192823),
new kakao.maps.LatLng(37.4572538, 127.022851),
new kakao.maps.LatLng(37.4574817, 127.0252753),
new kakao.maps.LatLng(37.4596417, 127.0265719),
new kakao.maps.LatLng(37.4633413, 127.0296306),
new kakao.maps.LatLng(37.4653746, 127.0295269),
new kakao.maps.LatLng(37.4656262, 127.0311954),
new kakao.maps.LatLng(37.4641547, 127.0346931),
new kakao.maps.LatLng(37.4612371, 127.0337319),
new kakao.maps.LatLng(37.4601754, 127.0349239),
new kakao.maps.LatLng(37.4578668, 127.0350694),
new kakao.maps.LatLng(37.455203, 127.0371709),
new kakao.maps.LatLng(37.4526095, 127.0347723),
new kakao.maps.LatLng(37.4514669, 127.0364748),
new kakao.maps.LatLng(37.4494531, 127.037741),
new kakao.maps.LatLng(37.4464509, 127.0372545),
new kakao.maps.LatLng(37.4451803, 127.0382301),
new kakao.maps.LatLng(37.4432667, 127.0374826),
new kakao.maps.LatLng(37.4410155, 127.0352603),
new kakao.maps.LatLng(37.4391373, 127.0356865),
new kakao.maps.LatLng(37.4383913, 127.0371471),
new kakao.maps.LatLng(37.4383412, 127.0401422),
new kakao.maps.LatLng(37.4335915, 127.0463942),
new kakao.maps.LatLng(37.4307906, 127.0473967),
new kakao.maps.LatLng(37.4303374, 127.0493227),
new kakao.maps.LatLng(37.4284561, 127.0520464),
new kakao.maps.LatLng(37.4301499, 127.0578618),
new kakao.maps.LatLng(37.4301216, 127.0608665),
new kakao.maps.LatLng(37.4290228, 127.0656551),
new kakao.maps.LatLng(37.4307189, 127.0683088),
new kakao.maps.LatLng(37.4308177, 127.0712064),
new kakao.maps.LatLng(37.4324169, 127.0705709),
new kakao.maps.LatLng(37.4358635, 127.0714392),
new kakao.maps.LatLng(37.4374234, 127.0738798),
new kakao.maps.LatLng(37.4388568, 127.0720075),
new kakao.maps.LatLng(37.4415239, 127.0716257),
new kakao.maps.LatLng(37.442133, 127.0761442),
new kakao.maps.LatLng(37.4410297, 127.0803008),
new kakao.maps.LatLng(37.4413384, 127.0821566),
new kakao.maps.LatLng(37.4439083, 127.083954),
new kakao.maps.LatLng(37.4442491, 127.0865305),
new kakao.maps.LatLng(37.4454138, 127.0882762),
new kakao.maps.LatLng(37.4486278, 127.0883265),
new kakao.maps.LatLng(37.4527827, 127.0909588),
new kakao.maps.LatLng(37.4536339, 127.0927253),
new kakao.maps.LatLng(37.4558885, 127.0935402),
new kakao.maps.LatLng(37.4565198, 127.095769),
new kakao.maps.LatLng(37.4562188, 127.0990955),
new kakao.maps.LatLng(37.4585341, 127.101167)
];

var seochoPolygonE = new kakao.maps.Polygon({
    path: seochoPolygonEPath,
    fillColor: '#7D160F',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강남구 다각형 생성(22수준)
var gangnamPolygonEPath = [
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5286757, 127.0551335),
new kakao.maps.LatLng(37.5342726, 127.0460023),
new kakao.maps.LatLng(37.5358577, 127.0396637),
new kakao.maps.LatLng(37.5358238, 127.0211723),
new kakao.maps.LatLng(37.5342595, 127.0177593),
new kakao.maps.LatLng(37.5308993, 127.0137073),
new kakao.maps.LatLng(37.52974, 127.0126563),
new kakao.maps.LatLng(37.5260027, 127.0163404),
new kakao.maps.LatLng(37.5248454, 127.0152308),
new kakao.maps.LatLng(37.521812, 127.0178222),
new kakao.maps.LatLng(37.5127991, 127.0205151),
new kakao.maps.LatLng(37.4843691, 127.0340872),
new kakao.maps.LatLng(37.4852405, 127.0416088),
new kakao.maps.LatLng(37.4775193, 127.0450987),
new kakao.maps.LatLng(37.4718104, 127.0509002),
new kakao.maps.LatLng(37.4700597, 127.0486692),
new kakao.maps.LatLng(37.4693652, 127.0510504),
new kakao.maps.LatLng(37.4675849, 127.0509517),
new kakao.maps.LatLng(37.4688702, 127.0553919),
new kakao.maps.LatLng(37.469237, 127.059066),
new kakao.maps.LatLng(37.4692945, 127.0650747),
new kakao.maps.LatLng(37.4709576, 127.0685473),
new kakao.maps.LatLng(37.4709943, 127.0704221),
new kakao.maps.LatLng(37.4748544, 127.0779631),
new kakao.maps.LatLng(37.4757966, 127.0844785),
new kakao.maps.LatLng(37.4729288, 127.0841728),
new kakao.maps.LatLng(37.4713002, 127.0850167),
new kakao.maps.LatLng(37.4698449, 127.0875642),
new kakao.maps.LatLng(37.4684889, 127.0881284),
new kakao.maps.LatLng(37.4671484, 127.0904301),
new kakao.maps.LatLng(37.4649182, 127.0920416),
new kakao.maps.LatLng(37.4622744, 127.0920966),
new kakao.maps.LatLng(37.4612481, 127.0933434),
new kakao.maps.LatLng(37.460993, 127.0956975),
new kakao.maps.LatLng(37.458464, 127.0949315),
new kakao.maps.LatLng(37.4564649, 127.0952452),
new kakao.maps.LatLng(37.456285, 127.0990383),
new kakao.maps.LatLng(37.4585341, 127.101167),
new kakao.maps.LatLng(37.4600566, 127.1039435),
new kakao.maps.LatLng(37.4621594, 127.1043465),
new kakao.maps.LatLng(37.4624345, 127.1064566),
new kakao.maps.LatLng(37.4616446, 127.1118201),
new kakao.maps.LatLng(37.4598893, 127.1134332),
new kakao.maps.LatLng(37.458634, 127.116896),
new kakao.maps.LatLng(37.4622006, 127.1174754),
new kakao.maps.LatLng(37.464372, 127.12144),
new kakao.maps.LatLng(37.4665205, 127.1242057)
];

var gangnamPolygonE = new kakao.maps.Polygon({
    path: gangnamPolygonEPath,
    fillColor: '#7D160F',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 송파구 다각형 생성(22수준)
var songpaPolygonEPath = [
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5414079, 127.1082818),
new kakao.maps.LatLng(37.5270069, 127.090161),
new kakao.maps.LatLng(37.524759, 127.0856328),
new kakao.maps.LatLng(37.5229485, 127.0799746),
new kakao.maps.LatLng(37.522514, 127.0769544),
new kakao.maps.LatLng(37.523872, 127.0686631),
new kakao.maps.LatLng(37.5268818, 127.0607945),
new kakao.maps.LatLng(37.5283299, 127.0562249),
new kakao.maps.LatLng(37.5250565, 127.0654321),
new kakao.maps.LatLng(37.5245822, 127.0674791),
new kakao.maps.LatLng(37.5208765, 127.0675889),
new kakao.maps.LatLng(37.5027396, 127.0698181),
new kakao.maps.LatLng(37.5020674, 127.0769871),
new kakao.maps.LatLng(37.499673, 127.0841541),
new kakao.maps.LatLng(37.4966827, 127.0947945),
new kakao.maps.LatLng(37.4927054, 127.1035119),
new kakao.maps.LatLng(37.4902947, 127.1070066),
new kakao.maps.LatLng(37.4817224, 127.1129675),
new kakao.maps.LatLng(37.4665205, 127.1242057),
new kakao.maps.LatLng(37.4684191, 127.1270342),
new kakao.maps.LatLng(37.4677511, 127.1301405),
new kakao.maps.LatLng(37.4683941, 127.1327994),
new kakao.maps.LatLng(37.4697986, 127.1319826),
new kakao.maps.LatLng(37.4715382, 127.1328449),
new kakao.maps.LatLng(37.4746269, 127.1328558),
new kakao.maps.LatLng(37.4742406, 127.1354681),
new kakao.maps.LatLng(37.4739308, 127.1435264),
new kakao.maps.LatLng(37.4773315, 127.1443703),
new kakao.maps.LatLng(37.4772222, 127.1471451),
new kakao.maps.LatLng(37.4815898, 127.1474588),
new kakao.maps.LatLng(37.4840436, 127.1486828),
new kakao.maps.LatLng(37.4862358, 127.1521778),
new kakao.maps.LatLng(37.489672, 127.1585233),
new kakao.maps.LatLng(37.492048, 127.1584792),
new kakao.maps.LatLng(37.4943902, 127.1600312),
new kakao.maps.LatLng(37.4968237, 127.1597796),
new kakao.maps.LatLng(37.4995369, 127.1613552),
new kakao.maps.LatLng(37.5031794, 127.1577291),
new kakao.maps.LatLng(37.5018946, 127.1565548),
new kakao.maps.LatLng(37.5029854, 127.1521336),
new kakao.maps.LatLng(37.5046783, 127.1502631),
new kakao.maps.LatLng(37.5032338, 127.1477163),
new kakao.maps.LatLng(37.5054583, 127.1411493),
new kakao.maps.LatLng(37.5067087, 127.1415163),
new kakao.maps.LatLng(37.5085171, 127.139952),
new kakao.maps.LatLng(37.5123608, 127.1413929),
new kakao.maps.LatLng(37.5126573, 127.1435398),
new kakao.maps.LatLng(37.5156419, 127.1421313),
new kakao.maps.LatLng(37.5155915, 127.1446078),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var songpaPolygonE = new kakao.maps.Polygon({
    path: songpaPolygonEPath,
    fillColor: '#D20D14',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

// 강동구 다각형 생성(22수준)
var gangdongPolygonEPath =[
new kakao.maps.LatLng(37.516886, 127.1450901),
new kakao.maps.LatLng(37.5196245, 127.1447856),
new kakao.maps.LatLng(37.5219397, 127.1457414),
new kakao.maps.LatLng(37.5221448, 127.1478181),
new kakao.maps.LatLng(37.5263728, 127.1504017),
new kakao.maps.LatLng(37.5285295, 127.1526867),
new kakao.maps.LatLng(37.5319199, 127.1539334),
new kakao.maps.LatLng(37.533683, 127.1536063),
new kakao.maps.LatLng(37.5392702, 127.1576512),
new kakao.maps.LatLng(37.5411651, 127.1598933),
new kakao.maps.LatLng(37.5449999, 127.1631595),
new kakao.maps.LatLng(37.5442561, 127.1666417),
new kakao.maps.LatLng(37.5455346, 127.1721068),
new kakao.maps.LatLng(37.5452104, 127.1757181),
new kakao.maps.LatLng(37.5466816, 127.1793088),
new kakao.maps.LatLng(37.5463443, 127.1828251),
new kakao.maps.LatLng(37.5518204, 127.1829114),
new kakao.maps.LatLng(37.5528619, 127.1813807),
new kakao.maps.LatLng(37.5609928, 127.1819994),
new kakao.maps.LatLng(37.5654958, 127.179585),
new kakao.maps.LatLng(37.5689182, 127.1792158),
new kakao.maps.LatLng(37.5722139, 127.1777375),
new kakao.maps.LatLng(37.5740993, 127.17614),
new kakao.maps.LatLng(37.5783633, 127.1754421),
new kakao.maps.LatLng(37.5792655, 127.1768832),
new kakao.maps.LatLng(37.5812008, 127.1771547),
new kakao.maps.LatLng(37.5797349, 127.1738711),
new kakao.maps.LatLng(37.5786946, 127.1671595),
new kakao.maps.LatLng(37.5764649, 127.1629721),
new kakao.maps.LatLng(37.5704037, 127.1536011),
new kakao.maps.LatLng(37.5681865, 127.1493618),
new kakao.maps.LatLng(37.5682007, 127.138063),
new kakao.maps.LatLng(37.567884, 127.135692),
new kakao.maps.LatLng(37.565944, 127.1290179),
new kakao.maps.LatLng(37.5633331, 127.1234369),
new kakao.maps.LatLng(37.5592439, 127.1176932),
new kakao.maps.LatLng(37.5568724, 127.1153231),
new kakao.maps.LatLng(37.5543662, 127.1143095),
new kakao.maps.LatLng(37.5504987, 127.1115571),
new kakao.maps.LatLng(37.5469267, 127.1114708),
new kakao.maps.LatLng(37.5431669, 127.1092397),
new kakao.maps.LatLng(37.5429792, 127.1130478),
new kakao.maps.LatLng(37.5410718, 127.1188769),
new kakao.maps.LatLng(37.5386463, 127.1234424),
new kakao.maps.LatLng(37.5296629, 127.1201352),
new kakao.maps.LatLng(37.5279602, 127.1190926),
new kakao.maps.LatLng(37.517039, 127.1438278),
new kakao.maps.LatLng(37.516886, 127.1450901)
];

var gangdongPolygonE = new kakao.maps.Polygon({
    path: gangdongPolygonEPath,
    fillColor: '#E85239',
    fillOpacity: 0.5,
    strokeWeight: 2,
    strokeColor: '#FFFFFF',
    strokeOpacity: 0.9,
    strokeStyle: 'solid'
});

        // Toggle buttons for each polygon
        var isPolygonAVisible = false;
        document.getElementById('togglePolygonA').addEventListener('click', function () {
            if (isPolygonAVisible) {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                yongsanPolygonA.setMap(null); // 용산구 다각형 제거
                dongdaemunPolygonA.setMap(null); // 동대문구 다각형 제거
                seodaemunPolygonA.setMap(null); // 성동구 다각형 제거
                seungdongPolygonA.setMap(null); // 서대문구 다각형 제거
                jongnoPolygonA.setMap(null); // 종로구 다각형 제거
                jungPolygonA.setMap(null); // 중구 다각형 제거
                gwangjinPolygonA.setMap(null); // 광진구 다각형 제거
                jungnangPolygonA.setMap(null); // 중랑구 다각형 제거
                seongbukPolygonA.setMap(null); // 성북구 다각형 제거
                gangbukPolygonA.setMap(null); // 강북구 다각형 제거
                dobongPolygonA.setMap(null); // 도봉구 다각형 제거
                nowonPolygonA.setMap(null); // 노원구 다각형 제거
                eunpyeongPolygonA.setMap(null); // 은평구 다각형 제거
                mapoPolygonA.setMap(null); // 마포구 다각형 제거
                yangcheonPolygonA.setMap(null); // 양천구 다각형 제거
                gangseoPolygonA.setMap(null); // 강서구 다각형 제거
                guroPolygonA.setMap(null); // 구로구 다각형 제거
                geumcheonPolygonA.setMap(null); // 금천구 다각형 제거
                yeongdeungpoPolygonA.setMap(null); // 영등포구 다각형 제거
                dongjakPolygonA.setMap(null); // 동작구 다각형 제거
                gwanakPolygonA.setMap(null); // 관악구 다각형 제거
                seochoPolygonA.setMap(null); // 서초구 다각형 제거
                gangnamPolygonA.setMap(null); // 강남구 다각형 제거
                songpaPolygonA.setMap(null); // 송파구 다각형 제거
                gangdongPolygonA.setMap(null); // 강동구 다각형 제거
            } else {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'block'; // Show bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                yongsanPolygonA.setMap(map); // 용산구 다각형 추가
                dongdaemunPolygonA.setMap(map); // 동대문구 다각형 추가
                seodaemunPolygonA.setMap(map); // 성동구 다각형 추가
                seungdongPolygonA.setMap(map); // 서대문구 다각형 추가
                jongnoPolygonA.setMap(map); // 종로구 다각형 추가
                jungPolygonA.setMap(map); // 중구 다각형 추가
                gwangjinPolygonA.setMap(map); // 광진구 다각형 추가
                jungnangPolygonA.setMap(map); // 중랑구 다각형 추가
                seongbukPolygonA.setMap(map); // 성북구 다각형 추가
                gangbukPolygonA.setMap(map); // 강북구 다각형 추가
                dobongPolygonA.setMap(map); // 도봉구 다각형 추가
                nowonPolygonA.setMap(map); // 노원구 다각형 추가
                eunpyeongPolygonA.setMap(map); // 은평구 다각형 추가
                mapoPolygonA.setMap(map); // 마포구 다각형 추가
                yangcheonPolygonA.setMap(map); // 양천구 다각형 추가
                gangseoPolygonA.setMap(map); // 강서구 다각형 추가
                guroPolygonA.setMap(map); // 구로구 다각형 추가
                geumcheonPolygonA.setMap(map); // 금천구 다각형 추가
                yeongdeungpoPolygonA.setMap(map); // 영등포구 다각형 추가
                dongjakPolygonA.setMap(map); // 동작구 다각형 추가
                gwanakPolygonA.setMap(map); // 관악구 다각형 추가
                seochoPolygonA.setMap(map); // 서초구 다각형 추가
                gangnamPolygonA.setMap(map); // 강남구 다각형 추가
                songpaPolygonA.setMap(map); // 송파구 다각형 추가
                gangdongPolygonA.setMap(map); // 강동구 다각형 추가
            }
            isPolygonAVisible = !isPolygonAVisible;
        });

        var isPolygonBVisible = false;
        document.getElementById('togglePolygonB').addEventListener('click', function () {
            if (isPolygonBVisible) {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                yongsanPolygonB.setMap(null); // 용산구 다각형 제거
                dongdaemunPolygonB.setMap(null); // 동대문구 다각형 제거
                seodaemunPolygonB.setMap(null); // 서대문구 다각형 제거
                seungdongPolygonB.setMap(null); // 성동구 다각형 제거
                jongnoPolygonB.setMap(null); // 종로구 다각형 제거
                jungPolygonB.setMap(null); // 중구 다각형 제거
                gwangjinPolygonB.setMap(null); // 광진구 다각형 제거
                jungnangPolygonB.setMap(null); // 중랑구 다각형 제거
                seongbukPolygonB.setMap(null); // 성북구 다각형 제거
                gangbukPolygonB.setMap(null); // 강북구 다각형 제거
                dobongPolygonB.setMap(null); // 도봉구 다각형 제거
                nowonPolygonB.setMap(null); // 노원구 다각형 제거
                eunpyeongPolygonB.setMap(null); // 은평구 다각형 제거
                mapoPolygonB.setMap(null); // 마포구 다각형 제거
                yangcheonPolygonB.setMap(null); // 양천구 다각형 제거
                gangseoPolygonB.setMap(null); // 강서구 다각형 제거
                guroPolygonB.setMap(null); // 구로구 다각형 제거
                geumcheonPolygonB.setMap(null); // 금천구 다각형 제거
                yeongdeungpoPolygonB.setMap(null); // 영등포구 다각형 제거
                dongjakPolygonB.setMap(null); // 동작구 다각형 제거
                gwanakPolygonB.setMap(null); // 관악구 다각형 제거
                seochoPolygonB.setMap(null); // 서초구 다각형 제거
                gangnamPolygonB.setMap(null); // 강남구 다각형 제거
                songpaPolygonB.setMap(null); // 송파구 다각형 제거
                gangdongPolygonB.setMap(null); // 강동구 다각형 제거

            } else {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'block'; // Hide bar b
                yongsanPolygonB.setMap(map); // 용산구 다각형 추가
                dongdaemunPolygonB.setMap(map); // 동대문구 다각형 추가
                seodaemunPolygonB.setMap(map); // 서대문구 다각형 추가
                seungdongPolygonB.setMap(map); // 성동구 다각형 추가
                jongnoPolygonB.setMap(map); // 종로구 다각형 추가
                jungPolygonB.setMap(map); // 중구 다각형 추가
                gwangjinPolygonB.setMap(map); // 광진구 다각형 추가
                jungnangPolygonB.setMap(map); // 중랑구 다각형 추가
                seongbukPolygonB.setMap(map); // 성북구 다각형 추가
                gangbukPolygonB.setMap(map); // 강북구 다각형 추가
                dobongPolygonB.setMap(map); // 도봉구 다각형 추가
                nowonPolygonB.setMap(map); // 노원구 다각형 추가
                eunpyeongPolygonB.setMap(map); // 은평구 다각형 추가
                mapoPolygonB.setMap(map); // 마포구 다각형 추가
                yangcheonPolygonB.setMap(map); // 양천구 다각형 추가
                gangseoPolygonB.setMap(map); // 강서구 다각형 추가
                guroPolygonB.setMap(map); // 구로구 다각형 추가
                geumcheonPolygonB.setMap(map); // 금천구 다각형 추가
                yeongdeungpoPolygonB.setMap(map); // 영등포구 다각형 추가
                dongjakPolygonB.setMap(map); // 동작구 다각형 추가
                gwanakPolygonB.setMap(map); // 관악구 다각형 추가
                seochoPolygonB.setMap(map); // 서초구 다각형 추가
                gangnamPolygonB.setMap(map); // 강남구 다각형 추가
                songpaPolygonB.setMap(map); // 송파구 다각형 추가
                gangdongPolygonB.setMap(map); // 강동구 다각형 추가
            }
            isPolygonBVisible = !isPolygonBVisible;
        });

        var isPolygonCVisible = false;
        document.getElementById('togglePolygonC').addEventListener('click', function () {
            if (isPolygonCVisible) {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                yongsanPolygonC.setMap(null); // 용산구 다각형 제거
                dongdaemunPolygonC.setMap(null); // 동대문구 다각형 제거
                seodaemunPolygonC.setMap(null); // 서대문구 다각형 제거
                seungdongPolygonC.setMap(null); // 성동구 다각형 제거
                jongnoPolygonC.setMap(null); // 종로구 다각형 제거
                jungPolygonC.setMap(null); // 중구 다각형 제거
                gwangjinPolygonC.setMap(null); // 광진구 다각형 제거
                jungnangPolygonC.setMap(null); // 중랑구 다각형 제거
                seongbukPolygonC.setMap(null); // 성북구 다각형 제거
                gangbukPolygonC.setMap(null); // 강북구 다각형 제거
                dobongPolygonC.setMap(null); // 도봉구 다각형 제거
                nowonPolygonC.setMap(null); // 노원구 다각형 제거
                eunpyeongPolygonC.setMap(null); // 은평구 다각형 제거
                mapoPolygonC.setMap(null); // 마포구 다각형 제거
                yangcheonPolygonC.setMap(null); // 양천구 다각형 제거
                gangseoPolygonC.setMap(null); // 강서구 다각형 제거
                guroPolygonC.setMap(null); // 구로구 다각형 제거
                geumcheonPolygonC.setMap(null); // 금천구 다각형 제거
                yeongdeungpoPolygonC.setMap(null); // 영등포구 다각형 제거
                dongjakPolygonC.setMap(null); // 동작구 다각형 제거
                gwanakPolygonC.setMap(null); // 관악구 다각형 제거
                seochoPolygonC.setMap(null); // 서초구 다각형 제거
                gangnamPolygonC.setMap(null); // 강남구 다각형 제거
                songpaPolygonC.setMap(null); // 송파구 다각형 제거
                gangdongPolygonC.setMap(null); // 강동구 다각형 제거
            } else {
                document.getElementById('legend').style.display = 'block'; // Show legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                yongsanPolygonC.setMap(map); // 용산구 다각형 추가
                dongdaemunPolygonC.setMap(map); // 동대문구 다각형 추가
                seodaemunPolygonC.setMap(map); // 서대문구 다각형 추가
                seungdongPolygonC.setMap(map); // 성동구 다각형 추가
                jongnoPolygonC.setMap(map); // 종로구 다각형 추가
                jungPolygonC.setMap(map); // 중구 다각형 추가
                gwangjinPolygonC.setMap(map); // 광진구 다각형 추가
                jungnangPolygonC.setMap(map); // 중랑구 다각형 추가
                seongbukPolygonC.setMap(map); // 성북구 다각형 추가
                gangbukPolygonC.setMap(map); // 강북구 다각형 추가
                dobongPolygonC.setMap(map); // 도봉구 다각형 추가
                nowonPolygonC.setMap(map); // 노원구 다각형 추가
                eunpyeongPolygonC.setMap(map); // 은평구 다각형 추가
                mapoPolygonC.setMap(map); // 마포구 다각형 추가
                yangcheonPolygonC.setMap(map); // 양천구 다각형 추가
                gangseoPolygonC.setMap(map); // 강서구 다각형 추가
                guroPolygonC.setMap(map); // 구로구 다각형 추가
                geumcheonPolygonC.setMap(map); // 금천구 다각형 추가
                yeongdeungpoPolygonC.setMap(map); // 영등포구 다각형 추가
                dongjakPolygonC.setMap(map); // 동작구 다각형 추가
                gwanakPolygonC.setMap(map); // 관악구 다각형 추가
                seochoPolygonC.setMap(map); // 서초구 다각형 추가
                gangnamPolygonC.setMap(map); // 강남구 다각형 추가
                songpaPolygonC.setMap(map); // 송파구 다각형 추가
                gangdongPolygonC.setMap(map); // 강동구 다각형 추가
            }
            isPolygonCVisible = !isPolygonCVisible;
        });

        var isPolygonDVisible = false;
        document.getElementById('togglePolygonD').addEventListener('click', function () {
            if (isPolygonDVisible) {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                document.getElementById('demographic-legend').style.display = 'none';
                markers.forEach(function(marker) {
                    marker.setMap(null);
                });
                yongsanPolygonD.setMap(null); // 용산구 다각형 제거
                dongdaemunPolygonD.setMap(null); // 동대문구 다각형 제거
                seodaemunPolygonD.setMap(null); // 서대문구 다각형 제거
                seungdongPolygonD.setMap(null); // 성동구 다각형 제거
                jongnoPolygonD.setMap(null); // 종로구 다각형 제거
                jungPolygonD.setMap(null); // 중구 다각형 제거
                gwangjinPolygonD.setMap(null); // 광진구 다각형 제거
                jungnangPolygonD.setMap(null); // 중랑구 다각형 제거
                seongbukPolygonD.setMap(null); // 성북구 다각형 제거
                gangbukPolygonD.setMap(null); // 강북구 다각형 제거
                dobongPolygonD.setMap(null); // 도봉구 다각형 제거
                nowonPolygonD.setMap(null); // 노원구 다각형 제거
                eunpyeongPolygonD.setMap(null); // 은평구 다각형 제거
                mapoPolygonD.setMap(null); // 마포구 다각형 제거
                yangcheonPolygonD.setMap(null); // 양천구 다각형 제거
                gangseoPolygonD.setMap(null); // 강서구 다각형 제거
                guroPolygonD.setMap(null); // 구로구 다각형 제거
                geumcheonPolygonD.setMap(null); // 금천구 다각형 제거
                yeongdeungpoPolygonD.setMap(null); // 영등포구 다각형 제거
                dongjakPolygonD.setMap(null); // 동작구 다각형 제거
                gwanakPolygonD.setMap(null); // 관악구 다각형 제거
                seochoPolygonD.setMap(null); // 서초구 다각형 제거
                gangnamPolygonD.setMap(null); // 강남구 다각형 제거
                songpaPolygonD.setMap(null); // 송파구 다각형 제거
                gangdongPolygonD.setMap(null); // 강동구 다각형 제거
            } else {
                document.getElementById('legend').style.display = 'none'; // Show legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                document.getElementById('demographic-legend').style.display = 'block';
                markers.forEach(function(marker) {
                    marker.setMap(map);
                });
                yongsanPolygonD.setMap(map); // 용산구 다각형 추가
                dongdaemunPolygonD.setMap(map); // 동대문구 다각형 추가
                seodaemunPolygonD.setMap(map); // 서대문구 다각형 추가
                seungdongPolygonD.setMap(map); // 성동구 다각형 추가
                jongnoPolygonD.setMap(map); // 종로구 다각형 추가
                jungPolygonD.setMap(map); // 중구 다각형 추가
                gwangjinPolygonD.setMap(map); // 광진구 다각형 추가
                jungnangPolygonD.setMap(map); // 중랑구 다각형 추가
                seongbukPolygonD.setMap(map); // 성북구 다각형 추가
                gangbukPolygonD.setMap(map); // 강북구 다각형 추가
                dobongPolygonD.setMap(map); // 도봉구 다각형 추가
                nowonPolygonD.setMap(map); // 노원구 다각형 추가
                eunpyeongPolygonD.setMap(map); // 은평구 다각형 추가
                mapoPolygonD.setMap(map); // 마포구 다각형 추가
                yangcheonPolygonD.setMap(map); // 양천구 다각형 추가
                gangseoPolygonD.setMap(map); // 강서구 다각형 추가
                guroPolygonD.setMap(map); // 구로구 다각형 추가
                geumcheonPolygonD.setMap(map); // 금천구 다각형 추가
                yeongdeungpoPolygonD.setMap(map); // 영등포구 다각형 추가
                dongjakPolygonD.setMap(map); // 동작구 다각형 추가
                gwanakPolygonD.setMap(map); // 관악구 다각형 추가
                seochoPolygonD.setMap(map); // 서초구 다각형 추가
                gangnamPolygonD.setMap(map); // 강남구 다각형 추가
                songpaPolygonD.setMap(map); // 송파구 다각형 추가
                gangdongPolygonD.setMap(map); // 강동구 다각형 추가
            }
            isPolygonDVisible = !isPolygonDVisible;
        });

        var isPolygonEVisible = false;
        document.getElementById('togglePolygonE').addEventListener('click', function () {
            if (isPolygonEVisible) {
                document.getElementById('legend').style.display = 'none'; // Hide legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                document.getElementById('demographic-legend').style.display = 'none';
                document.getElementById('barlegend').style.display = 'none'; // Hide legend
                mapContainer.querySelectorAll('.bar-chart').forEach(function (element) {
                    element.parentNode.removeChild(element);
                });

                yongsanPolygonE.setMap(null); // 용산구 다각형 제거
                dongdaemunPolygonE.setMap(null); // 동대문구 다각형 제거
                seodaemunPolygonE.setMap(null); // 서대문구 다각형 제거
                seungdongPolygonE.setMap(null); // 성동구 다각형 제거
                jongnoPolygonE.setMap(null); // 종로구 다각형 제거
                jungPolygonE.setMap(null); // 중구 다각형 제거
                gwangjinPolygonE.setMap(null); // 광진구 다각형 제거
                jungnangPolygonE.setMap(null); // 중랑구 다각형 제거
                seongbukPolygonE.setMap(null); // 성북구 다각형 제거
                gangbukPolygonE.setMap(null); // 강북구 다각형 제거
                dobongPolygonE.setMap(null); // 도봉구 다각형 제거
                nowonPolygonE.setMap(null); // 노원구 다각형 제거
                eunpyeongPolygonE.setMap(null); // 은평구 다각형 제거
                mapoPolygonE.setMap(null); // 마포구 다각형 제거
                yangcheonPolygonE.setMap(null); // 양천구 다각형 제거
                gangseoPolygonE.setMap(null); // 강서구 다각형 제거
                guroPolygonE.setMap(null); // 구로구 다각형 제거
                geumcheonPolygonE.setMap(null); // 금천구 다각형 제거
                yeongdeungpoPolygonE.setMap(null); // 영등포구 다각형 제거
                dongjakPolygonE.setMap(null); // 동작구 다각형 제거
                gwanakPolygonE.setMap(null); // 관악구 다각형 제거
                seochoPolygonE.setMap(null); // 서초구 다각형 제거
                gangnamPolygonE.setMap(null); // 강남구 다각형 제거
                songpaPolygonE.setMap(null); // 송파구 다각형 제거
                gangdongPolygonE.setMap(null); // 강동구 다각형 제거
            } else {
                document.getElementById('legend').style.display = 'none'; // Show legend
                document.getElementById('single-bar-container').style.display = 'none'; // Hide bar
                document.getElementById('single-bar-container-b').style.display = 'none'; // Hide bar b
                document.getElementById('demographic-legend').style.display = 'none';
                document.getElementById('barlegend').style.display = 'block'; // Show legend
                document.getElementById('barlegend').style.display = 'block'; // Show legend
                addBarCharts(map);
                yongsanPolygonE.setMap(map); // 용산구 다각형 추가
                dongdaemunPolygonE.setMap(map); // 동대문구 다각형 추가
                seodaemunPolygonE.setMap(map); // 서대문구 다각형 추가
                seungdongPolygonE.setMap(map); // 성동구 다각형 추가
                jongnoPolygonE.setMap(map); // 종로구 다각형 추가
                jungPolygonE.setMap(map); // 중구 다각형 추가
                gwangjinPolygonE.setMap(map); // 광진구 다각형 추가
                jungnangPolygonE.setMap(map); // 중랑구 다각형 추가
                seongbukPolygonE.setMap(map); // 성북구 다각형 추가
                gangbukPolygonE.setMap(map); // 강북구 다각형 추가
                dobongPolygonE.setMap(map); // 도봉구 다각형 추가
                nowonPolygonE.setMap(map); // 노원구 다각형 추가
                eunpyeongPolygonE.setMap(map); // 은평구 다각형 추가
                mapoPolygonE.setMap(map); // 마포구 다각형 추가
                yangcheonPolygonE.setMap(map); // 양천구 다각형 추가
                gangseoPolygonE.setMap(map); // 강서구 다각형 추가
                guroPolygonE.setMap(map); // 구로구 다각형 추가
                geumcheonPolygonE.setMap(map); // 금천구 다각형 추가
                yeongdeungpoPolygonE.setMap(map); // 영등포구 다각형 추가
                dongjakPolygonE.setMap(map); // 동작구 다각형 추가
                gwanakPolygonE.setMap(map); // 관악구 다각형 추가
                seochoPolygonE.setMap(map); // 서초구 다각형 추가
                gangnamPolygonE.setMap(map); // 강남구 다각형 추가
                songpaPolygonE.setMap(map); // 송파구 다각형 추가
                gangdongPolygonE.setMap(map); // 강동구 다각형 추가

            }
            isPolygonEVisible = !isPolygonEVisible;
        });

        // Zoom in and zoom out button handlers
        document.getElementById('zoomIn').addEventListener('click', function () {
            var level = map.getLevel() - 1;
            map.setLevel(level, { animate: true });
        });

        document.getElementById('zoomOut').addEventListener('click', function () {
            var level = map.getLevel() + 1;
            map.setLevel(level, { animate: true });
        });

        // 용산구 인포윈도우
var contentA = '<div style="padding:5px;">용산구 득표율 56.4%</div>';
var infowindowA = new kakao.maps.InfoWindow({
    content: contentA, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(yongsanPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowA.setPosition(mouseEvent.latLng); 
    infowindowA.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(yongsanPolygonC, 'mouseout', function() { 
    infowindowA.close(); 
}); 

// 동대문구 인포윈도우 B
var contentB = '<div style="padding:5px;">동대문구 득표율 49.2%</div>';
var infowindowB = new kakao.maps.InfoWindow({
    content: contentB, 
    removable: false 
});

// 다각형 B에 마우스오버 이벤트 등록
kakao.maps.event.addListener(dongdaemunPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowB.setPosition(mouseEvent.latLng); 
    infowindowB.open(map); 
});   

// 다각형 B에 마우스아웃 이벤트 등록
kakao.maps.event.addListener(dongdaemunPolygonC, 'mouseout', function() { 
    infowindowB.close(); 
});

//  성동구 인포윈도우 C
var contentC = '<div style="padding:5px;">성동구 득표율 53.2%</div>';
var infowindowC = new kakao.maps.InfoWindow({
    content: contentC, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(seungdongPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowC.setPosition(mouseEvent.latLng); 
    infowindowC.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(seungdongPolygonC, 'mouseout', function() { 
    infowindowC.close(); 
});

    // 종로구 인포윈도우 D
var contentD = '<div style="padding:5px;">종로구 득표율 49.5%</div>';
var infowindowD = new kakao.maps.InfoWindow({
    content: contentD, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(jongnoPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowD.setPosition(mouseEvent.latLng); 
    infowindowD.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(jongnoPolygonC, 'mouseout', function() { 
    infowindowD.close(); 
});

// 중구 인포윈도우 F
var contentF = '<div style="padding:5px;">중구 득표율 51.0%</div>';
var infowindowF = new kakao.maps.InfoWindow({
    content: contentF, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(jungPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowF.setPosition(mouseEvent.latLng); 
    infowindowF.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(jungPolygonC, 'mouseout', function() { 
    infowindowF.close(); 
});

// 광진구 인포윈도우 E
var contentE = '<div style="padding:5px;">광진구 득표율 48.8%</div>';
var infowindowE = new kakao.maps.InfoWindow({
    content: contentE, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(gwangjinPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowE.setPosition(mouseEvent.latLng); 
    infowindowE.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(gwangjinPolygonC, 'mouseout', function() { 
    infowindowE.close(); 
});
// 중랑구 인포윈도우 F
var contentF = '<div style="padding:5px;">중랑구 득표율 50.5%</div>';
var infowindowF = new kakao.maps.InfoWindow({
    content: contentF, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(jungnangPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowF.setPosition(mouseEvent.latLng); 
    infowindowF.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(jungnangPolygonC, 'mouseout', function() { 
    infowindowF.close(); 
});

// 성북구 인포윈도우 G
var contentG = '<div style="padding:5px;">성북구 득표율 49.3%</div>';
var infowindowG = new kakao.maps.InfoWindow({
    content: contentG, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(seongbukPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowG.setPosition(mouseEvent.latLng); 
    infowindowG.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(seongbukPolygonC, 'mouseout', function() { 
    infowindowG.close(); 
});

// 강북구 인포윈도우 H
var contentH = '<div style="padding:5px;">강북구 득표율 52.3%</div>';
var infowindowH = new kakao.maps.InfoWindow({
    content: contentH, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(gangbukPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowH.setPosition(mouseEvent.latLng); 
    infowindowH.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(gangbukPolygonC, 'mouseout', function() { 
    infowindowH.close(); 
});

// 도봉구 인포윈도우 I
var contentI = '<div style="padding:5px;">도봉구 득표율 49.8%</div>';
var infowindowI = new kakao.maps.InfoWindow({
    content: contentI, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(dobongPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowI.setPosition(mouseEvent.latLng); 
    infowindowI.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(dobongPolygonC, 'mouseout', function() { 
    infowindowI.close(); 
});
// 노원구 인포윈도우 J
var contentJ = '<div style="padding:5px;">노원구 득표율 48.9%</div>';
var infowindowJ = new kakao.maps.InfoWindow({
    content: contentJ, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(nowonPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowJ.setPosition(mouseEvent.latLng); 
    infowindowJ.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(nowonPolygonC, 'mouseout', function() { 
    infowindowJ.close(); 
});
// 은평구 인포윈도우 K
var contentK = '<div style="padding:5px;">은평구 득표율 51.3%</div>';
var infowindowK = new kakao.maps.InfoWindow({
    content: contentK, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(eunpyeongPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowK.setPosition(mouseEvent.latLng); 
    infowindowK.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(eunpyeongPolygonC, 'mouseout', function() { 
    infowindowK.close(); 
});
// 서대문구 인포윈도우 L
var contentL = '<div style="padding:5px;">서대문구 득표율 48.3%</div>';
var infowindowL = new kakao.maps.InfoWindow({
    content: contentL, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(seodaemunPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowL.setPosition(mouseEvent.latLng); 
    infowindowL.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(seodaemunPolygonC, 'mouseout', function() { 
    infowindowL.close(); 
});
// 마포구 인포윈도우 M
var contentM = '<div style="padding:5px;">마포구 득표율 49.0%</div>';
var infowindowM = new kakao.maps.InfoWindow({
    content: contentM, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(mapoPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowM.setPosition(mouseEvent.latLng); 
    infowindowM.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(mapoPolygonC, 'mouseout', function() { 
    infowindowM.close(); 
});
// 양천구 인포윈도우 N
var contentN = '<div style="padding:5px;">양천구 득표율 50.1%</div>';
var infowindowN = new kakao.maps.InfoWindow({
    content: contentN, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(yangcheonPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowN.setPosition(mouseEvent.latLng); 
    infowindowN.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(yangcheonPolygonC, 'mouseout', function() { 
    infowindowN.close(); 
});
// 강서구 인포윈도우 O
var contentO = '<div style="padding:5px;">강서구 득표율 49.2%</div>';
var infowindowO = new kakao.maps.InfoWindow({
    content: contentO, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(gangseoPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowO.setPosition(mouseEvent.latLng); 
    infowindowO.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(gangseoPolygonC, 'mouseout', function() { 
    infowindowO.close(); 
});
// 구로구 인포윈도우 P
var contentP = '<div style="padding:5px;">구로구 득표율 49.2%</div>';
var infowindowP = new kakao.maps.InfoWindow({
    content: contentP, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(guroPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowP.setPosition(mouseEvent.latLng); 
    infowindowP.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(guroPolygonC, 'mouseout', function() { 
    infowindowP.close(); 
});

// 금천구 인포윈도우 Q
var contentQ = '<div style="padding:5px;">금천구 득표율 51.6%</div>';
var infowindowQ = new kakao.maps.InfoWindow({
    content: contentQ, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(geumcheonPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowQ.setPosition(mouseEvent.latLng); 
    infowindowQ.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(geumcheonPolygonC, 'mouseout', function() { 
    infowindowQ.close(); 
});
// 영등포구 인포윈도우 R
var contentR = '<div style="padding:5px;">영등포구 득표율 51.6%</div>';
var infowindowR = new kakao.maps.InfoWindow({
    content: contentR, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(yeongdeungpoPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowR.setPosition(mouseEvent.latLng); 
    infowindowR.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(yeongdeungpoPolygonC, 'mouseout', function() { 
    infowindowR.close(); 
});
// 동작구 인포윈도우 S
var contentS = '<div style="padding:5px;">동작구 득표율 50.5%</div>';
var infowindowS = new kakao.maps.InfoWindow({
    content: contentS, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(dongjakPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowS.setPosition(mouseEvent.latLng); 
    infowindowS.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(dongjakPolygonC, 'mouseout', function() { 
    infowindowS.close(); 
});
// 관악구 인포윈도우 T
var contentT = '<div style="padding:5px;">관악구 득표율 50.3%</div>';
var infowindowT = new kakao.maps.InfoWindow({
    content: contentT, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(gwanakPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowT.setPosition(mouseEvent.latLng); 
    infowindowT.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(gwanakPolygonC, 'mouseout', function() { 
    infowindowT.close(); 
});
// 서초구 인포윈도우 U
var contentU = '<div style="padding:5px;">서초구 득표율 66.4%</div>';
var infowindowU = new kakao.maps.InfoWindow({
    content: contentU, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(seochoPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowU.setPosition(mouseEvent.latLng); 
    infowindowU.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(seochoPolygonC, 'mouseout', function() { 
    infowindowU.close(); 
});

//  강남구 인포윈도우 V
var contentV = '<div style="padding:5px;">강남구 득표율 67.0%</div>';
var infowindowV = new kakao.maps.InfoWindow({
    content: contentV, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(gangnamPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowV.setPosition(mouseEvent.latLng); 
    infowindowV.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(gangnamPolygonC, 'mouseout', function() { 
    infowindowV.close(); 
});

// 송파구 인포윈도우 W
var contentW = '<div style="padding:5px;">송파구 득표율 56.8%</div>';
var infowindowW = new kakao.maps.InfoWindow({
    content: contentW, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(songpaPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowW.setPosition(mouseEvent.latLng); 
    infowindowW.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(songpaPolygonC, 'mouseout', function() { 
    infowindowW.close(); 
});

// 강동구 인포윈도우 X
var contentX = '<div style="padding:5px;">강동구 득표율 51.7%</div>';
var infowindowX = new kakao.maps.InfoWindow({
    content: contentX, 
    removable: false 
});

// 다각형 마우스오버 이벤트 등록
kakao.maps.event.addListener(gangdongPolygonC, 'mouseover', function(mouseEvent) { 
    infowindowX.setPosition(mouseEvent.latLng); 
    infowindowX.open(map); 
});   

// 다각형 마우스아웃 이벤트 등록
kakao.maps.event.addListener(gangdongPolygonC, 'mouseout', function() { 
    infowindowX.close(); 
});

    </script>
</body>
</html>
