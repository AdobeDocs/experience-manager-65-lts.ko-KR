---
title: JBoss EAP 8(Linux)을 사용하는 AEM Forms 6.5 LTS에서 스크립트 실행이 실패합니다
description: Linux 환경에서 JBoss EAP 8.0(AEM Forms 6.5.1 LTS)을 설정하면 셸 스크립트나 시작 파일을 실행하는 동안 오류가 발생할 수 있습니다
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---


# JBoss EAP 8(Linux)을 사용하는 AEM Forms 6.5 LTS에서 스크립트 실행이 실패합니다

## 문제

**Linux** 환경에서 **JBoss EAP 8.0(AEM Forms 6.5.1 LTS)**&#x200B;을(를) 설정할 때 셸 스크립트 또는 시작 파일을 실행하는 동안 다음 오류 중 하나가 발생할 수 있습니다.

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

이러한 오류는 **Windows** 시스템에서 셸 스크립트나 구성 파일을 만들거나 편집하고 **CRLF(캐리지 리턴 + 줄 바꿈)** 줄 끝을 포함할 때 발생합니다.
Linux 시스템은 **LF(줄 바꿈)**&#x200B;개의 줄 끝만 지원하며 Windows 스타일의 줄 끝은 스크립트 실행 실패를 일으킵니다.

## 적용 대상

* **JBoss EAP 8.0**
* **Linux/UNIX 기반 운영 체제**

## 문제 해결 단계

1. **영향을 받는 파일 식별**

   * 오류 출력을 검토하여 오류의 원인이 되는 `.sh` 스크립트 또는 구성 파일을 식별하십시오.

2. **파일을 Unix 형식으로 변환**

   * `dos2unix` 유틸리티를 사용하여 Windows 스타일의 줄 끝을 Unix 형식으로 변환합니다.

     ```bash
     dos2unix <file_name>
     ```

   * `<file_name>`을(를) 오류를 발생시키는 실제 스크립트 또는 구성 파일로 바꾸십시오.

3. **필요한 경우 반복**

   * 여러 스크립트가 영향을 받는 경우 관련된 모든 `.sh` 파일(예: 설치 관리자, LCM 또는 JBoss 시작 스크립트)에 대해 전환을 반복합니다.

4. **스크립트 다시 실행**

   * 변환 후 스크립트를 다시 실행하여 문제가 해결되었는지 확인합니다.

파일을 Unix(LF) 줄 끝으로 변환한 후 `/bin/sh^M` 및 `$'\r': command not found` 오류가 해결되고 JBoss 스크립트가 Linux에서 성공적으로 실행됩니다.
