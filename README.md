# Zoned Namespace를 이용한 SSD 성능 Isolation 기법 연구
# 1. 프로젝트 소개
- 프로젝트 명
  - Zoned Namespace를 이용한 SSD 성능 Isolation 기법 연구
- 배경
    <img width="556" alt="image" src="https://github.com/pnucse-capstone/capstone-2023-1-47/assets/83194164/523f8b6b-2605-4b99-91ab-c914b81c9dd0">
  - **ZNS SSD**(Zoned Namespace SSD)는 메모리를 **Zone 단위로 구별하여 사용하는 SSD**로, 성능 및 공간 효율이 일반 SSD 보다 높다.
  <img width="525" alt="image" src="https://github.com/pnucse-capstone/capstone-2023-1-47/assets/83194164/77592bbe-ff49-4e58-8ca7-cf7de99fe48f">
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

## 3. 개선된 동작 방식
![image](https://github.com/pnucse-capstone/capstone-2023-1-47/assets/97718735/4aa7298c-c6d2-45d7-a694-69a6f271ea8d)
# 4. 소개 및 시연 영상
# 5. 사용법
