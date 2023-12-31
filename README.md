Спринт 1

ЗАДАЧА

```
Опишите инфраструктуру будущего проекта в виде кода с инструкциями по развертке, нужен кластер Kubernetes и служебный сервер (будем называть его srv):

1 Выбираем облачный провайдер и инфраструктуру.
В качестве облака подойдет и Яндекс.Облако, но можно использовать любое другое по желанию.
Нам нужно три сервера:
два сервера в одном кластере Kubernetes: 1 master и 1 app;
сервер srv для инструментов мониторинга, логгирования и сборок контейнеров.

2 Описываем инфраструктуру.
Описывать инфраструктуру мы будем, конечно, в Terraform.
Совет: лучше создать под наши конфигурации отдельную группу проектов в Git, например, devops.
Пишем в README.md инструкцию по развертке конфигураций в облаке. Никаких секретов в коде быть не должно.

3 Автоматизируем установку.
Надо реализовать возможность установки на сервер всех необходимых нам настроек и пакетов, будь то docker-compose, gitlab-runner или наши публичные ключи для доступа по SSH. Положите код автоматизации в Git-репозиторий.
Результат должен быть такой, чтобы после запуска подобной автоматизации на сервере устанавливалось почти всё, что нужно.

Совсем полностью исключать ручные действия не надо, но в таком случае их надо описать в том же README.md и положить в репозиторий.
```

Решение:

Terraform создает инфраструктуру и устанавливает нужные пакеты через bash:
  1) 
  ```
  terraform apply
  ```
  - В процессе установки, выполняются следующие действия: создание виртуальной машины (ВМ), сервисного аккаунта, сетей и сервера srv, который подготавливается с помощью provisioning-скрипта. В ходе установки также устанавливаются необходимые утилиты, пакеты и их зависимости, такие как: ansible, terraform, terragrunt, jq, docker, docker-compose, git, gitlab-runner, kubeadm, kubectl и helm. Кроме того, создается окружение для будущего развертывания кластера k8s. Для автоматического развертывания кластера k8s, на сервер srv клонируются репозитории (kubernetes_setup и форком kubespray) с кодом для развертывания кластера с использованием kubespray. Также производится настройка ключей и разрешений. После развертывания сервера srv, необходимо войти по ssh и запустить скрипт развертывания k8s кластера.
  
  ```
  cd /opt/kubernetes_setup/ && sudo ./cluster_install.sh
  ```
Результаты на скриншотах ниже:
![Sprint1](https://github.com/mazespd/DevOps-Srpint-1/assets/131882625/b9ea5a65-640e-40c6-a760-13e28a258511)

![Sprint1-1](https://github.com/mazespd/DevOps-Srpint-1/assets/131882625/02ea14a3-a02c-4009-9bc7-82643c7b0212)






