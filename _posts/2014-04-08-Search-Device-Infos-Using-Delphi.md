---
layout: post
title:  "delphi로 시스템에 연결된 장치 정보 확인하기"
date:   2014-04-08 10:11:00
categories: delphi
---
# Delphi로 장치정보를 조회하기

## 장치 정보를 조회하기

시스템의 장치 정보를 조회하는 방식은

- WQL질의
- Registory 죄회
- Windows API 활용

같은 방식이 있습니다.

## WQL 질의

WQL은 API의 접근대신에 시스템 정보를 추상화 시켜 놓은 아이입니다.

때문에, API를 몰라도 되며, API의 변화에 대응할 필요도 없습니다.

컨셉이 일관된 인터페이스제공(OS 버전따위는 상관없는)이기에 개발자에게는 매우 바람직한 아이라고 할 수 있습니다.

- 시스템의 정보를 가져올 수도 있으며, Event를 등록하면 Event를 받아 올 수도 있습니다. >_<
 - 단순하게는 Windows PowerShell 에서 확인할 수 있습니다.
 - http://msdn.microsoft.com/en-us/library/dd835506(v=vs.85).aspx
 - 질의`Select * from Win32_SerialPort`가 수행되면 PC에서 연결된 정보를 추려 옵니다.
- 개발자는 테스트를 수행하고 질의를 가다듬어 대응 코드를 작성를 작성하면됩니다.

### WMI Delphi Code Generator

[WMI Delphi Code Generator](http://theroadtodelphi.wordpress.com/wmi-delphi-code-creator/) 
*~~URL 멋집니다. ㅠ_ㅠ. theroadtodelphi, The Road To Delphi~~*

WQL을 사용하신다면 꼭 사용하세요. 두번 사용하세요.

Delphi, PurePascal, C#, MS C++ 코드가 이쁘게 줄맞춰 생성됩니다.

생성된 코드를 사용하시면 됩니다.

## registry 조회

- Comport: HKEY_LOCAL_MACHINE\HARDWARE\DEVICEMAP\SERIALCOMM
- Bluetooth: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\
  - 아래에 Btxxx 로 정의되는 아이들.
  - 외에도 여러 곳에 나열되어 있을겁니다.

해당 레지스트리를 조회하여 원하는 정보를 취합할 수 있습니다.

```delphi
unit mComportList;

interface

uses
  Classes, SysUtils, Windows, System.Generics.Collections;

type
  TComPortList = class(TStringList)
  private
  public
    procedure Search;
  end;

implementation

{ TComPortList }

procedure TComPortList.Search;
const
  RegPath = 'HARDWARE\DEVICEMAP\SerialComm';
var
  Reg: TRegistry;
  SL: TStringList;
  i: Integer;
begin
  Reg := TRegistry.Create(KEY_READ);
  SL := TStringList.Create;
  try
    Reg.RootKey := HKEY_LOCAL_MACHINE;
    if not Reg.KeyExists(RegPath) then Exit;
    if not Reg.OpenKey(RegPath, False) then
      raise Exception.Create('TSerialComDeviceList.find_SerialComDevice: RegKey OpenFailed ');

    Reg.GetValueNames(SL);
    for i := 0 to SL.Count - 1 do
      Values[Reg.ReadString(SL[i])] := SL[i];
    Reg.CloseKey;
  finally
    FreeAndNil(SL);
    FreeAndNil(Reg);
  end;
end;

end.
```


## Windows API (SetupDixxx) 사용

MSDN: http://msdn.microsoft.com/en-us/library/windows/hardware/ff551010(v=vs.85).aspx

- 링크와 같이 무수하게 많은 API가 있습니다.
- 일일이 Input, Output 파라미터, 각각의 구조체를 알아야지만 작성가능합니다. 손품을 팔아야 결과를 얻을 수 있습니다.

Comport와 USB의 연결정보는 아래의 예에서 찾을 수 있습니다.

- Source: https://github.com/gomsun2/gs2lib/tree/master/source/device.win
- Sample: https://github.com/gomsun2/gs2lib/tree/master/moduletest/mDvcObserver.WM_DEVICECHANGE





