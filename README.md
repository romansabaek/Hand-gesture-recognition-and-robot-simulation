1. 소개 :본 프로젝트는 손가락이 가리키는 방향 및 손가락의 개수를 파악하여 gazebo 시뮬레이터 상의 로봇의 움직임을 제어하는 프로젝트 입니다.

2. 개발 환경 : 리눅스 ubuntu14.04 와 ROS 를 사용했으며 Qt creator를 이용해서 개발하였습니다. 

3. 소스구성 : main.cpp를 중심으로 dh_cam 이라는 라이브러리를 만들었고, dh_cam.h 라는 헤더파일을 따로 만들어 주었습니다. 또한 blobabeling.cpp , h 라이브러리를 활용해서 라벨링을 해주었으며, test_pub.cpp 라는 ros 를 이용한 subscriber 와publisher 를 해주기위한 노드를 따로 구성하였습니다. (윈도우기반에서는 소스가 동작하지 않는것 양해해주시기 바랍니다.)


4.사용  알고리즘 : YUV를 기반으로 한 skin data 추출, camshift 와 마우스 이벤트를 활용한 얼굴 추적 및 제거, 배경제거 알고리즘, 모폴로지 등 필터, face cascade (처음 사용후 camshift로 변경), 라벨링, AND ,MUL 등의 각종 연산, ROI를 활용한 관심영역설정 등

(얼굴을 제외한 움직이는 살색을 검출하고 최대한 주변의 상황에 덜 영향을 받도록 구현. 최대한 깨끗한 이미지로 잡음제거를 하고 2차원 평면상에서 좌 우 전진 후진 등의 기능을 깔끔하게 구현할 수 있도록 함)

+ GAZEBO 와의 연동을 위해 따로 test_pub.cpp 라는 노드구성.
gazebo 에서의 사용 토픽과 메시지를 확인하여 연동시킴.
따로 map에 관한 gazebo 패키지를 사용하여 좀 더 실감나게 구성
  

5. 알고리즘 문제점: 사람이 여러명 있을때 특히 움직일 경우 손만 제대로 라벨링 하여 검출하지 못함. (한 사람이 앉아서 본 프로젝트를 시행할 경우에 해당해서 성능이 괜찮음)
또한 얼굴마스킹을 camshift를 이용해서 얼굴이 움직일 경우 꾸준히 마스킹 해줄 수 있지만, 손이 겹칠경우는 성능이 좋지 않음.
조명의 영향을 비교적 덜 받는 편이지만, 무시할 수 없음.
라벨링 알고리즘이 크기 제한이 있어 거리에 따라 라벨링을 검출하지 못하는 경우 발생. 



5. 참고자료 : 

http://blog.naver.com/phs6669/100141856073?copen=1&focusingCommentNo=17709876 (바간블로그)

http://cafe.naver.com/opencv/ (네이버 opencv 카페)

http://cafe.naver.com/openrt (오로카카페)

wiki.ros.org (ros 대백과) 등을 참고 하였습니다.
