---
title: AEM Forms Android 앱 빌드
description: Android Studio 프로젝트를 설정하고 Android용 AEM Forms 앱용 .apk 파일을 작성하는 절차
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: a804ba9b-c5c6-4d76-96e4-5d729b673ca4
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 3%

---

# AEM Forms Android 앱 빌드 {#build-the-aem-forms-android-app}

AEM Forms용 Android 앱을 빌드하려면 권장 시퀀스에서 다음 단계를 수행하십시오.

1. [AEM Forms 앱 Source 코드 패키지 다운로드](#download-android-zip)
1. [환경 변수 설정](#set-environment-variable-android)
1. [표준 AEM Forms 앱 빌드](#set-up-the-xcode-project)

## AEM Forms 앱 Source 코드 패키지 다운로드 {#download-android-zip}

AEM Forms 앱 Source 코드 패키지가 `adobe-lc-mobileworkspace-src-<version>.zip` 보관 파일을 참조합니다. 이 아카이브에는 사용자 지정 AEM Forms 앱을 빌드하는 데 필요한 소스 코드가 포함되어 있습니다. 소프트웨어 배포에서 사용할 수 있는 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 패키지에 보관이 포함되어 있습니다.

`adobe-aemfd-forms-app-src-pkg-<version>.zip` 파일을 다운로드하려면 다음 단계를 수행하십시오.

1. [소프트웨어 배포](https://experience.adobe.com/downloads)를 엽니다. 소프트웨어 배포에 로그인하려면 Adobe ID가 필요합니다.
1. 헤더 메뉴에서 사용할 수 있는 **[!UICONTROL Adobe Experience Manager]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 필터]** 섹션에서:
   1. **[!UICONTROL 솔루션]** 드롭다운 목록에서 **[!UICONTROL Forms]**&#x200B;을(를) 선택합니다.
   2. 패키지의 버전 및 유형을 선택합니다. **[!UICONTROL 다운로드 검색]** 옵션을 사용하여 결과를 필터링할 수도 있습니다.
1. 운영 체제에 적용할 수 있는 패키지 이름을 선택하고 **[!UICONTROL EULA 약관 동의]**&#x200B;를 선택한 다음 **[!UICONTROL 다운로드]**&#x200B;를 선택합니다.
1. [패키지 관리자](/help/sites-administering/package-manager.md)를 열고 **[!UICONTROL 패키지 업로드]**&#x200B;를 클릭하여 패키지를 업로드합니다.
1. 패키지를 선택하고 **[!UICONTROL 설치]**&#x200B;를 클릭합니다.
1. 소스 코드 아카이브를 다운로드하려면 브라우저에서 **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip**&#x200B;을 엽니다. Android 앱 .zip 파일이 장치에 다운로드됩니다.
1. 로컬 파일 시스템의 폴더에 .zip 파일의 압축을 풉니다. 예: *C:\&lt;폴더 구조>\adobe-lc-mobileworkspace-src-2.4.20*

다음 이미지는 `adobe-lc-mobileworkspace-src-<version>.zip\android`폴더의 구조를 표시합니다.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## 환경 변수 설정 {#set-environment-variable-android}

AEM Forms 앱에 대한 빌드 프로세스를 시작하기 전에 다음 환경 변수를 설정하십시오.

* JAVA_HOME 환경 변수를 로컬 파일 시스템에서 JDK 소프트웨어 위치로 설정합니다. 예: C:\Program Files\Java\jdk1.8.0_181
* `ANDROID_SDK_ROOT` 시스템 환경 변수를 Android의 SDK 위치로 설정합니다. 예: C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Android의 platform-tools 및 tools 폴더 위치를 포함하도록 `Path` 시스템 환경 변수를 설정하십시오. 예: C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools 및 C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools

## 표준 AEM Forms 앱 빌드 {#set-up-the-xcode-project}

로컬 파일 시스템에 adobe-lc-mobileworkspace-src-&lt;version>.zip 파일을 저장하고 환경 변수를 설정한 후 다음 옵션 중 하나를 사용하여 표준 AEM Forms Android 앱을 빌드합니다.

* [Android Studio를 사용하여 AEM Forms 앱 빌드](#using-android-studio)
* [Android Studio를 사용하여 .apk 파일 생성](#generate-apk-android-studio)

### Android Studio를 사용하여 AEM Forms 앱 빌드 {#using-android-studio}

Android Studio를 사용하여 AEM Forms 앱을 빌드하려면 다음 단계를 수행하십시오.

1. 컴퓨터에서 Android Studio 애플리케이션을 실행합니다.
1. **기존 Android Studio 프로젝트 열기**&#x200B;를 클릭합니다. 기존 프로젝트를 여는 대화 상자가 자동으로 나타나지 않으면 **파일** > **열기**&#x200B;를 선택하십시오.
1. 로컬 파일 시스템에서 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android*(으)로 이동한 다음 **확인**&#x200B;을 클릭합니다.

   **android** 옵션이 왼쪽 창에 표시됩니다.

   ![android_folder_studio](assets/android_folder_studio.png)

1. 왼쪽 창에서 **android**&#x200B;을(를) 선택하고 **실행** > **&#39;android&#39; 실행**&#x200B;을 클릭합니다.
1. [배포 대상 선택] 대화 상자의 [연결된 장치] 섹션에서 Android 장치를 선택하고 [확인]을 클릭합니다.

   개발 환경을 성공적으로 빌드하면 이제 앱에 사용자 지정을 적용할 수 있습니다. 다음 문서를 사용하여 앱을 사용자 지정합니다.

   * [브랜딩 사용자 지정](/help/forms/using/branding-customization.md)
   * [테마 맞춤화](/help/forms/using/theme-customization.md)
   * [제스처 사용자 지정](/help/forms/using/gesture-customization.md)

   앱에 적절한 사용자 지정을 적용한 후 배포할 .apk 파일을 생성할 수 있습니다.

### Android Studio를 사용하여 .apk 파일 생성 {#generate-apk-android-studio}

Android Studio를 사용하여 .apk 파일을 생성하려면 다음을 수행합니다.

1. 컴퓨터에서 Android Studio 애플리케이션을 실행합니다.
1. **기존 Android Studio 프로젝트 열기**&#x200B;를 선택합니다. 기존 프로젝트를 여는 대화 상자가 자동으로 나타나지 않으면 **파일** > **열기**&#x200B;를 선택하십시오.
1. 로컬 파일 시스템에서 *adobe-lc-mobileworkspace-src-&lt;version>.zip/android*(으)로 이동한 다음 **확인**&#x200B;을 클릭합니다.

   왼쪽 창에 android 옵션이 표시됩니다.

1. .apk 파일을 생성하려면 **빌드** > **APK 빌드**&#x200B;를 선택하십시오.

   필요한 경우 **빌드** > **서명된 APK 생성**&#x200B;을 선택하여 .apk 파일의 [서명된 버전](https://developer.android.com/studio/publish/app-signing)을(를) 생성합니다.

## Android Debug Bridge 사용 {#build-android-debug-bridge}

.apk 파일이 생성되면 다음 명령을 실행하여 [Android Debug Bridge](https://developer.android.com/tools/adb)를 사용하여 Android 장치에 응용 프로그램을 설치합니다.

**Windows 사용자:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Mac 사용자:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
