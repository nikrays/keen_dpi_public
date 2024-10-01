# Keen DPI

[Публичная Группа Telegram](https://t.me/keenetic_boost)

## Краткое описание.
#### Проект предназначен для установки и настройки фильтрации интернет-трафика через репозиторий Zapret. Он загружает необходимые пакеты, настраивает автозапуск, изменяет конфигурационные файлы, обновляет список заблокированных доменов и проверяет доступность ключевых сайтов. Также он включает функции автоподбора стратегий и автопроверки доменов.

## Что нового.
Доступна новая версия Keen DPI: 2024.9.3 🎉 

Что нового: 
1. Автоматическая установка необходимых пакетов, загрузка и настройка Zapret. 
2. Настройка правила для фильтрация UDP-трафика (QUIC). 
3. Автоматическое обновление списка доменов от antifilter. 
4. Автоматическое обновление Entware с zapret. 
5. Проверка доступности доменов на факт блокировки по IP. 
6. Автоматический поиск и применение стратегий на лету и применение приватных фейковых пакетов.

## Подготовка.
###  Все условия обязательны! Если у вас была установленна старая версия, то прийдется очистить корневой каталог OPKG, так как этот проект устанавливается на чистый, подготовленный Entware.
- Для форматирования раздела OPKG.
```shell
rm -rf /opt/*
```

- Обновить на канале "предварительный" до [Последней версии](https://docs.keenetic.com/eaeu/ultra/kn-1811/ru/24723-latest-development-release.html).
- В разделе "Интернет-фильтры" отключить все сторонние фильтры (NextDNS, SkyDNS, Яндекс DNS и другие).
- В настройках Ethernet поставить галочки "Игнорировать DNSv4 и DNSv6 интернет-провайдера"
- Необходимо настроить DоT вне зависимости от провайдера, согласно инструкции [Прокси-серверы DNS-over-TLS и DNS-over-HTTPS для шифрования DNS-запросов](https://help.keenetic.com/hc/ru/articles/360007687159).
<details>
    <summary>Обязательно привести настройки DNS к виду как на скриншоте.</summary>

- DoT1:
  ```
  ams01.dnscry.pt
  ```
- DoT2:
  ```
  77.88.8.8
  ```
  ```
  common.dot.dns.yandex.net
  ```
  - Еще один эффективный вариант - использовать ресолвер от yandex 77.88.8.88 на нестандартном порту 1253. Многие провайдеры не анализируют обращения к DNS на нестандартных портах.

![image](https://github.com/user-attachments/assets/4ab290e8-9dcd-4143-a3f2-584fd0a21530)

</details>

- [Установка системы пакетов репозитория Entware на USB-накопитель](https://help.keenetic.com/hc/ru/articles/360021214160).

<details>
    <summary>Короткая инстркция от себя.</summary>
    
1. Подключить флэш накопитель к ПК и подготовить его разделы. Для работы менеджера пакетов OPKG диск должен быть отформатирован в файловой системе EXT, желательно этой программой DiskGenius(архив можно взять в ТГ). В программе выберите флэшку, удалите все разделы, создайте новый как на скриншоте ниже и примените, нажам Save All  в верхнем левом углу.

![Снимок экрана 2024-09-10 174029](https://github.com/user-attachments/assets/0bd134b7-f5c9-4d1f-a22d-f41430c1f655)

![Снимок экрана 2024-09-10 174047](https://github.com/user-attachments/assets/fe08613c-b0fb-41b1-913c-1fd386dee543)

2. В компонентах операционной системы, спуститься в самый низ до раздела Пакеты OPKG и поставить везде галочки как на скриншоте ниже, применить и перезагрузиться.

![Снимок экрана 2024-09-30 132953](https://github.com/user-attachments/assets/4b813281-2b29-4e25-9945-54ae87331dd4)

3. Теперь нужно установить репозиторий системы пакетов Entware.

- Для моделей 4G (KN-1212), Omni (KN-1410), Extra (KN-1710/1711/1713), Giga (KN-1010/1011), Ultra (KN-1810), Viva (KN-1910/1912), Giant (KN-2610), Hero 4G (KN-2310), Hopper (KN-3810) и Zyxel Keenetic II / III, Extra, Extra II, Giga II / III, Omni, Omni II, Viva, Ultra, Ultra II используйте для установки архив mipsel — [mipsel-installer.tar.gz](https://bin.entware.net/mipselsf-k3.4/installer/mipsel-installer.tar.gz).

- Для моделей Ultra SE (KN-2510), Giga SE (KN-2410), DSL (KN-2010), Duo (KN-2110), Ultra SE (KN-2510), Hopper DSL (KN-3610) и Zyxel Keenetic DSL, LTE, VOX используйте для установки архив mips — [mips-installer.tar.gz](https://bin.entware.net/mipssf-k3.4/installer/mips-installer.tar.gz).

- Для моделей Peak (KN-2710), Ultra (KN-1811), Hopper SE (KN-3812) используйте архив aarch64 — [aarch64-installer.tar.gz](https://bin.entware.net/aarch64-k3.10/installer/aarch64-installer.tar.gz).

4. Например скачали [mipsel-installer.tar.gz](https://bin.entware.net/mipselsf-k3.4/installer/mipsel-installer.tar.gz).

- Подключите уже подготовленный накопитель c файловой системой EXT4 к USB-порту роутера. Диск должен отобразиться на странице "Приложения" в разделе "Диски и принтеры".

![Снимок экрана 2024-09-10 174748](https://github.com/user-attachments/assets/56349a82-95f8-46a2-b85a-26f5d2929180)

- Нажмите на флэшку и в корневом каталоге OPKG создайте директорию install, куда положите файл, например [mipsel-installer.tar.gz](https://bin.entware.net/mipselsf-k3.4/installer/mipsel-installer.tar.gz) ниже скринщот как должно быть.

![Снимок экрана 2024-09-10 175124](https://github.com/user-attachments/assets/f508739a-59fd-42be-872a-39733af57cc3)

5. Перейдите на страницу OPKG для выбора накопителя и нажмите применить. Идем в раздел диагностика, открываем журнал, дожидаемся сообщений installer: [5/5] Установка системы пакетов "Entware" завершена! Не забудьте сменить пароль и номер порта! И System configuration save.

![Снимок экрана 2024-09-10 175304](https://github.com/user-attachments/assets/5c451982-a36c-4a3d-aacb-497e8898caa4)

6. Скачайте [Putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe) для работы с протоколами SSH и Telnet. Запустите и выберите тип подключения SSH, впишите IP-адрес роутера в домашнем сегменте Home (по умолчанию 192.168.1.1), укажите 22-й порт или 222-й порт, если не подключается и нажмите кнопку Open. Если заходили под admin, то вводим exe sh.

![Снимок экрана 2024-09-10 175953](https://github.com/user-attachments/assets/066ae86b-237d-4e29-aae8-fd8ef6236b74)

7. Если видите это, то подготовка завершена.

![Снимок экрана 2024-09-10 180159](https://github.com/user-attachments/assets/21c9e155-25cf-41e6-8699-163afc839733)

</details>

- Проверить, что установленны все пакеты под категорией OPKG в наборах компонентов в настройках, также протокол IPv6 и Модули ядра подсистемы Netfilter, он появится в списке пакетов только после установки пакета "Протокол IPv6".

<details>
    <summary>Обязательно привести настройки OPKG к виду как на скриншоте.</summary>

![image](https://github.com/user-attachments/assets/9ee6d4c2-3311-483f-a930-6158c5f5ae82)

  - Проверить наличие галочки Протокол IPV6

![image](https://github.com/user-attachments/assets/bd52fd5c-0d96-40f3-93cf-2af89fdd9358)

</details>

!!! Если хотя бы одно обязательное условие не выполненно, мне не пишите !!!

- Сделать тест blockcheck на ПК, предварительно выключив все сервисы(VPN, proxy, DPI bypass), которые обходят блокировки. Скачать [zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle/archive/refs/heads/master.zip), распаковать, запустить исполняемый файл blockcheck.cmd как на скриншоте.

<details>
    <summary>Короткая инстркция.</summary>

1. Запустить:

![Снимок экрана 2024-09-10 180749](https://github.com/user-attachments/assets/93f9438d-1bf4-400e-bab3-17fc652ef304)

2. Вставить:

Сначала отдельно прогоняем для YouTube:
```bash
rr1---sn-ntq7ynle.googlevideo.com rr2---sn-q4flrnel.googlevideo.com rr3---sn-n8v7kn7k.googlevideo.com rr4---sn-jvhnu5g-n8ve7.googlevideo.com rr5---sn-jvhnu5g-n8v6.googlevideo.com rr6---sn-jvhnu5g-gv8e.googlevideo.com
```
Затем для всего стального, если потребуется:
```bash
rutor.info rutracker.org instagram.com static.cdninstagram.com scontent-hel3-1.cdninstagram.com facebook.com static.xx.fbcdn.net scontent-hel3-1.xx.fbcdn.net x.com api.x.com
```
Или все вместе, но это займет очень много времени, более 4 часов, лучше ставить на ночь:
```bash
rr1---sn-ntq7ynle.googlevideo.com rr2---sn-q4flrnel.googlevideo.com rr3---sn-n8v7kn7k.googlevideo.com rr4---sn-jvhnu5g-n8ve7.googlevideo.com rr5---sn-jvhnu5g-n8v6.googlevideo.com rr6---sn-jvhnu5g-gv8e.googlevideo.com rutor.info rutracker.org instagram.com static.cdninstagram.com scontent-hel3-1.cdninstagram.com facebook.com static.xx.fbcdn.net scontent-hel3-1.xx.fbcdn.net x.com api.x.com
```

3. Отвечать в такой последовательности: 
 - 4 или 6 или 46 решать вам, это означает по каким протоколам ip искать, зачастую "4"
 - у 4 раза
 - ENTER 3 раза
 - запустится тест, файл которого нужно будет скинуть мне в личку.

</details>

### Можно приступать к установке репозитория [Zapret](https://github.com/bol-van/zapret) или написать в группу, предварительно подготовив чистый Entware, чтобы использовать  коммерческий проект с автообновлением. Также можно воспользоваться веб архивом для поиска старой инструкции.
