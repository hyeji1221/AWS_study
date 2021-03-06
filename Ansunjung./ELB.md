> load balancing -> 접근을 여러 대의 EC2 인스턴스로 분산하는 역할
> + 부하 분산 : 대량의 접근을 여러 개의 인스턴스로
> + 가용성 보장 : 1대의 인스턴스에 장애가 발생할 경우 다른 인스턴스로 서비스 제공

## ELB 서비스 상세



### ELB 서비스의 가용성
+ 요청 처리 능력 : 접속 부하에 맞게 자동적으로 리소스의 확장/축소를 수행 -> 병목현상 중지
+ 확장/축소는 스케일업/스케일다운, 스케일 아웃/스케일인 방식 사용 --> ELB 접근 ip가 변경됨

### 싱글 AZ구성과 멀티 AZ구성
+ 싱글 AZ구성
> DNS 라운드 로빈 방식(단순하게 순서대로 분산)으로 EC2에 요청 분산

+ 멀티 AZ구성
> + AZ 내부에 EC2인스턴스의 개수의 상관없이 동일하게 분산시킴 --> **EC2 인스턴스 수를 동일하게 두어야한다.**
> + 특정 인스턴스에 문제가 발생하면 다른 인스턴스 중에서 특정 인스턴스에 부하가 많이걸림
> + cross-zone load balancing 사용 : 모든 AZ에 존재하는 Ec2인스턴스에 분산


### External-ELB와 internal-ELB
+ External-ELB : 인터넷에서 요청을 받음 -> vpc의 퍼블릭 subnet에 생성
+ internal-ELB : vpc subnet요청만 받음
> 둘이 조합하여 3계층 시스템 구성이 가능함


### 헬스 체크
+ 인스턴스의 상태 감지 -> 문제가 있으면 그 인스턴스에 ELB가 요청을 분산하지 않는다. 
+ **포트감시** : 포트의 listen상태를 감시
+ **서비스 감시** : html 파일 접근 가능여부 확인

### SSL 터미네이션
+ HTTPS 통신에서 사용하는 SSL증명서를 인증하는 기능 --> 각각의 인스턴스가 복호화 암호화를 안해도 되므로 부하를 낯출수 있음

### 스티키 세션
+ 같은 사용자의 요청을 같은 인스턴스에서 처리하게 만드는 기능 -> **ELB아래에 있는 인스턴스틀의 세션 정보를 공유하는 시스템** 사용 권장

### 로그 추출 기능
+ ELB로 처리한 요청 로그를 추출할 수 있음



