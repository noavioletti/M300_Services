# M300
Doku


# K1 <br>

Um mit dem der LB02 zu beginnen muss man einiges Vorbereiten. <br>
<br>
Dazu gehörte: <br>
- VirtualBox installieren
- Vagrant installieren
- Visual Studio Code installieren
- Git Client installieren
- SSH-Key für Client erstellen 
<br>
Als ich all diese Dinge zur Vorbereitung getätigt habe, konnte ich mit dem nächsten Kapitel beginnen. <br>

# K2 <br>

Git Account: <br>
- Login Mail: 	noavioletti@hotmail.com <br>
- Passwort: 	******* <br>
<br>
Mein Wissenstand: <br>

- Linux: <br>
	Im Bereich Linux habe ich lediglich die Grundkentnisse, was wir in den Schulen un Ük's erarbeitet haben. Im Büro arbeiten wir nur auf Windows umgebungen. <br>
	
- Virtualisierung <br>
	Ich finde ich habe einen sehr guten Wissenstand in der Virtualisierung. Grund dazu ist da wir in unserer Firma fast alle unsere Systeme Virtualisiert sind und ich schon einige Projekte getätig habe. <br>
	
- Vagrant <br>
	Bevor ich dieses Modul besuchte, hatte ich noch nie von Vagrant gehört. <br>
	
- Git <br>
	Ich arbeite in diesem Modul erst mal mit Git. Somit sind meine Kentnisse noch nicht vorhanden gewesen <br>
	
- Mark Down <br> 
	Mark Down ist ebenfall neu für mich. <br>
	
- Systemsicherheit <br>
	Im Bereich Systemsicherheit kannte ich die Meisten Themen bereits und es war nicht vieles Neu <br>
<br>
Meine Lernschritte: <br> 

- Linux: <br>
	Im Bereich Linux kam nicht ein Grosser Wissenzuwachs dazu. Hier war es mehr eine Repetition und Aufrischung von diversen Ablaufen und Funktionen bei Linux. <br>
	
- Virtualisierung <br>
	Bei der Virtualisierung habe ich keinen grossen Zuwachs von meinem Wissen erhalten.
	
- Vagrant <br>
	Vagrant ist ein Tool um sehr einfach Identische Virtuelle Maschinen zu erstellen, mithilfe von Infrstructure as Code. <br>
	Wie arbeitet Vagrant:<br>
	Um mit Vagrant eine VM erfolgreich aufzusetzen muss als erstes ein File erstllt werden. In diesem File werden alle Konfigurationen getätig um die VM anschliessend aufzusetzen. <br>
	Befehle von Vagrant: <br>
- Vagrant init: Erstellt Vagrant File <br>
- Vagrant up: Startet VM und richtet VM nach Vagrant File ein <br>
- Vagrant ssh: SSH Connection auf VM <br>
- Vagrant status: Status anzeige der VM <br>
- Vagrant port: Anzeige der Weitergeleiteten Ports von der VM <br>
- Vagrant halt: Stoppt laufende VM <br>
- Vagrant destroy: löscht VM <br>

- Git <br>
 	Git verwenden wir um unsere Theorie Information zu erhalten. Danach haben wir unseren eigene Account um hier unsere Repsitory zu führen. <br>
	Der Git Client kann auf verschiedene Arten genuzt werden. Er wird unteranderem verwendet um von unserem lokalen Rechner mit unserem Git Account zu Kommunizieren. <br>
	Git Befehle: <br>
- git clone: Repository Clonen <br>
- git pull: Repository aktuallisieren <br>
- gitt add: Datei für Upload vorbereiten <br>
- git commit: Upload bestätigen <br>
- git push: Upload pushen <br>

- Mark Down <br> 
 	Markdown brauchen wir um all unsere Lernschrite zu Dokumentieren. <br>
	Markdown ist ein sehr vereinfachtes HTML. <br>
	Markdown Syntax: http://markdown-syntax.de/Syntax/ <br>
	
- Systemsicherheit <br>
	Viel neues ist in diesem Bereich an Wissen nicht zugewachsen. Es war hier ebenfalls mehr eine Auffrischung und Repetition angelegen heit wie im Berreich Linux. <br>
<br>

# K3 <br>

Nun geht es daran Vagrant besser kennen zu lernen und mit Vagrant zu arbeiten. <br>
<br>
Als erstes erstellte ich eine Directory für meine Zukünftige Vagrant VM (/M300_Services/srv-nv). Als nächster Schritt erzeugute ich ein Vagrant File (Vagrant init). <br>
<br>
Das Vagrant File konnte nun angepasst werden. <br>
Folgende Sachen habe ich angepasst: <br>

