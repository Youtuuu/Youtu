# LB1 M300 Dokumentation

Hier werden einige Funktionen meines Vagrantfiles beschrieben. Dieses Vagrantfile wird einen Apache-Webserver mit einer Website installieren. Ausserdem wird Samba mit den nötigen Konfigurationen für ein Fileshare installiert.

## Vagrantfile
*config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true*


Hier sehen sie Konfigurierten Ports. Mit dem Port 8080, kann zum Beispiel dann die Website über den Browser abgerufen werden.

*config.vm.synced_folder ".", "/var/www/html"*


Hier wird der Synchronisierte Ordner erstellt. Diese Ordner werden dann auf dem Host und der VM ersichtlich sein. In diesem Verzeichnis wird dann auch das HTMl-File für die Website abgespeichert.

*config.vm.network "public_network", type:"dhcp"*


Mit diesem Command wird eine zusätzliche Netzwerkkarte hinzugefügt. Diese wird als Bridged konfiguriert. Somit haben wir nun zwei Netzwerkkarten eine Nat und die andere Bridged.

*sudo apt-get -y install apache2*
*sudo apt-get -y install samba*


Mit diesen zwei Befehlen werden der Apache und Samba Server installiert. Mit dem Parameter -y wird die Installation automatisch durchgeführt.

*sudo touch /etc/samba/smb.conf*


Anschliesend wird das smb.conf File erstellt. In diesem File werden die Konfigurationen für den Samba-Share reingeschrieben.

*echo "TEXT" | sudo tee -a /etc/samba/smb.conf*


Das smb.conf File wird so mit Daten befüllt. Mit dem Parameter -a werden die Zeilen nicht überschrieben sondern werden immer unterhalb eingefügt. In der letzten Zeile wird noch der eine Maske definiert. Ohne diese würde man nicht auf den Share ohne einen user zugreifen können.

*sudo mkdir -p /srv/samba/share*


Der Share wird erstellt. Mit dem Parameter -p wird das Verzeichnis erstellt falls es nicht vorhanden ist.

*sudo service smbd restart*


Nachdem alle Konfigurationen durchgeführt wurden, muss der smbd Service neugestratet werden.

*chown -R nobody.nobody /home/vagrant/share   /   chmod -R 777 /home/vagrant/share*


Mit dieses Commands wird das Verzeichnis für den Samba Share freigegeben. Ohne diese Commands würde nicht ohne gültigen Samba User auf den Share zugegriffen werden können.

*sudo touch /var/www/html/index.html*


Am Schluss wird noch das HTML-File für die Website erstellt, in dieses index.html kann man wieder belibig html-Code einfügen.

## Vagrant auf MacOS
*Schwierigkeiten*


Ich hatte zu beginn einige Startschwierigkeiten, vagrant auf dem Mac laufen zu lassen. Zuerst habe ich es mit einem Separaten Git Bash client probiert, was allerdings nicht funktioniert hatte. Dann habe ich eine Erweiterung für den in MacOS integrierten Terminal gefunden mit welchem Vagrant problemlos funktionierte. 

*Funktionen*


Es wäre möglich, dass der Share nicht überall funktioniert. Bei Windows Maschinen habe ich ein Problem mit der Authentifizierung festgestellt. Auf einem Unix System sollte der Share aber Problemlost laufen.

## Lerndokumentation

Ich habe zu diesem Thema ebenfalls eine kleine Lerndokumentation für meinen Betrieb geschrieben. In dieser habe ich die Grundlagen von Vagrant erwähnt und das Script Zeile für Zeile beschrieben. Die Dokumentation finden sie unter folgendem Link:https://drive.google.com/open?id=1R_s-GW89JtvACbfo9TUgKEQy62UlaRjO
Das ganze in Markdown zu schreiben wäre ein bisschen viel Arbeit für mich gewesen.

