---
title: 즉석 업그레이드 수행
description: AEM 6.5 LTS에 대한 즉각적 업그레이드를 수행하는 방법을 알아봅니다.
topic-tags: upgrading
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 67bd9b29ccc525111710a397cca5de1c961486ac
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# 즉석 업그레이드 수행 {#performing-an-in-place-upgrade}

>[!NOTE]
>
>이 페이지에서는 AEM 6.5 LTS의 즉각적 업그레이드 절차에 대해 간략히 설명합니다. 응용 프로그램 서버에 배포된 설치가 있는 경우 [응용 프로그램 서버 설치에 대한 업그레이드 단계](/help/sites-deploying/app-server-upgrade.md)를 참조하십시오.

## 업그레이드 전 단계 {#pre-upgrade-steps}

업그레이드를 실행하기 전에 완료해야 하는 몇 가지 단계가 있습니다. 자세한 내용은 [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md) 및 [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)을 참조하십시오. 또한 시스템이 [AEM 6.5 LTS에 대한 요구 사항](/help/sites-deploying/technical-requirements.md)을 충족하는지 확인하고 [업그레이드 계획 고려 사항](/help/sites-deploying/upgrade-planning.md) 및 [Analyzer](/help/sites-deploying/pattern-detector.md)를 통해 복잡성을 추정하는 방법을 확인하십시오.

<!--Finally, the downtime during the upgrade can be significally reduced by indexing the repository **before** performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

## 마이그레이션 사전 요구 사항 {#migration-prerequisites}

* **필요한 최소 Java 버전:** 시스템에 Oracle의 Java™ 17이 설치되어 있는지 확인하십시오.

## AEM Quickstart jar 파일 준비 {#prep-quickstart-file}

1. 새 AEM 6.5 LTS jar 파일 다운로드

1. [올바른 업그레이드 시작 명령 확인](/help/sites-deploying/in-place-upgrade.md#determining-the-correct-upgrade-start-command-determining-the-correct-upgrade-start-command)

1. 실행 중인 경우 인스턴스 중지

1. 새 AEM 6.5 LTS jar을 사용하여 `crx-quickstart` 폴더 외부의 이전 LTS Jar을 바꿉니다

1. `sling.properties` 파일(일반적으로 `crx-quickstart/conf/`에 있음)을 백업한 다음 삭제합니다.

1. 다음을 실행하여 새 quickstart jar 압축을 해제합니다.

   ```shell
   java -Xmx4096m -jar aem-quickstart.jar -unpack
   ```

1. 압축 해제 명령은 `crx-quickstart/conf/` 폴더 아래에 새 `sling.properties` 파일을 생성합니다. 이제 새로 생성된 `sling.properties` 파일에 사용자 지정 변경 사항을 적용할 수 있습니다.

<!-- Alexandru: drafting temporarily

## Content Repository Migration {#content-repository-migration}

This migration is not required if you are upgrading from AEM 6.3. For versions older than 6.3, Adobe provides a tool that can be used to migrate the repository to the new version of the Oak Segment Tar present in AEM 6.3. It is provided as part of the quickstart package and is mandatory for any upgrades that will be using TarMK. Upgrades for environments that are using MongoMK do not require repository migration. For more information on what the benefits of the new Segment Tar format are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions).

The actual migration is performed using the standard AEM quickstart jar file, executed with a new `-x crx2oak` option which executes the crx2oak tool to simplify the upgrade and make it more robust.

>[!NOTE]
>
>If you are performing TarMK repository content migration using the CRX2Oak Quickstart extension, you might remove the **samplecontent** runmode by adding the following to the migration command line:
>
>* `--promote-runmode nosamplecontent`
>

To determine the command that you should run, use the following command:

```shell
java -Xmx4096m -jar aem-quickstart.jar -v -x crx2oak -xargs -- --load-profile <<YOUR_PROFILE>> <<ADDITIONAL_FLAGS>>
```

Where `<<YOUR_PROFILE>>` and `<<ADDITIONAL_FLAGS>>` are replaced with the profile and flags listed in the following table:

