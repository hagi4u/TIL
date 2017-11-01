# jQuery API 중 data, attr 차이

jQuery 에서 attr() method 로 지정 한 data-* 관련 속성은, 
data()메소드로 빼올 경우 캐싱처리되어 연동이 되지 않는다.

즉,
변수처럼 사용 할 경우에는

data('variable', value)로 지정 후, (이때는 해당되는 dom에 data-attr 이 추가되지 않음)
data('variable')로 값을 가져와야 정상적으로 된다.

attr('data-variable', value)로 하는 경우, (이때는 해당되는 dom에 data-variable 이 추가)
attr로 가져와야 하며 data() 메소드로 가져 올 경우 jQuery 내부적인 변수전환으로 인해 캐싱되는 것 처럼 보여 갱신이 되지 않는다.