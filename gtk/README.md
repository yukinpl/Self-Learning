# Self-Learning - GTK



### Ubuntu 에서 개발 환경 설치는

gtk4의 경우 

```shell
sudo apt-get install libgtk-*
```

gtkmm의 경우

```shell
sudo apt-get install libgtkmm-*
```





### Compile 참고사항

include path와 link path를 하나 하나 기록하는 것은 너무 불편함으로 다음과 같이 pkg-config를 통해 Path를 가져온다. 우선 아래와 같이 shell에서 실행하여 include path와 link path가 표현되는지 확인한다.

```shell
`pkg-config --cflags --libs gtk4`
```

정상적으로 잘 되면 아래와 같이 컴파일 할 수 있다.

```shell
clang -Wall -g gtktest.c -o hello `pkg-config --cflags --libs gtk4`
```



Test 를 위한 Source File은 https://www.gtk.org/ 메인 화면의 C source를 그대로 컴파일 해 보는 것이 좋다.





### Gtkmm

Gtk는 C로 되어 있으니 C/C++로 사용하기에 문제 없으나 C++로 개발하기 편하도록 Gtkmm이 별도로 존재한다. Gtk를 Wrapping 하였다고 한다. Gtk와 동일하게 아래와 같이 점검할 수 있다.

```shell
`pkg-config --cflags --libs gtkmm-3.0`
```
정상적으로 잘 되면 아래와 같이 컴파일 할 수 있다.
```shell
clang++ -Wall -g *.cpp -o hello `pkg-config --cflags --libs gtkmm-3.0` -std=c++17
```
Ubuntu 22.04에는 gtkmm Ver 3.x 가 기본으로 준비되어 있다. Ver 4.x는 직접 설치해야한다.
