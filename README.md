# hassio-installer
How to install hass.io onto SSD under a Raspbian.
Raspbian image SD kártyára installálása az USB boot-hoz:
	Kell egy 16, de inkább egy 32GB-os SD kártyára.
	
	Töltsd le a legfrissebb Respbian (stretch lite) image-t.
		https://www.raspberrypi.org/downloads/raspbian/
		
	Töltsd le a balenaEtcher programot.
		https://www.balena.io/etcher/

	Installáld fel a Raspbian image-t az SD-kártyára a balenaEtcher segítségével.
	(Nem kell az SD kártyát formattálni, mert a balenaEtcher megcsinálja.)
	
	Ha kész, válaszd le az SD kártyát majd vedd ki.
	
	Tedd vissza az SD kártyát.

	A root/főkönyvtárba készíts egy 'ssh' nevű üres fájlt, aminek ne legyen kiterjesztése.
	Ez kell ahhoz, hogy elérd SSH-val a Putty segítségével.
	
	Válaszd le az SD kártyát majd vedd ki.
	
	Helyezd be az SD kártyát a RPI SD slotjába.
	
	Dugd be az RPI tápot.
	
	Várd meg amíg az RPI fel boot-ol.
	
Töltsd le a Putty -ot és installáld fel a PC-dre.
		https://www.putty.org/
		
	Keresd meg a router-eden melyik IP címen van az RPI.

	Indítsd el a Putty-ot.
	
	Állíts be a Putty -ban egy SSH kapcsolatot az RPI IP címére.
	
	Lépj be SSH-val az RPI ra a default jelszóval:
		user: pi
		pass: raspberry
	
	Update-ételd fel az SD image-t a következő parancsokkal:
		sudo apt-get update
		sudo apt-get upgrade
		sudo reboot

	Engedélyezd az USB boot módot:
		https://thepi.io/how-to-boot-your-raspberry-pi-from-a-usb-mass-storage-device/
		https://www.raspberrypi.org/forums/viewtopic.php?t=226865
		
		echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
		
		echo program_usb_boot_timeout=1 | sudo tee -a /boot/config.txt
		
		vcgencmd otp_dump | grep 17
		
		vcgencmd otp_dump | grep 66
		
		sudo nano /boot/config.txt
	
	Állítsd le az RPI-t:
		sudo poweroff

Készítsd elő az SSD/HDD-t:
	Installáld fel a Raspbian image-t az SSD/HDD-ra a balenaEtcher segítségével.
	(Nem kell az SSD/HDD-t formattálni, mert a balenaEtcher megcsinálja.)
	
	Ha kész, válaszd le az SSD/HDD-t majd húzd ki.
	
	Dugd vissza az SSD/HDD-t.

	A root/főkönyvtárba készíts egy 'ssh' nevű üres fájlt, aminek ne legyen kiterjesztése.
	Ez kell ahhoz, hogy elérd SSH-val a Putty segítségével.
	
	Válaszd le az SSD/HDD-t majd húzd ki.

Állítsd le az RPI-t:
	sudo poweroff

Vedd ki az SD kártyát.
	
Húzd ki az RPI tápot.

Dugd be az SSD/HDD-t.

Dugd be az RPI tápot.

Várd meg amíg az RPI be bootol az SSD/HDD-ről.

Frissítsd fel az SSD/HDD Respbian-t:
	sudo apt-get update
	sudo apt-get upgrade
	sudo reboot

	sudo raspi-config
		Állísd be a következket:
			SSH, VNC
	sudo reboot

Állítsd le az RPI-t:
	
	sudo poweroff
	
Töltsd le a VNC-t:
	https://www.realvnc.com/en/connect/download/viewer/

	Installáld fel a VNC-t és indítsd el.

Lépj be az RPI-ra.
	

hass.io installálása az SSD/HDD-re egy Docker image-be:
	sudo su
	
	https://github.com/dale3h/hassio-installer
		Ez a szkript hibás, a végén le fog állni 401-s hibával, emiatt kell a következő is.
		curl -sL https://raw.githubusercontent.com/dale3h/hassio-installer/master/hassio_rpi3bp | bash -s

	https://github.com/home-assistant/hassio-installer
		Ez fogja befejezni az installálást.
		FIGYELJ a végére ahol az eszköz tipusát kell helyesen megadni! (raspberrypi3)
		curl -sL https://raw.githubusercontent.com/home-assistant/hassio-installer/master/hassio_install.sh | bash -s -- -m raspberrypi3

	https://www.home-assistant.io/hassio/installation/
		Az  installálás után eléred a saját HA-dat egy adott IP címen.
		http://192.168.xxx.xxx:8123
	
