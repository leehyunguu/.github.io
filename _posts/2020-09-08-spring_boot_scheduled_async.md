---
title: Spring boot Scheduled Async
date: 2020-09-08
categories: spring-boot
---
스케줄을 추가하면서 스케줄이 다음 스케줄 시작시간보다 오래 걸릴경우 스케줄이 Skip되는 현상을 봤다.

```java
@Scheduled(cron = "0/1 * * * * *")
public void sleep() {
    Thread.sleep(5000);
}
```

이렇게 될 경우 5초 Sleep시간에 1초마다 실행되는 Schedule이 Skip이 되었다.

이 현상을 해결 하려고 config파일에

```yaml
spring:
  task:
    scheduling:
      pool:
        size: 2
```

라고 추가했지만, 역시 작동하지 않았다. 

찾아보니 위 설정은 한번에 실행되는 Schedule의 size를 설정하는 값이었다.

Schedule이 두개이고, 같은 시간에 실행될 경우 위 값이 없으면(Default: 1) 한개씩만 실행되게 된다. 

따라서 내가 원하는 하나의 Schedule에서 중복해서 실행하는 설정값이 아니었다.

그래서 @Async를 사용하기로 했다.

```java
@Scheduled(cron = "0/1 * * * * *")
@Async
public void sleep() {
    Thread.sleep(5000);
}
```

물론 ```@EnableAsync``` 설정을 해주어야 한다.

위를 실행할 경우 Thread 명은 schedule에서 task로 변경 되고, 이전 스케줄이 오래걸려도 시간에 맞춰 다음 스케줄이 실행된다.

Async의 기본 pool size는 8이고, 수정하려면

```yaml
spring:
  task:
    execution:
      pool:
        core-size: 10
```

이렇게 설정하면 된다.

만약 오래걸리지만 지정된 시간마다 해야하는 스케줄이라면 이렇게 설정하고 쓰면 될 것 같다.
