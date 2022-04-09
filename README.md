
# *Wi-Fi Controlled Car*

![Лого/Визия на проекта](https://i.imgur.com/6KZrcwA.jpg)

*Проекът представлява количка, която се управлява от компютър, свързан с нея, чрез интернет. За улесняване на управлението на количката, потребителят получава видео на живо и информация от ултразавуков сензор за разстояние. * (задължително)

## Презентация или документация или нещо друго 
[Линк към ресурса]](link)

## Как да си сваля и използвам проекта?

### Инструкции за сваляне

1) Първата стъпка за пресъздаването на този проект е подготвянето на компютъра, от който ще се контролира количката. За целта е нужен езикът за програмиране Python. Може да го инсталирате от [тук](https://www.python.org/downloads/). В случай, че изпозлвате операционна система Linux можете да инсталирате Python и като въведете тези команди в терминала:
Много от дистрибуциите на Linux имат инсталиран Python, за това преди да опитате да го инсталирате може да въведете тази команда, за да проверите дали вече го имате - ```python --version```. В случай, че нямате Python въведете следните команди в терминала:
```
sudo apt update && sudo apt upgrade -y
sudo apt install software-properties-common -y
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.10
python --version
```

2) След като вече имате Python трябва да инсталирате нужните библиотеки. За целта ще ви трябва package manager-а на Python - pip. Python за Windows вклучва pip. В по-новите версии на Python за Linux, pip се инсталира автоматично когато инсталирате Python, ако нямате инсталиран pip можете много лесно да поправите това със следната команда - ```apt install python3-pip```

3) Когато имате Python и pip, можете да започнете да инсталирате нужните за проекта библиотеки, като използвате следните команди в терминала:
```
pip3 install kivy
pip3 install opencv-python
pip3 install requests
```
4) След като вече имате всичко нужно за проекта е време да свалите и самото приложение, като кликнете [тук](https://github.com/ItzNinjaCat/WifiRCCar/archive/refs/heads/app.zip).
5) За проекта е нужнно едно от следните SBC-та:
 * Raspberry Pi 3 Model A+
 * Raspberry Pi 3 Model B
 * Raspberry Pi 3 Model B+
 * Raspberry Pi 4 Model A
 * Raspberry Pi 3 Model B

За подробно ръководсво как да инсталирате опреационна система на Raspberry Pi, както и допълнителни разяснения за самото SBC кликнете [тук](https://projects.raspberrypi.org/en/projects/raspberry-pi-getting-started)

6) Опрерационната система Raspbian, използвана от Raspberry Pi по подразбиране има Python и pip. Единственото, което трябва да направите е да инстлаирате нужните библиотеки със следните команди в терминала:
```
sudo pip3 install opencv-python
sudo pip3 install netifaces
sudo pip3 install arpreq
```
7) Дойде време да инсталирате и кода, който ще контролира количката и ще записва и изпраща видео и информация за разстоянието до сблъсък с обект. Можете да го инсталирате от [тук]. (https://github.com/ItzNinjaCat/WifiRCCar/archive/refs/heads/remote.zip)
### Инструкции за инсталация


1) Приложението, чрез което ще контролирате количката няма нужда от допълнителни ислации, освен гореспоменатите библиотеки.
2) За да може компютърът ви да се свърже с Raspberry Pi-то ви и двете устройства трябва да бъдат свързани с една и съща мрежа. Ако имате достъп до мрежата на мястото където сте свързали Raspberry Pi-то си с монитор, клавиатура и мишка можете просто да се свържете с нея и от тук нататък то автоматично ще се свързва с нея. Ако нямате достъп до мрежата на това място(например, ако смятате да използвате количката навън или от чужд компютър), но знаете името и паролата ѝ можете да я добавите по следния начин:
 1. Отворете терминал и напишете тази команда - ```sudo nano /etc/wpa_supplicant/wpa_supplicant.conf```
 2. В терминала ви ще се отвори текстов редактор, а в него ще видите файлът ```/etc/wpa_supplicant/wpa_supplicant.conf```. В края на този файл добавете следния код:
```
network={
 scan_ssid=1
 ssid="Име на мрежата"
 psk="Парола на мрежата"
}
```
 3. За да запазите промените натиснете Ctrl+S, а за да затворите редактора Ctrl+X.
