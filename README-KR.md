# 레노버 Y700 1세대 (TB9707F) 커스텀롬/순정롬 복원 가이드
Y700 1세대 (TB9707F) 태블릿에 관한 커스텀롬/순정롬 정보를 다루는 레포입니다. 현재 한글화 작업 중에 있습니다.

**Y700 2세대 (TB320FU)의 경우, [여기로 이동하십시오.](2023/README-KR.md)**
  
> [!WARNING]  
> 본 가이드를 따라하여 생기는 모든 문제는 사용자 본인에게 있습니다. 본 가이드에서 설명하는 과정은 기기를 벽돌 상태로 만들 수 있으며, [이 경우 여기를 클릭하여 나오는 동영상의 방법을 사용하여 복구를 시도할 수 있습니다.](https://www.youtube.com/watch?v=VaCjtUDoqXA) **필자는 당신의 기기가 어떻게 되든, 책임지지 않습니다.**
</br>

# 📚 목차


롬: 
* ⚡ [부트로더 언락](#blu)
* ⚡ [공식 중국 내수롬 설치 방법 (ZUI 14 안드로이드 12 또는 ZUI 15 안드로이드 13](#stock-rom) -> 소프트브릭 해결
* ⚡ [비공식 ZUI 15(안드로이드 13) OTA 사이드로딩하기](#unofficial-ota)
* ⚡ [GSI 롬(커스텀 롬) 설치](#flash-gsi)
* ℹ️ [Y700 1세대에서 정상 작동이 확인된 커스텀 롬 목록](#info)
* 🛠️ [GSI 롬 문제 해결](#gsifix)
  
<br>

기타 유틸리티: 
* 🦄 [Magisk 설치(태블릿 루팅하기)](#magisk)
* 🚀 [참조 목록](#acknowledgements)

---
<br>

## 부트로더 언락: <a name=blu></a>
설정->"About Tablet(이 태블릿에 관하여)" 로 이동한 다음 ZUI 버전을 여러 번 클릭하여 개발자 설정을 활성화합니다. 비밀번호를 설정한 경우, 비밀번호를 입력해야 활성화할 수 있습니다. <br>
개발자 설정으로 이동한 다음 "OEM 잠금 해제" 와 "USB 디버깅 허용"을 활성화하십시오.<br>
태블릿을 PC에 연결한 다음, 디버깅 허용 여부를 묻는 팝업이 나오면 "허용"을 누릅니다.<br>

PC에서 태블릿을 인식하는지 다음 명령어를 입력하여 확인합니다. ADB가 무엇인지 모르거나, 설치 여부를 모른다면 [여기](https://developer.android.com/tools/releases/platform-tools)로 이동하여 "Download SDK Platform-Tools for Windows/Mac/Linux" 중 자신의 운영체제에 맞는 커맨드 툴을 다운로드하고 적절한 위치에 압축을 푼 다음, cmd 창을 열고 압축을 푼 위치로 cd 명령어를 통해 이동하여 다음 명렁어를 입력합니다.
```
adb devices
```
기기 연결이 확인되면 위 명령어를 입력했을 때 기기의 시리얼 번호, 그리고 device 라는 줄이 출력됩니다. unauthorized 상태인 경우, ADB 권한 허용 팝업에서 허용을 눌렀는지 확인하고, 팝업이 나오지 않았는데 unauthorized 상태인 경우 `adb kill-server` 명령어로 ADB 서버를 종료하고, 태블릿 설정을 열고 개발자도구에서 "USB 디버깅 권한 승인취소" 버튼을 누른 다음 기기와 PC를 연결하는 케이블을 분리한 다음 다시 연결하여 재시도하십시오.

기기 연결이 확인되었으면 다음 명령어를 입력하여 부트로더 모드로 진입합니다.

```
adb reboot bootloader
```

정상적으로 재부팅되었다면 기기가 부트로더 모드로 진입했을 것입니다.<br>
PC에서 태블릿이 **부트로더 모드에 진입한 것을** 인식하는지 다음 명령어를 입력하여 확인합니다:
```
fastboot devices
```
> [!IMPORTANT]  
> fastboot 모드에서 기기가 인식되지 않는 경우 (위 명령어를 입력했을 때 기기가 표시되지 않는 경우): [여기를 참고하여 부트로더 인터페이스 드라이버를 설치하십시오.(영문)](https://droidwin.com/install-google-android-bootloader-interface-drivers/)

기기 연결이 확인되었으면 다음 명령어를 입력하여 부트로더를 언락합니다.:
```
fastboot flashing unlock
```
> [!WARNING]  
> **부트로더 언락 실행과 동시에 공장 초기화가 자동으로 이루어집니다.** 아직 중요한 데이터를 백업하지 않았다면, **아직 늦지 않았으니 기기를 정상 부팅한 다음 중요 데이터를 백업하십시오. 이 작업은 되돌릴 수 없습니다.** </br>
> **부트로더 언락 시 물리적으로 기기가 도난당했을 경우 데이터 유출 위험이 있습니다. 금융 앱과 같은 높은 수준의 보안을 요구하는 앱을 사용하거나, 그러한 데이터를 저장하지 않는 것을 권장합니다.** </br>
> **부트로더 언락 이후, 기기를 재부팅할 때마다 경고 메시지가 표시됩니다. 이는 부트로더를 다시 잠그지 않는 한 제거할 수 없습니다.**


경고 메시지가 표시됩니다. 볼륨 버튼을 이용하여 "UNLOCK THE BOOTLOADER"을 선택한 다음, 전원 버튼을 눌러 부트로더를 언락합니다.<br>
내부 저장소에 저장된 모든 데이터는 이 시점에서 삭제되며, 시스템은 자동으로 재부팅합니다.

정상적으로 부팅되었다면, 부트로더 언락 작업이 완료된 것입니다.

---
<br>

## ⚡ 공식 중국 내수롬(순정) 플래싱하기 (ZUI 14 안드로이드 12 or ZUI 15 안드로이드 13): <a name=stock-rom></a>

> [!WARNING]  
> 이 과정을 진행하려면 부트로더 언락이 필요합니다. 아직 언락하지 않은 경우, [이 포스팅(영문)](https://xdaforums.com/t/guide-unbrick-lenovo-y700-tablet.4509297/)을 참조하십시오. 혹은 위의 `부트로더 언락` 단락을 참고하여도 됩니다.
* ZUI 14, 안드로이드 12: [이 비디오(영문)](https://www.youtube.com/watch?v=VaCjtUDoqXA) 또는 [이 포스팅(영문)](https://xdaforums.com/t/guide-unbrick-lenovo-y700-tablet.4509297/)
* ZUI 15, Android 13: [이 동영상(영문)에서 설치 과정을 확인할 수 있습니다.](https://www.youtube.com/watch?v=aEHFUM-yLt0)

링크: 
* [공식 소스에서 ADB 다운로드](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
* [QFIL - 다운로드 링크](https://qpsttool.com/qpst-tool-v2-7-496)
* [ZUI 14 순정 중국 내수롬](https://drive.google.com/file/d/1P-8sFTtID0StfhNnf1kkROhzv0wHovun/view?usp=sharing)
* [ZUI 15 순정 중국 내수롬](https://drive.google.com/file/d/16PRQV0eE2F2GTm9eaFuoZoqGZgWcSTL_/view?usp=sharing)

Other alternatives: 
* [상기 필요한 모든 파일을 압축해놓은 ZIP파일](https://mega.nz/file/8XU1kLgT#GVKDjBmvmJgXYfxIUEHSxsxSqLjMDmjixbV-W9GYM9w)
* [OTA와 순정 롬을 모아놓은 다른 곳](https://sourceforge.net/projects/lenovo-y700/files/TB9707F/) [terajima-alc](https://terajima-alc.dev/)님께 감사의 말 전합니다.

---
<br>

## ⚡ 비공식 ZUI 15 OTA 사이드로딩하기 (ZUI 15 Android 13): <a name=unofficial-ota></a>
[이 동영상(영문)에서 설치 과정을 확인할 수 있습니다.](https://www.youtube.com/watch?v=ZN-D9tlXCTM)

* 다음 조건이 선행되어야 합니다:  
  * [공식 소스에서 ADB 다운로드](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
  * 중국 순정 내수롬이 이미 설치되어있어야 합니다. 아직 설치하지 않았다면, 다음 링크를 참조하십시오: ⚡ [공식 중국 내수롬 설치 방법](#stock-rom)
  * OTA 압축파일 (영상 설명란에도 링크가 기재되어 있습니다.):
    * [링크 1 - MEGA](https://mega.nz/file/lOUxnIYT#EzAg7reYfJ8oy_82OzCtQFi8XbMdhb_2YYjvVIf1P90)
    * [링크 2 - 공식 레노버 페이지](https://mobile-ota-cdn.lenovo.com/firmware/2023111110434825-3726.zip&v=ZN-D9tlXCTM)
    * OTA 압축 파일은 PC에 저장하십시오.

### 명령어: 
1. 태블릿을 PC에 연결하고, PC가 기기를 인식하는지 다음 명령어로 확인합니다.: 
```
adb devices
```
2. 다음 명령어를 사용하여 태블릿을 리커버리 모드로 재부팅합니다.
```
adb reboot recovery
```
3. 리커버리 모드에서 볼륨 버튼을 이용하여 "Apply update from ADB"로 이동하고 전원 버튼을 눌러 선택합니다.
   
4. PC에서 OTA 사이드로딩을 시작하는 명령어를 다음과 같이 입력합니다. OTA_FILENAME.zip에는 본인이 다운로드한 파일명을 입력하십시오.
```
adb sideload OTA_FILENAME.zip
```
5. 작업이 완료되면 리커버리 모드에서 "Reboot system now" 를 선택합니다. 그러면 기기가 자동으로 새로운 버전의 ZUI/안드로이드로 재부팅합니다.

---
<br>

## ℹ️ Y700 1세대(2022)에서 정상 작동이 확인된 GSI(커스텀 롬) 목록: <a name=info></a>
* 역자 주: 엄밀히 말하면 GSI와 커스텀 롬은 의미가 다릅니다만, 여기서 사용하는 GSI 이미지 자체가 커스텀 롬 이미지이므로 여기서는 편의상 구분 없이 서술합니다.
[이 링크에서](https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-%28GSI%29-list) GSI 롬 목록을 확인할 수 있습니다. **안드로이드 11 혹은 그 이상 버전의 GSI 롬을 사용하십시오.** 다음은 커뮤니티에서 정상 작동이 확인된 GSI 롬 목록입니다. 여기에 없는 롬도 정상 작동할 수 있으니, 설치 후 정상 작동이 확인되면 알려주시기 바랍니다.

현재 테스트된 롬과 버그에 대해서 확인하려면, 각 롬의 이름을 클릭하여 확인하십시오.
* [CRDROID](/roms/crdroid-kr.md)
* [EvolutionX](/roms/evolution-kr.md)
* [Voltage OS](/roms/voltageos-kr.md)
* [Google AOSP](/roms/google_aosp-kr.md)
* [LeOS U](/roms/leosu-kr.md)
* [Elixir Project](/roms/elixir-kr.md)


--- 
<br>

## ℹ️ GSI 버그 픽스: <a name=gsifix></a>
GSI 롬 사용 시 발생할 수 있는 문제와 해결 방법에 대해 서술합니다.
본 단락은 현재 최종본이 아닙니다. 기타 버그 및 그 해결법을 아는 경우 연락해 주십시오.

### 오디오 단자 (3.5mm) 가 작동하지 않음
<br>
설정 앱->Phh Treble Settings->Qualcomm features->`Use alternate audio policy` 을 활성화합니다.
<br>
설정 앱->Phh Treble Settings->Misc features->`Use alternate way to detect headsets`을 활성화합니다.
<br>
두 설정 모두 활성화한 다음 재부팅하십시오.

### 측면 스위치 활용하기 / 자동 밝기 문제 해결 / 얼굴 인식 잠금 해제 문제 해결
<br>

[이 모듈을 설치하십시오.](https://github.com/reindex-ot/LegionY700-GSI-Fix_MOD). Magisk가 설치되어 있어야 합니다.

### 두 번 눌러 깨우기(DT2W) 활성화
[여기(영문)](https://xdaforums.com/t/magisk-module-enable-dt2w-for-gsi-rom-zui14-base.4633371/)로 이동하여 Y700-DT2W-Enabler.zip 파일을 다운로드한 다음 Magisk를 통해 설치하십시오. Magisk가 설치되어 있어야 작동합니다.

---
<br>

## ⚡ GSI 롬 설치: <a name=flash-gsi></a>

> [!TIP]  
> [여기를 눌러 설치 과정이 담긴 동영상을 확인할 수 있습니다.(영문)](https://www.youtube.com/watch?v=zQ0Guo1v9LA). 설치 전 시청을 권장드립니다.

* 선행 사항:  
  * [공식 소스에서 ADB 다운로드](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
  * 순정롬의 vbmeta.img 파일 ([이 영상의 설명란에 있습니다.](https://www.youtube.com/watch?v=VaCjtUDoqXA&t=0s))
  * GSI 롬 이미지 파일. 여기에서는 예시로 [CRDROID](/roms/crdroid-kr.md) 롬을 사용합니다.


### 명령어: 
1. 태블릿을 PC에 연결하고, PC가 기기를 인식하는지 다음 명령어로 확인합니다.: 
```
adb devices
```

2. 다음 명령어를 사용해 부트로더로 재부팅합니다.
```
adb reboot bootloader
```

3. PC에서 태블릿이 **부트로더 모드에 진입한 것을** 인식하는지 다음 명령어를 입력하여 확인합니다:
```
fastboot devices
```
> [!IMPORTANT]  
> fastboot 모드에서 기기가 인식되지 않는 경우 (위 명령어를 입력했을 때 기기가 표시되지 않는 경우): [여기를 참고하여 부트로더 인터페이스 드라이버를 설치하십시오.(영문)](https://droidwin.com/install-google-android-bootloader-interface-drivers/)

4. vbmeta.img 파일을 다음 명령어를 사용하여 플래싱합니다. (파일은 순정 롬 또는 [여기에서(영문)](https://xdaforums.com/t/how-to-install-gsi-with-google-services-on-legion-y700-netflix-problem-solved-games-payment-issue-solved.4651090/) 얻을 수 있습니다.)
```
fastboot --disable-verification flash vbmeta vbmeta.img
```

5. fastboot 모드로 재부팅합니다.
```
fastboot reboot fastboot
```
그런 다음 볼륨키를 사용해 "Enter Fastboot"를 선택한 다음 전원키를 눌러 fastboot모드로 재부팅합니다.

6. user space를 사용중인지 다음 명령어로 확인합니다.
```
fastboot getvar is-userspace
```
is-userspace:yes 가 출력되면 계속 진행하십시오.

7. 기존 시스템을 다음 명령어를 입력하여 지웁니다.
```
fastboot erase system
```

8. 논리 파티션 B를 다음 명령어를 사용하여 삭제합니다.
```
fastboot delete-logical-partition product_b
```

9. GSI 롬을 다음 명령어를 이용하여 사용합니다. 여기에서는 예시로 [CRDROID](/roms/crdroid-kr.md) 롬을 사용합니다. system 뒤 파일명은 설치하려는 롬의 파일명으로 바꾸어 입력하십시오.
```
fastboot flash system crDroid-10.0-arm64_bgN-Unofficial.img
```

10. 다음 명령어를 사용하여 리커버리 모드로 재부팅합니다.
```
fastboot reboot recovery
```

11. "Wipe Data / Factory Reset"를 선택하고 확인합니다.
12. "Reboot System now"를 선택하여 재부팅합니다.
13. 이제 기기가 GSI 롬으로 정상적으로 부팅될 것입니다.

--- 
<br>

## 🦄 Magisk 설치 (태블릿 루팅): <a name=magisk></a>

### 복잡한 방법: 
직접 boot.img를 패치합니다. 방법은 [이 포스트(영문)](https://xdaforums.com/t/gsi-rom-install-magisk-with-no-root-on-gsi-rom-dsu-method.4651428/)에 서술되어 있습니다.

### 쉬운 방법: 
[동영상 가이드(영문)](https://www.youtube.com/watch?v=eVR1i7yASXA)

* [여기를 눌러](https://drive.google.com/drive/folders/1E5BsgLwW4Yc_2-ajOklnAVocDODDGs2M) Magisk 패치된 boot.img를 다운로드합니다.
* 이 이후는 다음 지시를 따르십시오.

#### 쉬운 방법용 명령어: 
1. 기기가 ADB에서 감지되었는지 다음 명령어로 확인합니다.
```
adb devices
```
2.Magisk apk를 설치합니다. (다음 명령어를 사용하거나, 기기에서 직접 다운로드 및 설치하여도 됩니다.)
```
adb install Magisk.apk
```
3. 부트로더로 재부팅합니다.
```
adb reboot bootloader
```
4. 기기가 fastboot 모드에서 감지되었는지 확인합니다.
```
fastboot devices
```
5. 패치된 boot.img를 설치합니다.
```
fastboot flash boot magiskPatchedBootB.img
```
6. "Restart recovery"를 선택하여 리커버리로 재부팅합니다. (볼륨 버튼으로 이동, 전원키로 확인)
7. 기기가 리커버리 모드로 재부팅되면 "Restar system now"를 눌러 재부팅합니다.
8. Magisk앱을 열고, 추가적 패치가 필요하다는 팝업이 뜨면 확인을 누릅니다. 기기가 자동으로 재부팅됩니다.
9. 기기가 재부팅되면 Magisk 앱을 열고 다음 사진과 같이 정상적으로 설치되었는지 확인합니다.
![](/images/magisk/magisk.png)

---  
<br>

## 🚀 참조 목록 <a name=acknowledgements></a>
vicenteMartinezY700 [XDA 포스팅](https://xdaforums.com/t/how-to-install-gsi-with-google-services-on-legion-y700-netflix-problem-solved-games-payment-issue-solved.4651090/) - GSI 롬 및 기기 테스팅 <br>
LinuxDroidMaster - [본 포스트의 원 저자입니다.](https://github.com/LinuxDroidMaster/Lenovo-Legion-Y700-ROMs)
[reindex-ot](https://note.com/reindex/m/m7b23ab35e0e3) - Y700 1세대 관련 유용한 정보가 있는 일본 사이트입니다. 
[reindex-ot](https://reindex-ot.github.io/) - 위 링크와 동일인이 운영하는 다른 사이트입니다. 아래로 내리면 순정롬 다운로드 링크를 확인할 수 있습니다.
---  
