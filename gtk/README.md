# Self-Learning - GTK



### Compile 시 주의사항

include path와 link path를 하나 하나 기록하는 것은 너무 불편함으로 다음과 같이 pkg-config를 통해 Path를 가져온다. 우선 아래와 같이 shell에서 실행하여 include path와 link path가 표현되는지 확인한다.

```shell
`pkg-config --cflags --libs gtk4`
```

정상적으로 잘 되면 아래와 같이 컴파일 할 수 있다.

```shell
clang -Wall -g gtktest.c -o hello `pkg-config --cflags --libs gtk4`
```



Test 를 위한 Source File은 https://www.gtk.org/ 메인 화면의 C source를 그대로 컴파일 해 보는 것이 좋다.
