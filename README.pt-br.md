# Configuração Minimalista do Android SDK

> 📘 Também disponível em [English](README.md)


> 📱 Setup minimalista do Android SDK e Emulador, sem depender do Android Studio.  
> 💡 Ideal para quem utiliza ambientes leves, automações, WSL, containers ou qualquer IDE (como VSCode, Neovim, JetBrains, Cursor) e não precisa do Android Studio completo apenas para executar o SDK.

---

## 📦 Baixando o SDK

Acesse: [Command-line tools only](https://developer.android.com/studio#command-line-tools-only)  
Extraia o conteúdo em uma pasta como `.android-sdk/cmdline-tools/latest`

```bash
.
└── .android-sdk
    └── cmdline-tools
        └── latest
            ├── bin
            └── lib
```

---

## ⚙️ Configuração das Variáveis de Ambiente

### Windows

```bat
REM Android
set ANDROID_HOME=%HOMEPATH%\.android-sdk
set PATH=%PATH%;%ANDROID_HOME%\cmdline-tools\latest\bin;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\emulator

REM Java
set JAVA_HOME=C:\tools\java\jdk\lts\jdk-21.0.2
set PATH=%PATH%;%JAVA_HOME%\bin
```

### Linux

```bash
# Android
export ANDROID_HOME=$HOME/.android-sdk
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin:$ANDROID_HOME/platform-tools:$ANDROID_HOME/emulator

# Java
export JAVA_HOME=$HOME/.jdk-21.0.2
export PATH=$PATH:$JAVA_HOME/bin
```

---

## 🔧 Instalando os Componentes

```bash
sdkmanager --update
sdkmanager "cmdline-tools;latest"
```

> ⚠️ Após o comando acima, pode ser criada uma pasta `latest-2`. Se isso ocorrer, remova a pasta anterior e renomeie a nova para `latest`.

Instale os demais componentes:

```bash
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "system-images;android-36;google_apis;x86_64"
sdkmanager "emulator"
```

---

## 📱 Criando e Executando um Emulador

Crie o AVD:

```bash
avdmanager create avd --name "DevPixel36" --device "pixel_6" --package "system-images;android-36;google_apis;x86_64" --sdcard 512M --force
```

Execute o emulador:

```bash
emulator -avd DevPixel36
```

Com opções úteis:

```bash
emulator -avd DevPixel36 -no-snapshot -memory 2048 -gpu auto
```

Execução em segundo plano (útil para CI/CD):

```bash
emulator -avd DevPixel36 -no-window -no-audio -no-boot-anim &
```

---

## 🛠️ Ajustes Visuais do Emulador

Caso ele inicie fora da tela ou em tamanho errado:

```bash
emulator -avd DevPixel36 -scale 0.75
```

Ou defina um tamanho de tela:

```bash
emulator -avd DevPixel36 -skin 720x1280
```

---

## ✍️ Autor

George Colber  
[george@colber.com.br](mailto:george@colber.com.br)

---

## 📘 Licença

Licença MIT — use, modifique e compartilhe à vontade!
