## Cyberdefenders: Insider Blue Team Lab

**Category**: Linux, FTK, Kali, Disk, T1496, T1059, T1005, T1003

---
## [0x01] Scenario

After Karen started working for 'TAAUSAI,' she began to do some illegal activities inside the company. 'TAAUSAI' hired you as a soc analyst to kick off an investigation on this case. You acquired a disk image and found that Karen uses Linux OS on her machine. Analyze the disk image of Karen's computer and answer the provided questions.

---
## [0x02] Tools

- FTK Imager

---
## [0x03] Write-Up

---
**Question 1**: What distribution of Linux is being used on this machine?

Исследуемый файл - `FirstHack.ad1` - образ жесткого диска. Файл исследуется с применением специализированного ПО `FTK Imager`. Для того, чтобы определить дистрибутив операционной системы, необходимо открыть раздел `boot`

![ScreenShot](Labs/screenshots/Insider-1.png)

Внутри `boot` находятся файлы, раскрывающие версию и название дистрибутива операционной системы.

**Answer 1**: `kali`

---
**Question 2**: What is the MD5 hash of the apache access.log?

Для того, чтобы определить хэш-сумму файла средствами `FTK Imager` необходимо нажать ПКМ по нужному файлу (`access.log`) и выбрать `Export File Hash List...`

![ScreenShot](Labs/screenshots/Insider-2.png)

Далее сохранить файл (формат `.csv`) в любое удобное место и открыть любым текстовым редактором:

![ScreenShot](Labs/screenshots/Insider-3.png)

**Answer 2**: `d41d8cd98f00b204e9800998ecf8427e`

---
**Question 3**: It is believed that a credential dumping tool was downloaded? What is the file name of the download?

Исходя из файлов, найденных в `/root/Downloads/` видно, что злоумышленник скачал инструмент `mimikatz` (`/root/Downloads/mimikatz_trunk.zip`)

![ScreenShot](Labs/screenshots/Insider-4.png)

**Answer 3**: `mimikatz_trunk.zip`

---
**Question 4**: There was a super-secret file created. What is the absolute path?

При просмотре `.bash_history` (история команд пользователя) относительно пользователя `root` найден абсолютный путь к файла `SuperSecretFile.txt`. При этом в системе этот файл не обнаружен

![ScreenShot](Labs/screenshots/Insider-5.png)

**Answer 4**: `/root/Desktop/SuperSecretFile.txt`

---
**Question 5**: What program used didyouthinkwedmakeiteasy.jpg during execution?

Также в ходе исследования истории команд обнаружено, что файл `didyouthinkwedmakeiteasy.jpg` был использован утилитой `binwalk`

![ScreenShot](Labs/screenshots/Insider-6.png)

**Answer 5**: `binwalk`

---
**Question 6**: What is the third goal from the checklist Karen created?

На рабочем столе пользователя `root` обнаружен файл `Checklist`, где в последнем пункте числится `Profit`:

![ScreenShot](Labs/screenshots/Insider-7.png)

**Answer 6**: `Profit`

---
**Question 7**: How many times was apache run?

Исходя из истории команд пользователя `root`, а также наличия ПУСТЫХ файлов с логами в `/var/log/apache2`, можно сделать вывод о том, что веб-сервер `Apache` не был запущен ни разу

![ScreenShot](Labs/screenshots/Insider-8.png)

**Answer 7**: `0`

---
**Question 8**: It is believed this machine was used to attack another. What file proves this?

В директории `/root` обнаружен скриншот рабочего стола пользователя `Bob`

![ScreenShot](Labs/screenshots/Insider-9.png)

**Answer 8**: `irZLAohL.jpeg`

---
**Question 9**: Within the Documents file path, it is believed that Karen was taunting a fellow computer expert through a bash script. Who was Karen taunting?

Обнаружено, что bash-скрипт должен был применяться или применялся по отношению к сущности `Young`

![ScreenShot](Labs/screenshots/Insider-10.png)

**Answer 9**: `Young`

---
**Question 10**: A user su'd to root at 11:26 multiple times. Who was it?

Исследование пользователей, которые производили попытки аутентификации в 11:26, производится с помощью файла `/var/log/auth.log`

![ScreenShot](Labs/screenshots/Insider-11.png)

Как видно на скриншоте в указанное время функционировал пользователь `postgres`

**Answer 10**: `postgres`

---
**Question 11**: Based on the bash history, what is the current working directory?

Судя по истории команд, последний переход в директорию осуществлен в `../Documents/myfirsthack/` =>`/root/Documents/myfirsthack/`

![ScreenShot](Labs/screenshots/Insider-12.png)

**Answer 11**: `/root/Documents/myfirsthack/`

---