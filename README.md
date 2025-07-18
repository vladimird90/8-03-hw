# Домашнее задание к занятию "GitLab" - Дьяков Владимир

### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

**Решение:**

![img](img/8-03-1-1.png)

---

### Задание 2

**Что нужно сделать:**

1. Запушьте [репозиторий](https://github.com/netology-code/sdvps-materials/tree/main/gitlab) на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте:

* файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне;
* скриншоты с успешно собранными сборками.

**Решение:**

.gitlab-ci.yml:
```
stages:
  - test
  - build

test_app:
  stage: test
  image: golang:1.17
  script:
    - go test .
  tags:
    - neto

build_app:
  stage: build
  image: docker:latest
  script:
    - docker build .
  tags:
    - neto
```

![img](img/8-03-2-1.png)

---

### Задание 3*

Измените CI так, чтобы:

* этап сборки запускался сразу, не дожидаясь результатов тестов;
* тесты запускались только при изменении файлов с расширением *.go.

В качестве ответа добавьте в шаблон с решением файл gitlab-ci.yml своего проекта или вставьте код в соответсвующее поле в шаблоне.

**Решение:**

.gitlab-ci.yml:
```
stages:
  - test
  - build

test_app:
  stage: test
  image: golang:1.17
  script:
    - go test .
  tags:
    - neto
  rules:
    - changes:
      - "**/*.go"

build_app:
  stage: build
  image: docker:latest
  script:
    - docker build .
  tags:
    - neto
  needs: []
  ```

![img](img/8-03-3-1.png)