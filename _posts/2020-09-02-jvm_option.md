---
title: JVM 변수
date: 2020-09-02
categories: jvm
---
이번에 인수 가이드대로 JVM 환경변수를 적용하면서,

기존에 알고 있었던 것도 있고, 새롭게 알게 된 것도 있다.

나중에 언제 써먹을지 몰라 최대한 정리하려고 한다.

잘 모르는 부분도 있다.

공식으로 제공하는 가이드는 [이곳(Java 8)]에 있다.

|옵션|설명|
|---|---|
|-Xms1024m|Heap 메모리 최소 Size|
|-Xmx1024m|Heap 메모리 최대 Size|
|-XX:NewSize=256m|New 영역 최소 Size|
|-XX:MaxNewSize=256m|New 영역 최대 Size|
|-XX:SurvivorRatio=8|New 영역 내 Survivor 영역과 Eden 영역의 비율 설정(1:8)[[참고1]]|
|-XX:MetaspaceSize=256m|MetaspaceSize 영역 최소 Size(1.8 이전:-XX:PermSize)|
|-XX:MaxMetaspaceSize=512m|MetaspaceSize 영역 최대 Size(1.8 이전:-XX:MaxPermSize)|
|-XX:MaxDirectMemorySize=512m|Non-heap 메모리 최대 Size 설정[[참고2]]|
|-XX:+UseParallelGC|Miner GC를 병렬로 처리|
|-XX:ParallelGCThreads=20|동시에 GC를 수행할 Thread 갯수 설정|
|-XX:MaxGCPauseMillis=200|최대 GC 중지 시간|
|-XX:+UseG1GC|G1GC를 사용하도록 설정[[참고3]]|
|-XX:+UnlockExperimentalVMOptions|VM 플래그를 확장|
|-XX:+UnlockDiagnosticVMOptions|VM 플래그를 확장|
|-XX:+G1SummarizeConcMark|Concurrent Marking 정보를 출력[[참고4]]|
|-XX:InitiatingHeapOccupancyPercent=45|설정된 Heap 메모리 사용 비율에 따라 GC 발생|
|-XX:G1ReservePercent=10|오버플로우 위험을 감소시키기 위해 예비 메모리를 백분율로 설정|
|-XX:G1HeapRegionSize=32m|Heap 영역을 균일한 크기의 영역으로 세분화 설정 시 사용|
|-XX:+UseParallelOldGC|Major GC를 병렬로 처리|
|-XX:+UseConcMarkSweepGC|성능은 낮지만, GC로 인한 정지시간 최소화|
|-XX:+UseParNewGC|Minor GC에서 Parallel Collector를 활성화(CMS GC에서는 필수)|
|-verbose:gc|GC 로그 사용|
|-Xloggc:<path>|GC 로그 위치 설정|
|-XX:+PrintGCDetails|GC 완료된 후 자세한 내용 로그 남기기|
|-XX:+PrintGCTimeStamps|GC 발생 시 JVM 기준의 시작 시간을 로그에 남기도록 설정|
|-XX:+PrintHeapAtGC|GC 발생 전 후의 Heap에 대한 정보 기록|
|-XX:+UseGCLogFileRotation|GC 로그 Rotation 설정|
|-XX:NumberOfGCLogFiles=9|Rotate 로그 갯수 설정|
|-XX:GCLogFileSize=20m|로그 로테이트를 수행할 기준 용량|
|-XX:+HeapDumpOnOutOfMemoryError|Out Of Memory 발생 시 Heap Dump가 발생하도록 설정|
|-XX:HeapDumpPath=<path>|Heap Dump 발생 위치|

[이곳(Java 8)]: https://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html
[참고1]: https://ukzzang.tistory.com/32
[참고2]: https://www.samsungsds.com/global/ko/support/insights/1209234_2284.html
[참고3]: https://initproc.tistory.com/entry/G1-Garbage-Collection
[참고4]: https://wiki.openjdk.java.net/display/HotSpot/G1GC+Feedback
