# Zoned Namespace를 이용한 SSD 성능 Isolation 기법 연구
# 1. 프로젝트 소개
- 프로젝트 명
  - Zoned Namespace를 이용한 SSD 성능 Isolation 기법 연구
- 배경
  - **ZNS SSD**(Zoned Namespace SSD)는 메모리를 **Zone 단위로 구별하여 사용하는 SSD**로, 성능 및 공간 효율이 일반 SSD 보다 높다.
  - **Linux Container**란 운영체제 수준의 가상화 기술로 단일 리눅스 커널에서 동작하고 있는 **각 프로세스를 격리시켜 독자적인 리눅스 시스템 환경을 구축**하는 것이다.
- 목표
 <img width="625" alt="image" src="https://github.com/pnucse-capstone/capstone-2023-1-47/assets/83194164/a8de03a5-1148-4738-99d4-6e8781c35859">
  - **Dm-zoned**는 리눅스 커널에서 **기존의 파일 시스템과 ZNS SSD를 연결**해주는 역할을 하는 Device Mapper이다.
  - 기존의 Dm-zoned를 이용하면 컨테이너간의 Zone 격리가 일어나지 않아 **I/O 간섭**이 생긴다.
  -> **컨테이너간의 Zone 분리 할당 정책**을 개발하여 **I/O를 격리시키고 컨테이너의 성능을 향상** 시키는 것이 본 과제의 목표이다.
# 2. 팀 소개
|팀원|이메일|역할|
|---|---|---|
|윤건우|glove2275@gmail.com|- dm-zoned 코드 분석 : bio, chunk<br>- Chunk – Group 매핑 알고리즘 설계<br>-  I/O Isolation 성능 평가|
|황인욱|arheon2469@gmail.com|- 리눅스 환경 설정<br>- dm-zoned 코드 분석 : 구조체, bio<br>- 구조체 및 알고리즘 테스트 및 디버깅|
|조준서|monstazo911@gmail.com|- 커널 분석 환경 설정<br>- dm-zoned 코드 분석 : 구조체, chunk 관련<br>- Chunk – Group 매핑 구조체 설계|
# 3. 구성도

### 청크-그룹 매핑 테이블
<img width="460" alt="image" src="https://github.com/pnucse-capstone/capstone-2023-1-47/assets/83194164/4a36785f-8c81-4e8e-adac-3c0f292c8efb">
- Chunk와 Cgroup 사이의 매핑 관계를 배열로 저장한다.
- 특정 Cgroup에게 할당된 Chunk를 기억한 후, 다른 Cgroup은 해당 Chunk에 할당되지 않도록 한다.

### Zone 할당 과정
<img width="1218" alt="image" src="https://github.com/pnucse-capstone/capstone-2023-1-47/assets/83194164/d2243e60-0bc5-40db-8e5c-dd840eceed52">
1. I/O를 실행하기 위해 컨테이너가 Dm-zoned에 요청
2. 해당 컨테이너의 cgroup id를 확인
3. 매핑 테이블을 확인하여, 해당 cgroup에 할당된 chunk가 없으면 새로운 chunk 할당 후 I/O 작업 요청
4. 이미 할당된 chunk가 있다면 해당 chunk에 I/O 작업 요청
5. chunk는 zone과 1:1 매핑되어 I/O 처리

# 4. 소개 및 시연 영상
# 5. 사용법
