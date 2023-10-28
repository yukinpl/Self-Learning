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

  

  


### Gtk4 - Compile 참고사항

include path와 link path를 하나 하나 기록하는 것은 너무 불편함으로 다음과 같이 pkg-config를 통해 Path를 가져온다. 우선 아래와 같이 shell에서 실행하여 include path와 link path가 표현되는지 확인한다.

```shell
`pkg-config --cflags --libs gtk4`
```

정상적으로 잘 되면 아래와 같이 컴파일 할 수 있다.

```shell
clang -Wall -g gtktest.c -o hello `pkg-config --cflags --libs gtk4`
```

  

Test 를 위한 Source File은 https://www.gtk.org/ 메인 화면의 C source를 그대로 컴파일 해 보는 것이 좋다.

  

  


### Gtkmm - Compile 참고사항

Gtk는 C로 되어 있으니 C/C++로 사용하기에 문제 없으나 C++로 개발하기 편하도록 Gtkmm이 별도로 존재한다. Gtk를 Wrapping 하였다고 한다. Gtk와 동일하게 아래와 같이 점검할 수 있다.

```shell
`pkg-config --cflags --libs gtkmm-3.0`
```
정상적으로 잘 되면 아래와 같이 컴파일 할 수 있다.
```shell
clang++ -Wall -g *.cpp -o hello `pkg-config --cflags --libs gtkmm-3.0` -std=c++17
```
Ubuntu 22.04에는 gtkmm Ver 3.x 가 기본으로 준비되어 있다. Ver 4.x는 직접 설치해야한다.
아래 내용을 참고하여 Ver 4.x을 설치했다면 gtkmm-3.0 부분을 gtkmm-4.0으로 바꿔 컴파일하면 된다.

  


### Gtkmm - ver 4.x 설치

Ubuntu 22.04 에는 gtkmm Ver 3.x 가 기본으로 준비되어 있어서 Ver 4.x는 Repo를 통한 바이너리 설치를 하는 것이 아니라 직접 컴파일 해서 설치해야 한다. 또한, dependency 도 대부분 Repo에 포함되어 있지 않으므로 관련 lib도 직접 컴파일 해서 설치할 필요가 있다.

  


##### docbook-xsl

아래 진행 과정중 파일 Parsing 문제로 컴파일 진행 중 오류가 발생하므로 우선 설치할 필요가 있다. 이는 간단히 **apt** ( **apt-get** )를/을 사용하여 설치하면 된다.

```shell
sudo apt-get install docbook-xsl
```

  


##### libsigc++-3.6.0

```shell
wget https://ftp.acc.umu.se/pub/GNOME/sources/libsigc++/3.6/libsigc++-3.6.0.tar.xz
tar Jxvf libsigc++-3.6.0.tar.xz
cd libsigc++-3.6.0/
./autogen.sh --prefix=/usr/local
sudo make install
```

prefix로 /usr/local이 아닌 /usr에 하는 경우 발생하지 않을 문제이나 /usr/local 로 지정하였으므로 dynamic lib 가 /usr/local/lib 아래 위치하게 되므로 symbolic link를 /usr/lib/ 에 만들어 두어야 프로그램이 실행될 때 문제 없이 실행될 수 있으므로 아래와 같이 Symbolic link를 생성한다.

```shell 
sudo ln -s /usr/local/lib/libsigc-3.0.so.0.0.0 /usr/lib/libsigc-3.0.so.0.0.0
sudo ln -s /usr/local/lib/libsigc-3.0.la /usr/lib/libsigc-3.0.la
sudo ln -s /usr/local/lib/libsigc-3.0.so /usr/lib/libsigc-3.0.so
sudo ln -s /usr/local/lib/libsigc-3.0.so.0 /usr/lib/libsigc-3.0.so.0
```

생성시 미리 파일 명을 확인 하는 것이 좋다.

  

  


##### glibmm
```shell
wget https://download.gnome.org/sources/glibmm/2.68/glibmm-2.68.2.tar.xz
tar Jxvf glibmm-2.68.2.tar.xz
cd glibmm-2.68.2/
./autogen.sh --prefix=/usr
make
sudo make install
```

  


##### cairomm

cariomm이 이전에는 github에 repo가 있었으나 현재는 freedesktop의 gitlab에 존재한다.
```shell
git clone https://gitlab.freedesktop.org/cairo/cairomm
cd cairomm
./autogen.sh --prefix=/usr
make
sudo make install
```

  


##### pangomm

```shell
wget https://download.gnome.org/sources/pangomm/2.50/pangomm-2.50.0.tar.xz
tar Jxvf pangomm-2.50.0.tar.xz
cd pangomm-2.50.o/
./autogen.sh --prefix=/usr
make
sudo make install
```

  


##### gtkmm

```shell
wget https://download.gnome.org/sources/gtkmm/4.6/gtkmm-4.6.1.tar.xz
tar Jxvf gtkmm-4.6.1.tar.xz
cd gtkmm-4.6.1
./autogen.sh --prefix=/usr
make
sudo make install
```



