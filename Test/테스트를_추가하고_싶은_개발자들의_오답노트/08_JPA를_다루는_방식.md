## JPA 분리

### Repository를 다루는 방식
1. JpaRepository as Repository
    
    : 인터페이스에 직접 사용하는 방법
    
    - 서비스 구현체가 JpaRepository에 바로 의존 하는 방식
        
        `public interface UserRepository extends JpaRepository*<UserEntity, Long>`
        
    - JpaRepository도 Interface이기 때문에 Fake를 사용하여 소형 테스트를 만들 수 있다 하지만 아래의 문제점이 발생한다
        1. Fake가 불필요한 인터페이스를 구현해야한다
        2. Service가 Repository의 불필요한 모든 메소드에 대해 알게된다
        3. Domain Entity가 영속성 Entity에 종속된다
        4. Service는 Jpa에 의존된다
2. JpaRepository as RepositoryImpl
    
    : Repository의 구현체로 쓰는 방법
    
    - Repository의 구현체가 JpaRepository 인터페이스를 상속하게 만드는 것
        
        RepositoryImpl extends JpaRepository
        
        (잘 이해가 안되지만 테스트 해봤더니 되긴 한다고 함..)
        
    - 이와 같이 구성하게되면 불필요한 인터페이스를 구현해줄 필요가 없어진다
    - 하지만 아래의 문제점이 발생한다
        1. Domain Entity가 Persistence Entity에 종속된다
            
            ⇒ 구현제가 영속성 객체를 반환해야하기 때문에 Repository의 출력도 영속성 객체여야한다
            
        2. 결국 마찬가지로 Service는 Jpa에 의존된다
3. JpaRepository as RepositoryImpl`s member
    
    : Repository의 구현체의 멤버 변수로 쓰는 방법
        

### 서비스 레이어

- 서비스 레이어는 추상화 되어야 하는가?
    - 강사의 사견: 유스케이스를 분리했을 때 얻는 장점을 체감하지 못한다면, 서비스 레이어를 굳이 추상화 할 필요가 없다고 생각된다.
    

## DDD와 클린 아키텍처

- 비즈니스를 집중하는 방법: DDD
- 비즈니스를 잘 짜는 방법: 테스트
- 비즈니스와 기술을 분리하는 방법: 클린 아키텍처
- 비즈니스와 기술을 분리하는 구체적인 방법: 헥사고날 아키텍처