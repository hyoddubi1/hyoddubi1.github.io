---
layout: post
title: Docker에서 dtderr linux용 windows 하위 시스템 설치되어 있지 않습니다. 에러
subtitle: WSL, 도커, 우분투 에러
categories: misc
tags: [Docker, Windows subsystem Linux (WSL)]
---

### 어느날부터

컴퓨터를 부팅하면 Docker desktop에서 오류 메시지가 뜨더라.

오류 메시지 내용은

```
dtderr: linux용 windows 하위 시스템 설치되어 있지 않습니다.
```
블라블라블라..

사실 이것보다는 윈도우즈 PowerShell 프롬프트로 작업할 때가 더 문제였다.

파워쉘 키면

```
. : 이 시스템에서 스크립트를 실행할 수 없으므로 C:\Users\user\Documents\WindowsPowerShell\profile.ps1 파일을 로드할 수 없습니다. 자세한 내용은 about_Execution_Policies(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하십시오.
```

이러면서 WSL 자체가 먹통이 돼 있는 것이었다.

나는 얼마전까지 Docker랑 WSL 다 잘 쓰고 있었다. 

WSL이 설치가 안 돼있을리는 만무.

그래서 Windows 스토어에서도 Ubuntu가 정상적으로 잘 설치되어 있다고 되어 있었다.

그래서 여기서 Ubuntu를 키니까

```
AppData\Local\Docker\wsl\distro: exit code: 1
```
라는 오류가 또 뜬다.


그래서 나랑 관련된 모든 해결책들을 다 시도해 보았다.

## 1 권한 주기(설치도?)

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart  
```
위 세 개는 아무 문제 없이 됐는데
```
wsl --set-default-version 2
```
로 하면 wsl이 없다고 다시 오류가 뜬다

## 2 Windows 기능에서 윈도우즈 서브시스템 체크하기

"Windows 기능"이라는 앱을 키면

Windows 기능 켜기/끄기가 있다.

근데 난 원래 쓰던 사람이었으니 당연히 미리 체크가 돼있었지.

그래서 체크 풀고 확인하고 다시 체크를 키고 확인하고 재부팅했다.

## 3 도커 끄고 다시 하기(매우굿)

열심히 찾아보니까 스택오버플로우에 링크가 있었다.

[Stackoverflow Link](https://stackoverflow.com/questions/66074090/system-invalidoperationexception-failed-to-deploy-distro-docker-desktop-to-loc)

그 중 Greenfly77의 의견을 반영했다.

왜? 다른건 막 다 WSL 지우고 도커 지우고 그러라는데 나는 그러고 싶지 않았다.

답변에 의하면 도커에서는 WSL이 없노라고 뜬다만 이 문제는 WSL 문제가 아니라 Docker의 문제라는 것.

도커랑 윈도우즈 업데이트가 될 때 이런일이 있는데, 그러면 WSL을 재설치하면서 막 죽여버린단다.

그래서 이 사람이 주는 해답은 설정(구 제어판)의 시작프로그램에서 Docker를 없애고 (도커를 지우는게아니라 시작때 키지만 말라 이말)
윈도우를 키면 WSL이 된단다.

그래서 재시작했는데

여전히 WSL 오류가 있어서

이 때 메시지에 "wsl.exe --install"하십쇼 라고 돼있어서

속는 셈 치고 했다.

그랬더니 우분투랑 wsl을 다시 까는 액션을 하더라.

그리고 설치 후 재부팅해서 파워쉘 가니

**wsl이 작동이 잘 됐다!!**

WSL 작동 확인 하고 도커실행하니

WSL과 도커 모두 작동이 됐다.