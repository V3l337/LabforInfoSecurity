# Task1















# Task2
```
Установите поддержку LUKS.
Создайте небольшой раздел, например, 100 Мб.
Зашифруйте созданный раздел с помощью LUKS.
```

1. Создание раздела. Так как ОС стоит на физическом устройстве, добавить и создать новый раздел не получится. Решел создать уже из имеющегося. (данный процес опишу чуть подробнее для себя)
```
У меня есть диск
...
sda                         8:0    0 298.1G  0 disk
├─sda1                      8:1    0     1G  0 part /boot/efi
├─sda2                      8:2    0     2G  0 part /boot
└─sda3                      8:3    0   295G  0 part
  ├─ubuntu--vg-ubuntu--lv 252:0    0   100G  0 lvm  /
  ├─ubuntu--vg-lv--0      252:1    0    70G  0 lvm  /home
  └─ubuntu--vg-lv--1      252:2    0   100G  0 lvm  /var
```
2. Так как /home не сильно влияет на работоспособность сиситемы (работаю из под рута), было решено размонтировать /home (принудительно) -> уменьшить размер файловой системы -> уменьшить размер логического тома -> создать новый логический том -> и создать фаловую систему в новом логическом томе = монтировать /home обратно
```
umount -l /home
e2fsck -f /dev/ubuntu-vg/lv-0  ### проверка и обновление файловой системы
resize2fs /dev/ubuntu-vg/lv-0 69G  ### уменьшаем размер файловой системы
lvreduce -L 69G /dev/ubuntu-vg/lv-0  ### уменьшаем размер логического тома
e2fsck -f /dev/ubuntu-vg/lv-0  ### проверка и обновление файловой системы
lvcreate -L 1G -n new-lv ubuntu-vg  ### создаем новый логический том
mkfs.ext4 /dev/ubuntu-vg/new-lv  ### созадем файловую систему на логический том
mount /home

вывод:
NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
...
sda                         8:0    0 298.1G  0 disk
├─sda1                      8:1    0     1G  0 part /boot/efi
├─sda2                      8:2    0     2G  0 part /boot
└─sda3                      8:3    0   295G  0 part
  ├─ubuntu--vg-ubuntu--lv 252:0    0   100G  0 lvm  /
  ├─ubuntu--vg-lv--0      252:1    0    69G  0 lvm  /home
  ├─ubuntu--vg-lv--1      252:2    0   100G  0 lvm  /var
  └─ubuntu--vg-new--lv    252:3    0     1G  0 lvm
```
3. Шифруем созданый раздел
```
cryptsetup luksFormat /dev/mapper/ubuntu--vg-new--lv
```
4. Открываем созданый раздел
```
cryptsetup open /dev/ubuntu-vg/new-lv cryptovolume
```
5. Проверяю
```
...
sda                         8:0    0 298.1G  0 disk
├─sda1                      8:1    0     1G  0 part  /boot/efi
├─sda2                      8:2    0     2G  0 part  /boot
└─sda3                      8:3    0   295G  0 part
  ├─ubuntu--vg-ubuntu--lv 252:0    0   100G  0 lvm   /
  ├─ubuntu--vg-lv--0      252:1    0    69G  0 lvm   /home
  ├─ubuntu--vg-lv--1      252:2    0   100G  0 lvm   /var
  └─ubuntu--vg-new--lv    252:3    0     1G  0 lvm
    └─cryptovolume        252:4    0  1008M  0 crypt /crypto_volume
```
6. Создаю фаловую систему
```
mkfs.ext4 /dev/mapper/cryptovolume
```
7. Монтирую в систему ОС
```
mkdir /crypto_volume
mount /dev/mapper/cryptovolume /crypto_volume
```
8. Проверяю


