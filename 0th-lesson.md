[Back to main](https://github.com/QuackRichard/docker-practical-works/tree/main)
###### Подготовка среды для работы с Docker на Windows

![mRemoteNG](https://github.com/mRemoteNG/mRemoteNG/blob/mRemoteNGProjectFiles/Header_dark.png?raw=true)

В нулевом уроке будет описанно, как установить Docker в ОС Debian и настроить удобную среду с помощью программы mRemoteNG
---
> После окончания своей первой рабочей недели в FishTech, Ивану стало интересно поработать с Docker самостоятельно. Самому узнать как его установить, настроить и наконец увидеть версию установленного именно им Docker'а. Основной/домашней ОС Ивана является Windows 10. Начал Иван с выбора и установки программы [гипервизора](https://www.rusonyx.ru/blog/post/chto-takoe-hypervisor/), выбор его пал на VMware Workstation и ОС [Debian](https://www.debian.org/index.html). После успешной установки как программы для виртуализации, так и гостевой ОС, Иван скачал и установил Docker, затем узнал версию программы, успех.

1. Что будет описано в нулевом уроке:
   - Какие программы использую именно я.
   - Откуда их установить.
   - Базовая настройка в этих программах.
   - Как узнать версию установленного Docker.
2. Программы, ОС и ссылки на скачивание:
   - [VMware Workstation 17.6.4](https://disk.yandex.ru/d/fG5QisWQkvQzSw) | sha256 - 10fe3a36f525d88aa133118ab3b5a16b18da88d4aa11b14d74e4164b3fb94ba9
   - [mRemoteNG 1.76.20](https://github.com/mRemoteNG/mRemoteNG/releases/download/v1.76.20/mRemoteNG-Installer-1.76.20.24615.msi)
   - [ОС Debian 13.2](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-13.2.0-amd64-netinst.iso)
3. Почему именно эти программы?
   - VMware workstation - По сравнению с VMware Player и Oracle VirtualBox оказалась самой удобной для **именно** для **меня**.
   - mRemoteNG - По сравнению с PuTTY, ssh сессиями запущенными в screen'е, так же оказалась самой удобной + эта программа сама подхватывает мои присеты сессий от PuTTY.
   - ОС Debian - тут как с [женой](https://ru.wikipedia.org/wiki/%D0%96%D0%B5%D0%BD%D0%B0), сам особо не понял почему полюбил именно её.

Перейдём к дейстию:
<br>❗ПРЕДУПРЕЖДЕНИЕ❗: Работа из-под root пользователя как показана тут, противопоказана на реальных проектах, это учебный стенд, который не жалко в случае поломки системы! Если нужна установка Docker'а, переходим сразу на 13-й этап.
1. Скачиваем и устанавливаем VMware workstation, mRemoteNG и iso образа ОС Debian, установка VMware workstation пройдёт без проблем так как после ноября 2024 года, программа стала бесплатной для всех, поэтому просто кликаем по принципу next, next install. По такому же принципу устанавливаем mRemoteNG.
2. Создание нашей первой машины хорошо описали [тут](https://remontka.pro/vmware-workstation/#:~:text=%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B9%20%D0%BC%D0%B0%D1%88%D0%B8%D0%BD%D1%8B%20%D0%B2%20VMware%20Workstation%20Pro) и [тут](https://dtf.ru/howto/2433221-ustanovka-linux-debian-dlya-nachinayushih), так же не забудьте при установке поставить галку на пункте про ssh server.
3. После того как мы попали в нашу ос, можем приступать к установке самого Docker:
   - Удостоверемся, что установили именно 13-й Debian коммандой:
   ```bash
   cat /etc/os-release | grep "PRETTY_NAME"
   ```
   - Должны получить `PRETTY_NAME="Debian GNU/Linux 13 (trixie)"`
4. Обновим пакеты коммандой:
   ```bash
   apt update && apt upgrade
   ```
5. Настроим ssh-сервер для работы в mRemoteNG:
   - Откроем файл конфигурации:
   ```bash
   nano /etc/ssh/sshd_config
   ```
   - Тут надо раскоментировать параметр #PermitRootLogin и поменять значение:
   ```nano
   #PermitRootLogin prohibit-password -> PermitRootLogin yes
   ```
   - Сохраняем и выходим из файла(ctrl+o enter ctrl+x) и прописываем команду для перезапуска sshd:
   ```bash
   systemctl restart ssh && systemctl status ssh | grep "Active:"
   ```
   - Должно быть: 'Active: active (running)...'
6. Узнаём ip-адрес нашей тачки:
   ```bash
   ip -c a
   ```
   Должны получить 2 адреса: 1) lo-адрес и 2) в **моём** случае адаптера ens33 c адресом 192.168.0.21, запомним.
   ![Debian-docker-practice-ip-c-a-command](https://github.com/QuackRichard/docker-practical-works/blob/main/0th-lesson-materials/Debian-docker-practice-ip-c-a-command.png?raw=true)
   
7. Выйдем из окна ВМ сочетанием клавишь ctrl+alt и откроем программу mRemoteNG:
   ![mRemoteNG-main-gui](https://github.com/QuackRichard/docker-practical-works/blob/main/0th-lesson-materials/mRemoteNG-main-gui.png?raw=true)

8. Нажмём "Файл" -> "Новое подключение" или ctrl+n:
   ![mRemoteNG-new-connection](https://github.com/QuackRichard/docker-practical-works/blob/main/0th-lesson-materials/mRemoteNG-new-connection.png?raw=true)

9. Пишем имя подключения, к примеру "Debian-docker-practice", нажимаем enter и смотрим ниже на вкладку "Конфигурация":
   ![mRemoteNG-configuration-tab](https://github.com/QuackRichard/docker-practical-works/blob/main/0th-lesson-materials/mRemoteNG-configuration-tab.png?raw=true)

10. В этой вкладке есть множество настроек:
   - Из интересного:
      - Значок - для быстрой навигации по подключениям.
      - Имя вкладки - при открытие нескольких соединений с одинаковым именем вкладки, они логично будут в одной вкладке, удобно для группировки нескольких подключений.
   - Из нужного:
        - Имя хоста / IP - сюда пишем ip, который ранее запомнили.
        - Пользователь - так как это учебный стенд, пишу root
        - Пароль - по причине выше, пароль при установке поставил toor, соответственно сюда же пишу toor.
        - Протокол - SSH version 2
        - Порт - 22

11. После успешной настройки подключения, огонёк правее иконки стал зелёным.
   <br>![mRemoteNG-configuration-tab-complete](https://github.com/QuackRichard/docker-practical-works/blob/main/0th-lesson-materials/mRemoteNG-configuration-tab-complete.png?raw=true)

12. Нажимаем два раза по подключению, выбираем "Да" и попадаем на сервер.

13. Установка Docker: WIP
   
Источники:
1) [mRemoteNG documentation](https://mremoteng.readthedocs.io/en/v1.77.3-dev/)
2) [Гипервизор простыми словами](https://www.rusonyx.ru/blog/post/chto-takoe-hypervisor/)
3) [Hypervisor Wiki](https://en.wikipedia.org/wiki/Virtualization)
4) [Сайт Debian](https://www.debian.org/index.html)
5) [Install Docker Engine on Debian](https://docs.docker.com/engine/install/debian/)