3) Следващата стъпка е да направите скрипт, който да пуска програмата при стартиране на компютъра. За целта можете да отворите файла `launcher.sh`, който се намира в папката, която свалихте в стъпка №7 от инструкциите за сваляне. За ваше улеснение файлът е готов като единсвеното нещо, което трябва да промените е ред №5 - `cd home/pi/run_script/code`, в случай че папката `run_script` се намира на друго място.
4) За да може да работи скрипта трябва да се превърне в изпълним файл. За целта напишете командата в терминала си докато се намирате в директорията `run_script` - ```chmod 755 launcher.sh```. А за да се пуска всеки път когато пуснете компютъра трябва да въведете ```sudo crontab -e``` в терминала и да добавите този ред накрая на файла - ```@reboot sh /home/pi/run_script/launcher.sh >/home/pi/run_script/logs/cronlog 2>&1```, като ако директорията `run_script` не се намира там трябва да посочите пътя към нея вместо `/home/pi/` и на двете места, на които се споменава на този ред.
5) За да се свържете с количката си трябва да използвате комбинация от Ipv4 адред и порт. Желателно е да сложите статичен адрес на Raspberry Pi-то ви, за да не ви се налага да търсите Ip-то му всеки път. За целта може да следвате това [ръководство](https://www.makeuseof.com/raspberry-pi-set-static-ip/)

### Инструкции за стартиране на проекта


1) За да започнете да управлявате своята количка е нужно първо да се свържете с нея. За целта са ви нужни Ipv4 адред и порт. Портът може да намерите и настроите, като отворите файлът `connections.txt` намиращ се в `run_script/options` директорията. Когато отворите този файл ще видите 4 реда:
 - първият ред (security) има стойност 1 или 0 и от него зависи дали искате допълнителна сигурност при управление на количката. При стойност 0 тази опция е изключена, а при стойност 1 е включена. NB! Когато тази опция е включена трябва да добавите MAC адреса на устройството, от което ще управлявате количката във файла `trusted.txt`. Ако имате повече от едно устройство, с което искате да свързвате количката можете да добавите и техните MAC адреси разделени със запетаи.
 - вторият ред (ctrl_socket_port) отговаря за порта, на който ще бъде отворен сървърът за управление на количката
 - третият ред(info_on) има стойност 1 или 0 по подразбиране е сложен на 1, като при стойност 1 от количката ще се предоставя сървър, от който при управление ще получите видео и информация от сензора, а прио 0 няма да се създава такъв сървър. 
 - четвъртият ред (flask_port) отговаря за порта, на който ще бъде отворен сървърът отговарящ за видео стрийма и данните, получени от ултразвуковия сензор. 
2) Ако сте задали статичен Ipv4 адрес на Raspberry Pi-то си то може да го използвате, при всяко свързване в тази мрежа и може да пропуснете следващите две стъпки, но ако не използвате статично ip ще трябва всеки път да го търсите преди да се свържете с количката. За целта тряба да намерите неговият MAC адрес, както е показано [тук](https://linuxhint.com/get-mac-address-raspberry-pi/) и да го запомните, препоръчително е да си го запишете някъде. 
3) След като сте се сдобили с MAC адрес отворете терминал на устройството, от което ще управлявате количката, въведете командата ```arp -a``` и потърсете ip-то, което отговаря на MAC адреса на Raspberry Pi-то ви. Ще трябва да изпълнявате тази стъпка всеки път, когато искате да се свържете с количката, тъй като Raspberry Pi-то ви има динамично ip и не е сигурно, че ще бъде същото при следващия ви опит за свързване.
4) Raspberry Pi-то ви вече е настроено и вече можете да го свържете с количката си на следните пинове:
```
Движение напред - GPIO пин 24
Движение назад - GPIO пин 24
Завиване наляво - GPIO пин 6
Завиване надясно - GPIO пин 12

Trigger пин на сензора - делител на напрежение, който превръща сигнала от 5V в 3.3V
3.3V сигнал - GPIO пин 4
Echo пин - GPIO пин 21
Vcc пин на сензора - 5V захранващ пин на Raspberry Pi-то
Ground пин на сензора - с Ground пин на делителя на напрежение
Ground пин на делителя на напрежение - Ground пин на Raspberry pi-то
```
4) След като сте поставили Raspberry Pi-то върху количката и сте го закрепили го свържете с USB Type C кабела на количката.
6) Накрая пуснете приложението от компютъра си и въведете Ipv4 адресът на Raspberry Pi-то, порта, който се намира в `connections.txt` файла и ако сте ги пуснали и желате можете да се свържете с камерата и сензора, като въведете следния линк - `http://ip:flask_port/`, като замените 'ip' с ip адреса на Raspberry Pi-то си и flask_port с порта, на който отговаря от гореспоменатия файл.
7) Готови сте! Количката е свързана и можете да започнете да я управлявате и да наблюдавате през камерата, ако сте я пуснали.

## Използвани технологии

* [Python](https://www.python.org/) - *Python e интерпративен език за програмиране от високо ниво. Python разболага с голямо количество вградени и стандартни модули, които значително улесняват работата с него. Освен това поддържа и външни библиотеки, което значително улеснява ползването му.*
* [Kivy](kivy.org) - *Kivy e Python Framework, за създаване на приложения за множество платформи.*
* [Flask](https://flask.palletsprojects.com/en/2.1.x/) - *Flask е уеб framework създаден на Python.*
* [Raspberry Pi](https://www.raspberrypi.com/) - *Raspberry Pi или RPI е серия от едноплаткови компютри с размери на кредитна карта, разработена в Обединеното кралство от специално създадена за целта фондация (Raspberry Pi Foundation) с цел популяризиране на обучението по основи на компютърните науки в училищата.*
* [OpenCV](https://opencv.org/) - *OpenCV e библиотека предназначена главно към компютърното зрение в реално време.*
* [Buildozer](https://buildozer.readthedocs.io/en/latest/) - Buildozer е инструмент за превръщане на Python приложения в мобилни приложения.
## Информация за авторите на проекта

* **Симеон Христов** - *програмист, дизаинер, хардуерист* - [ItzNinjaCat](https://github.com/ItzNinjaCat)
