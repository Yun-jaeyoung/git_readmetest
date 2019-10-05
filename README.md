# 온습도 기능 구성도 
![humtem](https://user-images.githubusercontent.com/54908993/66253759-e2ac2d00-e7a7-11e9-95ea-41a481a8f1f2.png)

# 음성출력 과정
- dht11과 esp8266이 연결돼있는 아두이노가 dht11의 실시간 집안 온,습도를 thingspeak로 보냄과 동시에 웹서버로도 보낸다.
- 실시간 온,습도가 온도30도 이상 습도 80% 이상이 되거나 온도 혹은 습도 둘중 하나만 높을시 서버로부터 데이터를 받아온다.
 ```
 if (esp8266.available()) { 
    if (esp8266.find("+IPD,")) {
      income_wifi = esp8266.readStringUntil('\r');
      wifi_temp = income_wifi.substring(income_wifi.indexOf("1:")+2, income_wifi.indexOf(""-1));
      Serial.println(wifi_temp);
   } 
  }
  ```
- dht11과 esp8266이 연결돼있는 아두이노가 mp3모듈이 연결돼있는 아두이노에 serial로 데이터값을 전송한다.
- 미리 저장돼있는 mp3파일을 mp3모듈을 통해 온,습도값에 따라서 음성을 출력한다.(온도가 높을때, 습도가 높을때, 온습도 둘 다 높을때)

# 기능
- 온도가 30°C 이상일 때, 온도를 조정해달라는 음성을 출력한다.
- 습도가 80% 이상일 때, 습도를 조정해달라는 음성을 출력한다.
- 온도가 30°C 이상, 습도가 80% 이상일 때 온도와 습도를 조정해달라는 음성 출력한다.
- thingspeak에 실시간 온습도 그래프 확인 가능하다.

# 개인공간 침해방지 기능 구성도
![privacyspace](https://user-images.githubusercontent.com/54908993/66254125-1473c280-e7ad-11e9-9360-add532a07c1b.png)

# 음성출력 과정
- 외부인이 사적인 공간에 접근시 pir센서가 이를 감지한다.
- esp8266이 연결된 아두이노가 thingspeak에 몇번 감지되었는지 전송한다. (1시간 간격으로 감지횟수는 0으로 초기화됨)
- 미리 저장돼있는 mp3파일을 mp3모듈을 통해 출력한다. (사적인 공간이니 집주인의 허락을 받아주세요.)

# 기능
- 사적인 공간에 외부인이 출입하였을시, 집주인의 허락을 받아달라는 음성을 출력한다.
- 1시간 간격으로 외부인이 몇번 출입하였는지 thingspeak를 통해 확인 가능하다.