<table>
 <tbody>
  <tr>
   <td><strong>Source Repository</strong></td>
   <td><strong>Target Repository</strong></td>
   <td><strong>Profile</strong></td>
   <td><strong>Additional Flags</strong><br /> </td>
  </tr>
  <tr>
   <td>crx2 or TarMK with <code>FileDataStore</code></td>
   <td>TarMK</td>
   <td>segment-fds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>crx2</td>
   <td>MongoMK</td>
   <td>mongo-from-crx2 </td>
   <td><code>-T mongo-uri=mongo://mongo-host:mongo-port -T mongo-db=mongo-database-name</code></td>
  </tr>
  <tr>
   <td>TarMK or crx2 with <code>S3DataStore</code></td>
   <td>TarMK</td>
   <td>segment-custom-ds</td>
   <td>See Troubleshooting section below</td>
  </tr>
  <tr>
   <td>TarMK with no datastore</td>
   <td>TarMK</td>
   <td>segment-no-ds</td>
   <td> </td>
  </tr>
  <tr>
   <td>MongoMK</td>
   <td>MongoMK</td>
   <td>No migration is needed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

**Where:**

* `mongo-host` is the MongoDB server IP (for example, 127.0.0.1)

* `mongo-port` is the MongoDB server port (for example: 27017)

* `mongo-database-name` represents the name of the database (for example: aem-author)

**You may also require additional switches for the following scenarios:**

* If you are performing the upgrade on a Windows system where Java memory mapping is not handled correctly, add the `--disable-mmap` parameter to the command.

For additional instructions on using the crx2oak tool, see Using the [CRX2Oak Migration Tool](/help/sites-deploying/using-crx2oak.md). The crx2oak helper JAR can be manually upgraded if needed, by manually replacing it with newer versions after unpacking the quickstart. Its location in the AEM installation folder is: `<aem-install>/crx-quickstart/opt/extensions/crx2oak.jar`. The newest version of the CRX2Oak migration tool is available for download from the Adobe Repository at: [https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)

If the migration has completed successfully, the tool will exit with an exit code of zero. Additionally, check for WARN and ERROR messages in the `upgrade.log` file, located under `crx-quickstart/logs` in the AEM installation directory, as these could indicate non-fatal errors that occurred during the migration.

Check the configuration files beneath `crx-quickstart/install` folder. If a migration was necessary these will be updated to reflect the target repository.

**A note on datastores:**

While `FileDataStore` is the new default for AEM 6.3 installations, using an external datastore is not required. While using an external datastore is recommended as a best practice for production deployments, it is not a prerequisite to upgrade. Due to the complexity already present in upgrading AEM, Adobe recommends performing the upgrade without doing a datastore migration. If desired, a datastore migration can be executed afterwards as a separate effort.

## Troubleshooting Migration Issues {#troubleshooting-migration-issues}

Skip this section if you are upgrading from 6.3. While the provided crx2oak profiles should meet the needs of most customers, there are times when additional parameters will be necessary. If you run into an error during your migration, it is possible that there are aspects of your environment that require additional configuration options to be provided. If so, you will likely encounter the following error:

**Checkpoints are not copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info.**

For some reason, the migration process needs access to binaries in the datastore and is unable to find it. To specify your datastore configuration, include the following flags in the `<<ADDITIONAL_FLAGS>>` portion of your migration command:

**For S3 datastores:**

```shell
--src-s3config=/path/to/SharedS3DataStore.config --src-s3datastore=/path/to/datastore
```

Where `/path/to/SharedS3DataStore.config` represents the path to your S3 datastore config file and `/path/to/datastore` represents the path to your S3 datastore.

**For File datastores:**

```shell
--src-datastore=/path/to/datastore
```

Where `/path/to/datastore` represents the path to your File Datastore.

-->

## 업그레이드 수행 {#performing-the-upgrade}

**S3을 사용하는 경우:**

1. 이전 버전의 S3 커넥터와 연결된 `crx-quickstart/install` 아래의 jar를 제거합니다.