- config.vm.hostname = "srv-nv" (Hostename) <br>
- config.vm.box = "ubuntu/xenial64" <br>
- config.vm.box_check_update = false <br>
- config.vm.network "forwarded_port", guest:80, host:8080, auto_correct: true <br>
- vb.gui = true
- config.vm.network "public_network", ip: "192.168.55.10" (Netzwerk) <br>
- vb.memory = "2048" (VM memory) <br>
- vb.cpus = "2" (CPU Cores) <br>
<br>
Mit Vagrant up konnte ich nun die VM Starten. Nun musste ich nur noch überprüfen ob meine es meine Einstellungen planmässig übernommen hat. Ich habe mich mit dem Git Client und Vagrant ssh mich auf die VM verbunden. Mit den ensprechenden Terminal Befehlen von Linux konnte man nun ganz Simpel alle Informationen abrufen und überprüfen. <br>
Testfälle: <br>
ifconfig: inet addr:192.168.55.10 <br>
hostname: srv-nv <br>
memory: 2048 MB <br>
CPU Cores: 2 <br>
Virtual Box Benutzeroberfläche startet ebenfalls mit Vagrant up <br>
Weitere Infos zu meiner Konfiguration beschreibe ich in K4 <br>

# K4 <br>
Ich habe mir eine VM erstellt, die die Möglichkeit hat später als Webserver zu verwenden. <br>
- Apache Server installieren: <br>
	Meine Vagrant VM sollte einen Apache Webserver enthalten. Desswegen muss dies in meinem Vagrant File folgender massen hinterlegt sein. <br>
    sudo apt-get update <br>
    sudo apt-get upgrade <br>
    sudo apt-get install -y apache2 <br>
- Firewall: <br>
	Die Folgenden Commands zeigen was ich in meinem Vagrantfile bezüglich Firewall eingestellt habe. <br>
	sudo apt-get install ufw (ufw Firewall installieren) <br>
    sudo ufw default deny incoming (Jeglicher Einkommender Traffic standardmässig verweigern) <br>
    sudo ufw default allow outgoing Jeglicher Ausgehender Traffic standardmässig erlauben) <br>
    sudo ufw allow 80/tcp (Port 80 öffnen) <br>
    sudo ufw allow 443/tcp (Port 443 öffnen) <br>
    sudo ufw allow 22/tcp (Port 22 öffnen) <br>
    echo "y" | sudo ufw enable (Firewall aktivieren) <br>
- Standard User erzeugen mit Admin Recheten: <br>
	Ich wollte einen Standard User erzeugen somit habe ich dies auch noch in mein Vagrantfile gepackt. <br>
    sudo useradd localadmin (Nutzer erzeugen) <br>
    sudo usermod -aG sudo localadmin (Nutzer in Admin Rechte erteilen) <br>
- SSH <br>
	Damit ich mich via SSH mich sicher verbinden kann müssen wir noch einige Einstellungen Tätigen. <br>
	Zuerste muss ein Key generiert werden (ssh-keygen -t rsa -b 4096) <br>
	Als nächstes muss ich den öffentlichen Schlüssel auf meinem Zielsystem in die Datei schreiben. (ssh-copy-id -i ~/.ssh/id_rsa.pub localadmin@srv-nv) <br>
	<br>
-Testfälle <br>
	HTTP://localhost:8080: Apache default Website muss aufgeführt werden. <br>
	sudo ufw status: Alle vordefinierten Regeln müssen aufgeführt werden <br>
	cat /etc/group: localadmin muss gefunden werden + muss in sudo Gruppe sein <br>
	cat /.ssh/id_rsa | cat /.ssh/id_rsa.pub: SSH Key sollte erstellt worden sein. <br>
	
# K5 <br>

- kurz Reflexion
Ich hatte anfangs einige Schwirigkeiten mit dem Modul, da einiges für mich neu war und ich noch nie damit gearbeitet habe. 
Als ich einigermassen reingekommen bin, lief es relativ gut. Ich habe ebenfalls mein Wissen vergrössern können. <br>
Wenn wir nun vergleichen was ich zuvor kannte im Vergleich mit jetzt, kann ich sagen ich habe einiges dazu lernen können: <br>
- komplette Vagrant Umgebung inkl. Infrstructure as Code <br>
- komplette Git Umgebung <br> 
- Markdown <br>
Diese Themen waren für mich komplettes Neuland. Der Rest war wie ich bei K2 bereits erwähnt habe hilfreiches auffrischen der Themen. <br>
- Meine Probleme <br>
Ich hatte diverse Probleme und Stolpersteine. Mit dem Reverse Proxy hatte ich meine ersten Schwierigkeiten. Ich musste diverse Themen Googeln. Leider landete ich immer in einer Sackgasse. Das gleiche hatte ich mit LDAP.
Auch hier konnte ich weder mit den Unterlagen, die mir zur verfügung standen noch mit meinen Googel künsten erfolgreich werden. <br>
Nun kommen wir zu meinem grössten Problem. Ich brachte es fertig mein Vagrant und mein Virtual Box kaputt zu machen. Ich musste mehrere Stunden investieren um dieses Problem zu lösen. Dieses Problem brachte ebenfalls meinen Zeitplan extrem durcheinander. <br>