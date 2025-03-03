---
title: Oak 업그레이드를 사용하여 AEM 6.5에서 AEM 6.5로 LTS 컨텐츠 마이그레이션
description: oak 업그레이드 도구를 사용하여 AEM 6.5에서 AEM 6.5 LTS로 콘텐츠를 마이그레이션하는 방법에 대해 알아봅니다
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8798c608ea168d753be2a08b25a0d0d344b0fef6
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Oak 업그레이드를 사용하여 AEM 6.5에서 AEM 6.5로 LTS 컨텐츠 마이그레이션 {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

이 문서에서는 정밀하고 통제된 상태로 다른 저장소 간에 콘텐츠를 전송할 수 있는 강력한 유틸리티인 oak-upgrade 도구를 사용한 콘텐츠 저장소 마이그레이션에 중점을 두고 Adobe Experience Manager을 버전 **6.5**&#x200B;에서 **6.5 LTS**(으)로 업그레이드하는 방법에 대한 포괄적인 안내서를 제공합니다.

## 사전 요구 사항 {#prerequisites}

마이그레이션을 시작하기 전에 다음 요구 사항이 충족되는지 확인하십시오.

1. Java 호환성: AEM 6.5 LTS가 Java 17에서 실행되도록 설치 및 구성되어야 합니다. 설정되면 AEM 인스턴스를 시작하고 모든 번들이 활성 상태이며 문제 없이 실행되는지 확인합니다
1. 시스템 리소스: 마이그레이션 프로세스 중에 두 저장소를 모두 처리할 수 있는 적절한 디스크 공간 및 메모리를 확보하십시오
1. Oak 업그레이드 도구: [공식 Maven 저장소](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade)에서 `oak-upgrade` jar를 다운로드합니다. 버전이 AEM 6.5 LTS에서 사용되는 oak-core 버전과 일치하는지 확인하십시오. Oak 업그레이드 도구는 Oracle Java 11 이상에서 실행됩니다

## 단계별 마이그레이션 프로세스 {#step-by-step-migration-process}

### AEM 6.5 및 AEM 6.5 LTS 중지 {#stopping-aem65-and-aem65lts}

마이그레이션을 시작하기 전에 AEM 6.5 및 AEM 6.5 LTS 인스턴스를 중지합니다. 이렇게 하면 저장소가 안정적인 상태에 있고 마이그레이션 중에 추가 쓰기가 발생하지 않습니다.

### AEM 6.5 인스턴스 백업 {#backing-up-the-aem65-instance}

아직 백업하지 않은 경우 AEM 6.5 인스턴스의 전체 백업을 수행합니다.

### 컨텐츠 마이그레이션에 Oak 업그레이드 도구 사용 {#using-the-oak-upgrade-tool-for-content-migration}

Oak 업그레이드 도구는 다음과 같이 명령줄을 통해 실행됩니다.

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

다음은 필수 명령 및 옵션입니다.

**키 옵션**

* `--include-paths`: 마이그레이션에 포함할 하위 트리를 지정하십시오. 명령 사용법은 다음 예를 참조하십시오.

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`: 마이그레이션에서 특정 경로를 제외합니다. 이 옵션을 사용하는 동안 주의하십시오. 대상 시스템에 경로가 있으면 제거됩니다. 명령 사용법은 다음 예를 참조하십시오.

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`: 기본적으로 oak-upgrade는 바이너리에 대한 참조만 마이그레이션하여 실제 파일을 원래 blob/데이터 저장소에 남깁니다. 따라서 새 저장소는 여전히 바이너리 소스 저장소에 의존합니다. 저장소 콘텐츠와 함께 바이너리를 마이그레이션하려면 아래와 같이 `--copy-binaries` 매개 변수를 사용하여 모든 바이너리 데이터를 새 저장소에 복사합니다.

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### 체크포인트 마이그레이션 {#migratiing-checkpoints}

이전 SegmentMK 저장소(Oak 1.6 이전)를 새 SegmentMK(Oak 버전이 1.6보다 크거나 같음)로 마이그레이션할 때 체크포인트도 마이그레이션됩니다. 따라서 새 저장소에서 Oak을 처음 실행할 때 리인덱싱을 방지할 수 있습니다. 단, 다음과 같은 경우에는 체크포인트가 마이그레이션되지 않습니다.

1. 사용자 지정 포함, 제외 또는 병합 경로가 지정되거나
1. 바이너리는 참조에 의해 복사되며 소스 데이터 저장소는 지정되지 않고 두 개의 다른 체크포인트에 동일한 경로 아래에 다른 바이너리가 포함됩니다.

두 번째 경우 oak 업그레이드는 다음과 같은 경고와 중단을 발생시킵니다.

```
Checkpoints won't be copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

이 문제를 해결하는 가장 쉬운 방법은 명령줄 옵션(예: `--src-datastore` 또는 `--src-s3datastore`)에서 소스 데이터 저장소를 지정하는 것입니다.

경고는 무시할 수도 있지만, 이 경우 저장소는 처음 시작할 때 완전히 다시 인덱싱됩니다. 특히 큰 사건에 있어서 그것은 긴 과정일 수도 있습니다. 리인덱싱 프로세스가 완료될 때까지 저장소를 사용할 수 없습니다. `--skip-checkpoints` 옵션을 사용하여 경고를 표시하지 않습니다.

[오프라인 리인덱싱](/help/sites-deploying/upgrade-offline-reindexing.md)를 사용하여 AEM을 시작하기 전에 저장소를 오프라인 리인덱싱할 수도 있습니다. 처음 시작할 때 전체 리인덱싱을 사용하지 않도록 하십시오.