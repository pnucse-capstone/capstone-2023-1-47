# Zoned Namespace를 이용한 SSD 성능 Isolation 기법 연구
# 1. 프로젝트 소개
## 1.1 배경
  현재 Linux 커널에서는 ZNS SSD를 저장소로 사용하기 위해 dm-zoned라는 Device Mapper를 사용한다. 컨테이너들을 생성한 후, 입출력을 요청하면 dm-zoned에 의해 요청들이 청크(Chunk)에 모이게 되고 청크의 요청들은 매핑된 각 존에 쓰여지게 된다. 하지만 현재 dm-zoned의 입출력 요청들은 어떤 컨테이너로부터 생성되었는지 구분되지 않은 채 청크에 모인다. 따라서 결국 여러 컨테이너에서 생성된 입출력 요청들이 구분되지 않은 채 하나의 청크에 같이 쓰여지고 존에 매핑되고 저장된다. 결과적으로 컨테이너 간의 데이터 격리가 이루어지지 않게 된다.
# 2. 팀 소개
|팀원|이메일|역할|
|---|---|---|
|윤건우|glove2275@gmail.com|- dm-zoned 코드 분석 : bio, chunk<br>- Chunk – Group 매핑 알고리즘 설계<br>-  I/O Isolation 성능 평가|
|황인욱|arheon2469@gmail.com|- 리눅스 환경 설정<br>- dm-zoned 코드 분석 : 구조체, bio<br>- 구조체 및 알고리즘 테스트 및 디버깅|
|조준서|monstazo911@gmail.com|- 커널 분석 환경 설정<br>- dm-zoned 코드 분석 : 구조체, chunk 관련<br>- Chunk – Group 매핑 구조체 설계|
# 3. 구성도
##
## 3. 개선된 동작 방식
![image](https://github.com/pnucse-capstone/capstone-2023-1-47/assets/97718735/4aa7298c-c6d2-45d7-a694-69a6f271ea8d)
# 4. 소개 및 시연 영상
# 5. 사용법
