# [Nginx Server Configs](https://github.com/h5bp/server-configs-nginx)

[![Test](https://github.com/h5bp/server-configs-nginx/workflows/server/badge.svg)](https://github.com/h5bp/server-configs-nginx/actions?query=workflow%3Aserver)

**Nginx Server Configs** is 도움이 될 수 있는 구성 파일 모음
서버는 웹사이트의 성능과 보안을 개선하는 동시에 리소스가 올바른 콘텐츠 유형으로 제공되고 필요한 경우 도메인 간에도 액세스할 수 있도록 보장합니다.


## Getting Started

Nginx 서버 구성 리포지토리를 직접 사용하려면 몇 가지 필수 단계가 있습니다.

* [Nginx Beginners Guide](https://nginx.org/en/docs/beginners_guide.html)
* [Nginx Request Processing](https://nginx.org/en/docs/http/request_processing.html)


### Check `nginx.conf` settings

가장 먼저 확인해야 할 것은 `nginx.conf` 파일에 특정 설치에 적합한 값이 포함되어 있는지 확인하는 것입니다.

가장 구체적인 변수는 다음과 같습니다:

* `user`
* `error_log`
* `pid`
* `access_log`

### Nginx 테스트 및 재시작

* Nginx 현재구성 검증:

  ```shell
  nginx -t
  ```

* 사용자 정의 파일로 Nginx 구성 검증:

  ```shell
  nginx -t -c nginx.conf
  ```

* Nginx 리로드 및 새구성 적용:

  ```shell
  nginx -s reload
  ```

### 저장소 구조

이 리포지토리의 구조는 다음과 같습니다:

```text
./
├── conf.d/
│   ├── default.conf
│   └── templates/
├── h5bp/
│   ├── basic.conf
│   ├── location/
│   └── .../
├── custom.d/
│   └── .../
├── mime.types
└── nginx.conf
```

* **`conf.d/`**

  이 디렉터리에는 모든 `server` 정의가 포함되어야 합니다.

  점 앞에 접두사가 붙거나 확장자가 '.conf'가 아닌 경우를 제외하고 이 디렉터리에 있는 모든 파일은 자동으로 로드됩니다.

  * **`templates` folder**

    이 디렉터리의 파일에는 보안 및 비보안 호스트를 위한 `server` 템플릿이 포함되어 있습니다. 이 파일은 모든 `example.com`이 대상 호스트로 변경된 상태로 `conf.d` 디렉터리에 복사되어야 합니다.

* **`h5bp/`**

  이 디렉토리에는 원하는 대로 포함할 수 있는 스니펫(mixins)이 포함되어 있습니다.

  제공되는 config 파일에는 개별 config 스니펫과 편리한 기본값을 제공하는 결합 config 파일의 두 가지 유형이 있습니다.

  * **`basic.conf`**

    이 파일은 이 저장소에서 제공하는 규칙의 일부 하위 집합을 로드하여 'expires' 헤더를 추가하고, cross-domain 글꼴을 허용하며, 웹 액세스로부터 시스템 파일을 보호합니다. 액세스합니다. `basic.conf` 파일에는 항상 정의하는 것이 권장되는 규칙이 포함되어 있습니다.

  * **`location/`**

    이 디렉토리에 있는 파일은 하나 이상의 `location` 지시어를 포함합니다. 이러한 파일은 `server` 컨텍스트(또는 중첩된 `location` 블록)에서 로드되도록 되어 있습니다.

* **`custom.d/`**

  이 디렉터리에는 모든 사용자 정의 `nginx.conf` 구성이 포함되어야 합니다.

  점 앞에 접두사가 붙거나 확장자가 `.conf`가 아닌 경우를 제외하고 이 폴더의 모든 파일은 자동으로 로드됩니다.

* **`mime.types`**

  `mime.types` 파일은 파일 확장자를 MIME 유형에 매핑하는 역할을 합니다.

* **`nginx.conf`**

  기본 Nginx 구성 파일입니다.


## 사용법

### As a reference

reference 로 사용하려면 특별한 설치단계 없이 편리한 위치에 리포지토리를  download/checkout 하고, 이 리포지토리에서 원하는 기능을 통합하여 기존 Nginx 구성을 조정하면 됩니다.

Download the [latest release archive](https://github.com/h5bp/server-configs-nginx/releases/latest).

### Directly

직접 사용하려면 Nginx config 디렉터리를 이 리포지토리로 바꾸세요.
예를 들어:

```shell
nginx -s stop
cd /etc
mv nginx nginx-previous
git clone https://github.com/h5bp/server-configs-nginx.git nginx
# install-specific edits
nginx
```

### 사이트 관리

```bash
cd /etc/nginx/conf.d
```

* 사이트 생성

  ```bash
  cp templates/example.com.conf .actual-hostname.conf
  sed -i 's/example.com/actual-hostname/g' .actual-hostname.conf
  ```

* 사이트 활성화

  ```bash
  mv .actual-hostname.conf actual-hostname.conf
  ```

* 사이트 비활성화

  ```bash
  mv actual-hostname.conf .actual-hostname.conf
  ```

```bash
nginx -s reload
```


## Support

 * Nginx v**1.8.0**+


## Contributing

Anyone is welcome to [contribute](.github/CONTRIBUTING.md),
however, if you decide to get involved, please take a moment to review
the [guidelines](.github/CONTRIBUTING.md):

* [Bug reports](.github/CONTRIBUTING.md#bugs)
* [Feature requests](.github/CONTRIBUTING.md#features)
* [Pull requests](.github/CONTRIBUTING.md#pull-requests)


## Acknowledgements

[Nginx Server Configs](https://github.com/h5bp/server-configs-nginx) is
only possible thanks to all the awesome
[contributors](https://github.com/h5bp/server-configs-nginx/graphs/contributors)!


## License

The code is available under the [MIT license](LICENSE.txt).
