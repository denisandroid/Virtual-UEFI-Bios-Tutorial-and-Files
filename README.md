Russian (<b>черновая версия</b>): 

Полноценный UEFI Bios для устройств не обладающих возможности старта с EFI разделов, работает все от acpi таблиц до мини графического меню биоса.

Компоненты:
1. Tianocore (https://github.com/m13253/tianocore_uefi_duet_installer)
2. Grub mkbootlist


# Возможности:

1. UEFI.
2. Графический режим настройки UEFI, с сохранением настроек.
3. Загрузка с флеш накопителей
4. Готовый образ для GRUB, скрипты для автопривязки образа к GRUB LOAD LIST.
5. Можно адаптировать под syslinux, используя тотже memdisk syslinux.

# Протестировано:

1. Работает загрузка с флеш накопителей
2. Полноценный UEFI. Операционные системы видят что это действительно BIOS UEFI.
3. Не замечено дефектов в работе.
4. Определяет автоматически EFI разделы и запускает операционную систему. Тестировалась Win10.
5. Работает в QEMU.

# Лицензия:
1. Собранный Tianocore: GNU GENERAL PUBLIC LICENSE (1991), GNU GENERAL PUBLIC LICENSE (2007), ...
2. Grub скрипты и собранный образ, ...: Apache License 2.0 (2004)

===========================================

# Процесс установки

```bash
cd /Virtual-UEFI-Bios
cp ./root/* /

grub-mkconfig -o /boot/grub/grub.cfg
```

При правильном использовании должно отобразится:

```
Generating grub configuration file ...
...
Found UEFI+ image: /boot/bios_uefi.gz
...
```

<small>При перезагрузке требуется войти в меню GRUB. Меню GRUB отобразится автоматически или вам потребуется при загрузке компьютера несколько раз нажать ESC и ожидать отображения меню GRUB в нем выбирайте UEFI+. Ожидайте загрузки.

Если все выполнено успешно виртуальный UEFI BIOS должен подхватить ваш EFI BOOT раздел и с него уже прочитать нужный загрузчик и произвести запуск операционной системы с уже виртуальным UEFI. Если так не произошло попробуйте настроить виртуальный UEFI BIOS.</small>

===========================================

# Описание технической части

1. /etc/grub.d/29_uefi скрипт для автогенератора grublist,

Для загрузки сжатого образа UEFI в ОЗУ используется /boot/memdisk, обязательное наличие /boot/memdisk!

2. /boot/bios_uefi.gz

Готовый UEFI BIOS образ для memdisk




