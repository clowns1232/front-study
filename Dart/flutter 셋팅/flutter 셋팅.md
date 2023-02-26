# flutter 셋팅

# MAC(애플 실리콘)에서 설치하기

1. Flutter을 [다운](https://docs.flutter.dev/get-started/install/macos)받습니다.
2. `unzip ~/Downloads/flutter_macos_arm64_3.7.5-stable.zip` 
3.  저는 zshrc를 사용하기 때문에 `vim ~/.zshrc`  으로 들어가서`export PATH**=**"$PATH:`pwd`/flutter/bin"` 을 추가해줍니다.
    1. 이후 적용할려면 `source ~/.zshrc` 나 터미널을 껐다 켜줍니다.
4. 이 후 iterm에서 `flutter doctor` 명령어로 flutter을 설치가능한지 확인해봅시다.
    1. 저는 실리콘 맥으로 아래와 같은 에러가 떴습니다.
    2. [✗] Android toolchain - develop for Android devices
    3. [✗] Xcode - develop for iOS and macOS
5. flutter doctor에서 나온 이슈를 처리합니다.
6. 안드로이드 스튜디오에서 flutter 플러그인 다운
7. 그다음 flutter 프로젝트를 만들고 실행하면 아래와 같은 폴더가 구성됩니다.

![Untitled](./flutter%20%EC%85%8B%ED%8C%85/Untitled.png)

이 후 폴더에 대한 구성을 알아보겠습니다.