# Guide Android Development

1. Скачать шаблон приложения можно здесь:
[Kotlin Multiplatform](https://www.jetbrains.com/help/kotlin-multiplatform-dev/get-started.html)…

2. Донастройка проекта в Termux:

- [ ] Sdk and Ndk

- [ ] Нюанс

```json
android {
  buildToolsVersion = "36.1.0"
    compileSdk {
      version = release(36) {
        minorApiLevel = 1
      }
    }
}
```

- [ ] env

```bash
export JAVA_HOME="$PREFIX/lib/jvm/java-21-openjdk"
export ANDROID_HOME="$HOME/Android"


for dir in "$ANDROID_HOME/cmdline-tools/latest/bin" \
           "$ANDROID_HOME/platform-tools" \
           "$ANDROID_HOME/build-tools/36.1.0"; do
    case ":${PATH}:" in
        *:"$dir":*) ;;
        *) export PATH="$dir:$PATH" ;;
    esac
done
```

- [ ] ...
- [ ] ...
- [ ] ...

