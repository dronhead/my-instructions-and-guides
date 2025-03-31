# Инструкция по изменению прав доступа в Recovery Mode Linux
Данная инструкция поможет:
 - При восстановлении серверов с повреждёнными правами доступа.
 - Когда разработка привела к изменению системных прав (например, скрипт случайно выполнил `chmod -R` на системных файлах).
 - Если система перестала загружаться после неккоректных команд с `chmod` или `chown`.

## Содержание
1. [Вход в Recovery Mode для систем с GRUB (Ubuntu, Debian и др)](#1-вход-в-recovery-mode-для-систем-с-grub-ubuntu-debian-и-др)
2. [Открытие консоли (root shell)](#2-открытие-консоли-root-shell)
3. [Изменение прав через chmod](#3-изменение-прав-через-chmod)
4. [Выход из Recovery Mode](#4-выход-из-recovery-mode)

### 1. Вход в Recovery Mode для систем с GRUB (Ubuntu, Debian и др):
1. Перезагрузите компьютер.
2. В меню GRUB:
	- Удерживайте `Shift` (BIOS) или `Esc` (UEFI).
3. Выберите:
	`Advanced options for Ubuntu > recovery mode`.
4. Нажмите `Enter`.

### 2. Открытие консоли (root shell)
1. В меню Recovery Mode выберите:
	`root > Drop to root shell promt.`
2. Нажмите `Enter`.

### 3. Изменение прав через `chmod`
1. Введите команду:
	```bash
    chmod 755 /usr
	```
	- `755` означает:
		- **7 (владелец):** чтение + запись + выполнение (`rwx`)
		- **5 (группа/остальные):** чтение + выполнение (`r-x`)

2. Проверьте изменения:
	```bash
	ls -ld /usr
	```
	Вывод должен содержать: `drwxr-xr-x`.

### 4. Выход из Recovery Mode

1. Перезагрузите систему:

	```bash
	reboot
	```
	Или:

	```bash
	exit
	```
	> Выберите `resume` в меню Recovery.


# Instructions for changing access rights in Recovery Mode Linux
This instruction will help:
- When restoring servers with damaged access rights.
- When development has led to a change in system rights (for example, a script accidentally executed `chmod -R` on system files).
- If the system stopped loading after incorrect commands with `chmod` or `chown`.

## Contents
1. [Entering Recovery Mode for systems with GRUB (Ubuntu, Debian and others)](#1-entering-recovery-mode-for-systems-with-grub-ubuntu-debian-and-others)
2. [Opening the console (root shell)](#2-opening-the-console-root-shell)
3. [Changing permissions via chmod](#3-changing-permissions-via-chmod)
4. [Exit Recovery Mode](#4-exit-recovery-mode)

### 1. Entering Recovery Mode for systems with GRUB (Ubuntu, Debian and others):
1. Restart your computer.
2. In the GRUB menu:
	- Hold `Shift` (BIOS) or `Esc` (UEFI).
3. Select:
`Advanced options for Ubuntu > recovery mode`.
4. Press `Enter`.

### 2. Opening the console (root shell)
1. In the Recovery Mode menu, select:
`root > Drop to root shell promt.`
2. Press `Enter`.

### 3. Changing permissions via `chmod`
1. Enter the command:
	```bash
    chmod 755 /usr
	```
	- `755` means:
		- **7 (owner):** read + write + execute (`rwx`)
		- **5 (group/other):** read + execute (`r-x`)

2. Check the changes:
	```bash
	ls -ld /usr
	```
	The output should contain: `drwxr-xr-x`.

### 4. Exit Recovery Mode

1. Reboot the system:

	```bash
	reboot
	```
	Or:

	```bash
	exit
	```
	> Select `resume` from the Recovery menu.