## Laboratory work IV

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Actions**

## Tasks

- [ ] 1. Авторизоваться на сервисе **Actions** с использованием **GitHub** аккаунта
- [ ] 2. Создать публичный репозиторий с названием **lab04** на сервисе **GitHub**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Включить интеграцию сервиса **Actions** с созданным репозиторием
- [ ] 5. Получить токен для **Actions** с правами **repo** и **user**
- [ ] 6. Получить фрагмент вставки значка сервиса **Actions** в формате **Markdown**
- [ ] 7. Выполнить инструкцию учебного материала
- [ ] 8. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_TOKEN=<полученный_токен>
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
```

```sh
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate
$ . scripts/activate
$ rvm autolibs disable
$ rvm install ruby-2.4.2
$ rvm use 2.4.2 --default
$ gem install Actions
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab04
$ cd projects/lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04
```

```sh
$ cat > .Actions.yml <<EOF
language: cpp
EOF
```

```sh
$ cat >> .Actions.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```sh
$ cat >> .Actions.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

```sh
$ Actions login --github-token ${GITHUB_TOKEN}
```

```sh
$ Actions lint
```

```sh
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md
```

```sh
$ git add .Actions.yml
$ git add README.md
$ git commit -m"added CI"
$ git push origin master
```

```sh
$ Actions lint
$ Actions accounts
$ Actions sync
$ Actions repos
$ Actions enable
$ Actions whatsup
$ Actions branches
$ Actions history
$ Actions show
```

## Report

```sh
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

Вы продолжаете проходить стажировку в "Formatter Inc." (см [подробности](https://github.com/tp-labs/lab03#Homework)).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы **CMake**.

```
Copyright (c) 2015-2022 The ISC Authors
```
