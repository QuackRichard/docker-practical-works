###### Подготовка среды для работы с Docker на Windows

![mRemoteNG](https://github.com/mRemoteNG/mRemoteNG/blob/mRemoteNGProjectFiles/Header_dark.png?raw=true)

В нулевом уроке будет описанно, как настроить удобную среду с помощью программы mRemoteNG
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
   - VMware workstation - По сравнению с VMware Player и Oracle VirtualBox оказалась самой удобной для **имеено** для **меня**.
   - mRemoteNG - По сравнению с PuTTY, ssh сессиями запущенными в screen'е, так же оказалась самой удобной + эта программа сама подхватывает мои присеты сессий от PuTTY.
   - ОС Debian - тут как с [женой](https://ru.wikipedia.org/wiki/%D0%96%D0%B5%D0%BD%D0%B0), сам особо не понял почему полюбил именно её.

Перейдём к дейстию:
1. Скачиваем и устанавливаем VMware workstation, mRemoteNG и iso образа ОС Debian, установка VMware workstation пройдёт без проблем так как после ноября 2024 года, программа стала бесплатной для всех, поэтому просто кликаем по принципу next, next install. По такому же принципу устанавливаем mRemoteNG.
2. Создание нашей первой машины хорошо описали [тут](https://remontka.pro/vmware-workstation/#:~:text=%D0%A1%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%B2%D0%B8%D1%80%D1%82%D1%83%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B9%20%D0%BC%D0%B0%D1%88%D0%B8%D0%BD%D1%8B%20%D0%B2%20VMware%20Workstation%20Pro).

Источники:
1) [mRemoteNG documentation](https://mremoteng.readthedocs.io/en/v1.77.3-dev/)
2) [Гипервизор простыми словами](https://www.rusonyx.ru/blog/post/chto-takoe-hypervisor/)
3) [Hypervisor Wiki](https://en.wikipedia.org/wiki/Virtualization)
4) [Сайт Debian](https://www.debian.org/index.html)
5) [Как ]()
