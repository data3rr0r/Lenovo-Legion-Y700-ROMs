# 레노버 Y700 2세대 (TB320FC) 커스텀롬/순정롬 복원 가이드

Y700 2세대 (TB320FC) 태블릿에 관한 커스텀롬/순정롬 정보를 다루는 레포입니다.

### 🚧 현재 작업중 🚧

> [!WARNING]
> 본 가이드를 따라하여 생기는 모든 문제는 사용자 본인에게 있습니다. 본 가이드에서 설명하는 과정은 기기를 벽돌 상태로 만들 수 있습니다. [이 영상](https://www.youtube.com/watch?v=VaCjtUDoqXA)을 참고용으로 사용할 수 있습니다만(동영상은 1세대 모델을 기준으로 하고 있습니다.), 기기에 생기는 문제에 대해서는 책임지지 않습니다.

</br>

# 📚 목차

- ⚡ [일본 NEC롬 플래싱](#global-rom)
- 🚀 [참조 목록](#acknowledgements)

<br>
<br>

## ⚡ 일본 NEC 글로벌 롬 플래싱 (ZUI 15 Android 13): <a name=global-rom></a>

설치 과정은 [이 동영상(영문)](https://www.youtube.com/watch?v=VaCjtUDoqXA)이나 [이 XDA 포스트(영문)](https://xdaforums.com/t/guide-unbrick-lenovo-y700-tablet.4509297/)을 참조하십시오.

링크:

- [공식 소스에서 ADB 다운로드](https://developer.android.com/studio/releases/platform-tools?hl=es-419)
- [QFIL - 다운로드 링크](https://qpsttool.com/qpst-tool-v2-7-496)
- [모토롤라 USB 드라이버](https://en-us.support.motorola.com/app/answers/detail/a_id/88481/)
- [퀄컴 9008 드라이버](https://androiddatahost.com/nbyn6)
- [NEC 글로벌롬 링크](https://mirrors.lolinet.com/firmware/nec/NEC_Lavie_Tab_9QHD1/)
- [NEC 글로벌롬 커뮤니티 포스트(XDA)](https://xdaforums.com/t/y700-2023-nec-lavie-tab-9qhd1.4642255/)

> [!TIP]
> 상기한 모든 툴을 다운로드받고 작업하기를 권장드립니다.

### 명령어:

#### 부트로더 언락

1. 설정 -> 태블릿 정보 -> 버전을 여러번 탭하여 개발자 설정을 활성화합니다.
2. 설정 앱으로 되돌아온 다음, 개발자 설정으로 진입합니다.
3. USB 디버깅을 켭니다.
4. OEM 잠금 해제를 켭니다.
5. [모토롤라 드라이버](https://en-us.support.motorola.com/app/answers/detail/a_id/88481/)를 설치합니다.
6. [setup-tools](https://developer.android.com/studio/releases/platform-tools?hl=es-419)를 다운로드한 다음 압축을 풀고 복사합니다.
7. fastboot 모드로 진입합니다.
   - 볼륨 상 버튼을 홀드한 상태에서 fastboot 화면이 나타날 때까지 전원버튼을 누릅니다.
8. 긴 쪽 USB 포트에 케이블을 연결합니다.
9. cmd창을 엽니다.
10. 다음 명령어를 실행하십시오.
```
fastboot devices
```
11. 기기가 인식된 것을 확인하고, 다음 단계로 진행합니다.
12. 다음 명령어를 입력합니다.
```
fastboot oem unlock-go
```
13. 공장 초기화가 진행되며 부트로더가 언락되고, 기기는 자동으로 재부팅됩니다.

#### 롬 설치

1. [QFIL](https://qpsttool.com/qpst-tool-v2-7-496)을 설치합니다.
2. [NEC 글로벌롬](https://mirrors.lolinet.com/firmware/nec/NEC_Lavie_Tab_9QHD1/)을 다운로드한 다음, 압축파일의 내용물은 QFIL.exe가 위치한 `bin`폴더에 복사합니다.
3. QFIL을 열고 파일 시스템을 `UFS`로 설정합니다.
4. QFIL에서 `contents.xml`을 로드합니다.
5. Programmer file 칸에 `xbl_s_devprg_ns.melf`이 자동으로 선택됩니다. 이대로 두십시오.
6. [퀄컴 9008 드라이버](https://androiddatahost.com/nbyn6)를 설치합니다.
7. EDL 모드에 진입합니다.
   1. fastboot 모드로 진입합니다.
      - 볼륨 상 버튼을 홀드한 상태에서 fastboot 화면이 나타날 때까지 전원버튼을 누릅니다.
   2. 볼륨 하 버튼을 이용하여 Shutdown을 선택합니다.
   3. 기기가 진동하면 볼륨 상 버튼을 기기 화면이 검은색으로 될 때까지 누르고 있습니다.
8. 긴 쪽의 USB 포트에 케이블을 연결합니다.
9. 해당 포트가 QFIL에 자동으로 인식됩니다. 인식되지 않은 경우 수동으로 선택하여 지정합니다. 그래도 나타나지 않는 경우 EDL 모드 재진입을 시도합니다.
10. 모든 것이 제대로 나타났는지 다시 한 번 확인하십시오. **잘못 사용하는 경우 기기를 하드 브릭 상태로 만들 수 있습니다.**
11. "Download Content"를 누릅니다.
12. 하단 로그에서 `download complete` 메시지가 나올 때까지 기다립니다.
13. 완료되면 기기를 재부팅하면 됩니다.

> [!IMPORTANT]
> EDL 모드 진입부터 "Download Content" 클릭까지 너무 오랜 시간이 소요된 경우, Sahara error 메시지가 나오며 플래싱이 실패할 수 있습니다.

<br>
<br>

## ℹ️ Y700 2세대에서 작동하는 GSI 롬: <a name=info></a>
현재 확인된 정보가 없습니다. 직접 테스트해보고 결과를 보내주시면 반영하겠습니다.



## 🚀 참고 사항 <a name=acknowledgements></a>

blueberryapple - Y700 2023 정보 추가에 도움을 주셨습니다.
LinuxDroidMaster - 본 포스트의 원 저자입니다.
