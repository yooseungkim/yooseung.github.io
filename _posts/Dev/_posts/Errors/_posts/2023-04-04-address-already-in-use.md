---
layout: post
title: Jekyll - Address already in use
tags: [Error]
hide_last_modified: true
permalink: "dev/error/address-already-in-use"
---

github 블로그 포스팅을 위해 local 호스팅을 하던 중 에러가 발생했다.

```sh
jekyll 3.9.3 | Error: Address already in use - bind(2) for 127.0.0.1:4000
```

대충 보아하니 이미 local에서 jekyll이 돌아가고 있는데 다시 실행해서 오류가 나는 듯했다. 그래서 다른 터미널에 켜진게 있나 찾아봤는데 아무리 찾아도 볼 수가 없었다.

아마 강제 종료를 시켜주면 해결될 문제 같아 구글링을 해봤다.

먼저 현재 돌아가고 있는 local 호스팅의 PID를 알아야한다. 이는 터미널에

```sh
lsof -wni tcp:<port no.>
```

를 입력하여 찾을 수 있다. 내가 사용하는 jekyll의 경우 로컬 주소가 127.0.0.1:4000인데, 이 때는 `<port no.>`에 `4000`을 입력해주면 된다.

그렇게 하면

```sh
COMMAND   PID        USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
ruby    24896 yooseungkim   12u  IPv4 0x1144c4ca0131ecbd      0t0  TCP 127.0.0.1:terabase (LISTEN)
```

이와 같은 결과가 나오는데, 이 때 `PID`가 우리가 찾고자 하는 것이다.

이제 PID를 알았으니 강제 종료를 시킬 일만 남았다. 이는

```sh
kill -9 <PID>
```

으로 강제 종료시킬 수 있다.

```sh
[1]    24896 killed     bundle exec jekyll serve
```

그러면 이렇게 강제로 killed 되었다는 메세지가 뜨며 종료되는 것을 확인할 수 있다.

다시 `bundle exec jekyll serve`를 통해 재실행하면 정상적으로 실행된다.