1. [https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/) <!-- Alexandru: this is a stub link for now -->에서 1.60.2 S3 커넥터의 최신 릴리스를 다운로드하십시오.

1. S3 커넥터(버전 1.60.2)를 추출하고 `crx-quickstart/install` 아래에 있는 다음 폴더의 내용을 다음과 같이 복사합니다.

   1. `crx-quickstart/install/1` 아래의 `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/1` 복사
   1. `crx-quickstart/install/15` 아래의 `com.adobe.granite.oak.s3connector-1.60.2/jcr_root/libs/system/install/15` 복사

이제 [올바른 업그레이드 시작 명령 결정](#determining-the-correct-upgrade-start-command) 섹션의 정보를 사용하여 결정된 새 명령을 사용하여 AEM 인스턴스를 시작합니다.

### 올바른 업그레이드 시작 명령 확인 {#determining-the-correct-upgrade-start-command}

>[!NOTE]
>
>Java 17에서 일부 Java 8/11 인수에 대한 지원이 제거되었습니다. [Oracle Java™ 17 문서](https://docs.oracle.com/en/java/javase/17/docs/specs/man/java.html) 및 [AEM 6.5 LTS에 대한 Java&amp;trade 인수 고려 사항](/help/sites-deploying/custom-standalone-install.md#java-17-considerations-java-considerations)을 참조하십시오.

업그레이드를 실행하려면 jar 파일을 사용하여 AEM을 시작하여 인스턴스를 불러오는 것이 중요합니다.

시작 스크립트에서 AEM을 시작하면 업그레이드가 시작되지 않습니다. 대부분의 고객은 시작 스크립트를 사용하여 AEM을 시작하고 메모리 설정, 보안 인증서 등과 같은 환경 구성을 위한 스위치를 포함하도록 이 시작 스크립트를 사용자 정의했습니다. 이러한 이유로 Adobe에서는 다음 절차에 따라 적절한 업그레이드 명령을 결정할 것을 권장합니다.

1. 실행 중인 AEM 인스턴스에서 명령줄에서 다음을 실행합니다.

   ```shell
   ps -ef | grep java
   ```

1. AEM 프로세스를 찾습니다. 다음과 같이 표시됩니다.

   ```shell
   /usr/bin/java -server -Xmx1024m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar crx-quickstart/app/cq-quickstart-6.5.0-standalone-quickstart.jar start -c crx-quickstart -i launchpad -p 4502 -Dsling.properties=conf/sling.properties
   ```

1. 기존 jar(이 경우 `crx-quickstart/app/aem-quickstart*.jar`)에 대한 경로를 `crx-quickstart` 폴더의 형제 항목인 새 AEM 6.5 LTS jar로 대체하여 명령을 수정합니다. 이전 명령을 예로 들면 다음과 같습니다.

   ```shell
   /usr/bin/java -server -Xmx4096m -Djava.awt.headless=true -Dsling.run.modes=author,crx3,crx3tar -jar <AEM-6.5-LTS.jar> -c crx-quickstart -p 4502 -Dsling.properties=conf/sling.properties
   ```

   이렇게 하면 모든 적절한 메모리 설정, 사용자 지정 실행 모드 및 기타 환경 매개 변수가 업그레이드에 적용됩니다. 업그레이드가 완료되면 이후 시작의 시작 스크립트에서 인스턴스를 시작할 수 있습니다.

## 업그레이드된 코드베이스 배포 {#deploy-upgraded-codebase}

즉각적 업그레이드 프로세스가 완료되면 업데이트된 코드 베이스를 배포해야 합니다. 대상 버전의 AEM에서 작동하도록 코드 베이스를 업데이트하는 단계는 [코드 및 사용자 지정 업그레이드 페이지](/help/sites-deploying/upgrading-code-and-customizations.md)에서 확인할 수 있습니다.

## 업그레이드 후 확인 및 문제 해결 수행 {#perform-post-upgrade-check-troubleshooting}

[업그레이드 확인 후 및 문제 해결](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)을 참조하세요.
