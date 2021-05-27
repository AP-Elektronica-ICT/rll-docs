# Over the aire update strategy for remote labs

## Inleiding
Het Doel van de RemoteLabs oplossing is studenten een IoT ervaring geven zonder dat ze op 
de campus aanwezig moeten zijn. Om dit te realiseren moeten we microcontrollers kunnen 
programmeren via het internet. Hiervoor is er onderzoek gedaan naar technologieën dit zou 
kunnen realiseren.

## Microcontroller
Voor de remote labs oplossing moet er een microcontroller gevonden worden die met het 
internet verbonden kan worden. De microcontroller moet deze functionaliteit hebben zodat 
de studenten de microcontroller zijn firmware via het internet kunnen updaten.
Ik ben begonnen met het een aantal microncontrollers op te zoeken die een ingebouwde wifi 
module hebben. Ik heb specifiek gekozen voor een ingebouwde wifi module omdat dit 
handiger is voor montage.
Bij de microcontrollers die ik heb onderzocht sprong de ESP32 eruit. Deze microcontroller 
beschikt niet enkel over een wifi module maar ook deze draadloze module bevat ook een 
bluetooth mogelijkheid. Met deze extra technologie kunnen de docenten een groter bereik
van labo’s creëren. De microcontroller beschikt over een groot GPIO-pinnen, zo kan er 
verschillende sensoren op één microcontroller worden aangesloten. Dit geeft een bepaalde 
flexibiliteit bij het ontwerpen van de labo’s. 
Een voordeel van deze microcontroller is ook dat er veel documentatie beschikbaar is en dat 
er een groot aantal compatible bibliotheken beschikbaar zijn. Met de beschikbaarheid van 
deze labo’s is het mogelijk om de firmware van de microcontroller te updaten via het 
internet. 
Het enige probleem dat ik had met de ESP32 was dat tijdens het programmeren de boot 
knop moest ingedrukt worden om correct te programmeren. Dit was snel opgelost door een 
condensator tussen de ground en de enable pin van de controller. De controller wordt ook in 
het project op een pcb geplaatst dus is het hier geen probleem. 
Met het behulp van deze microcontroller zullen de studenten via het internet zijn firmware 
kunnen updaten en zo de remote labo’s kunnen uitvoeren.

## OTA-update Technologieën
### Arduino OTA
De Arduino foundation heeft een [bibliotheek](https://www.arduino.cc/reference/en/libraries/arduinoota/) de erbij helpt om arduino compatible 
microcontrollers te programmeren over een wifi verbinding. Om deze bibliotheek te 
kunnen gebruiken moet python op je computer hebben geïnstalleerd.
Voordat je je code over the air kan uploaden naar de microcontroller. Als je de 
arduino IDE gebruikt kan je via file -> examples -> ArduinoOTA -> BasicOTA de 
voorbeeld code vinden. Deze voordbeeld code moet eerst op de microcontroller in 
persoon geprogrammeerd worden op de microcontroller. Voor dat je de code upload 
moet je in de voordbeeld code de passwoord en SSID aanpassen naar de SSID en 
passwoord van het netwerk waar de controller verbonden mee moet worden.

![OTA_SSID_PWD](/img/OTAUpdateStratagy/OTA_SSID_PWD.png)

Wanneer de voordbeeld code is geprogrammeerd op de controller moet je naar de 
seriële monitor gaan, hier zal bij een succesvolle connectie het IP-adres van de 
controller staan. Deze heb je nodig om bij het OTA updaten de juiste controller te 
identificeren.

![OTA_IP](/img/OTAUpdateStratagy/OTA_IP.png)

Wanneer dit allemaal succesvol was, kan je beginnen met het programmeren van de 
code die je OTA wilt updaten. Als je nu je nieuwe code OTA wilt updaten ga je eerst 
naar tools -> port, hier ga je i.p.v. een seriële poort te kiezen een netwerkpoort
kiezen voor de juiste controller.

![OTA_Upload](/img/OTAUpdateStratagy/OTA_Upload_Poort.png)

Het probleem bij deze methode is dat deze methoden niet ontworpen is voor de 
toepassing waarvoor we ze willen gebruiken. Deze methode is ontworpen om 
verschillende microcontrollers eenmaal te programmeren over een netwerk. Deze 
methode is een goede optie als je verschillende controllers éénmaal moet
programmeren zonder dat je fysiek contact moet hebben met de controllers.

### Microcontroller als updateserver
Bij deze methode zal de microcontroller zich gedragen als een webserver. Bij deze 
methode gaan we gebruik maken van verschillende bibliotheken om van de 
controller een webserver te maken, de hooft bibliotheken die we bij deze methode 
gaan gebruiken is de updatebibliotheek. Deze bibliotheek maakt het mogelijk om via
een http request de firmware versie van de controller te updaten. 
Hierbij gaan we gebruik maken van de voordbeeld code OTAWebUpdater deze kunt u 
vinden onder examples -> AdruinoOTA in de arduino IDE. In deze code moet je het 
password en de SSID aanpassen naar de authenticatie van het netwerk waar de 
controller verbinding mee moet maken.

![UpdateServer_SSID_PASWD](/img/OTAUpdateStratagy/UpdateServer_SSID_PASWD.png)

Wanneer je de nodige aanpassingen hebt aangebracht kan je de code uploaden. Deze 
code moeten je fysiek uploaden. Als de code op de controller geprogrammeerd is,
open je de serieel monitor. Hier vind je het IP-adres dat is toegekend aan de 
microcontroller.

![UpdateServer_IP](/img/OTAUpdateStratagy/UpdateServer_IP.png)

Als je deze hebt open je een browser en plaats je het IP-adres van de microcontroller 
in de zoekbalk. Hierbij komt u op een login pagina, het passwoord en de 
gebruikersnaam zijn beide admin. Wanneer je bent ingelogd kom je op de 
“serverIndex” pagina, op deze pagina kun je je code OTA uploaden naar de 
microcontroller.

![UpdateServer_Login](/img/OTAUpdateStratagy/UpdateServer_Login.png)

Op dit moment kun je beginnen met het schrijven van nieuwe code. Wanneer de 
nieuwe code klaar is maak je van je code een binair bestand, dit doe je in de arduino 
IDE door naar sketch toegaan in de bovenstaande menu en hier kies je voor “export 
compield binary”. Het binair bestand zal in dezelfde directory staan als de code.

![UpdateServer_Login](/img/OTAUpdateStratagy/UpdateServer_UploadPage.png)

Het probleem dat zich hier voordoet als we het willen gebruiken voor remote labs, is 
hetzelfde als bij de vorige methode. De OTA-code wordt bij het uploaden van je eigen 
code overschreven. Als je opnieuw code wilt uploaden zal je het volledig proces 
opnieuw moeten doen.

### OTA-drive

OTA-drive is een tool die je toelaat verschillende IoT apparaten te updaten via het 
internet. Het deze tool kan je ook de firmware versie van de microcontroller 
aanpassen.
Voor deze methode moet je eerst een account aanmaken bij otadrive.com. Wanneer 
je een account hebt aangemaakt log je in. Als je ingelogd bent ga je naar de 
“products” pagina hier maak je een nieuw product aan. Bij Het nieuwe product staat 
een knop met een mapje, hier moet je op drukken. Via deze knop kom je op de 
product overview pagina, hier kan je de API key vinden die je nodig gaat hebben voor 
de voordbeeld code. 
De voordbeeld code die je eerst moet uploaden voordat je via OTA kan updaten vind 
je op de documentatie [documentatie](https://otadrive.com/doc/) pagina van OTA-drive. In de voordbeeldcode moet je de API
key aanpassen naar je eigen key. Als dit gebeurt moet je de code fysiek uploaden op 
de controller. Als de code op de controller staat zal je op de product overview pagina 
van de OTA dive website deze pagina vernieuwen en bij een normale werking zal je 
microcontroller toegevoegd zijn aan het product.

Als De controller correct is toegevoegd ga je naar de “device groups” pagina. Op De 
pagina ga je naar jouw apparaat en druk je op het mapje, dit opent een overview 
pagina van je controller. Onderaan deze pagina bij “groups devices “hier moet u het 
huidige versienummer van de firmware ingeven.

![OTADrive_group_properties](/img/OTAUpdateStratagy/OTADrive_GroupProperties.png)

Als je nieuwe code via OTA wilt uploaden moet je de voordbeeld code gebruiken als 
een template deze zal de connectie met OTA-drive stabiliseren. Als je de nieuwe code 
hebt geschreven moet je de versie nummer aanpassen naar een hogere dan de 
voordbeeld code die nu op de controller staat. De code moet je nu omzetten naar 
een binair bestand.
Binnen de overview pagina is er een “firmwares” tap je navigeert naar de tap.
Bovenaan kun je dan een nieuwe firmware toevoegen. Bij het toevoegen kies je het 
binair bestand van je code en je voert de nieuwe versie in en upload je de firmware 
naar OTA Drive. De firmware wordt niet direct op de controller geprogrammeerd 
maar wordt klaargezet bij OTA-drive. 

![OTADrive_group_properties](/img/OTAUpdateStratagy/OTADrive_AddFirmware.png)

Om de code op de microcontroller te plaatsen moet je naar de overview pagina van 
je controller gaan. Hier staat een optie “firmware” daar kunt u de nieuwe firmware 
versie kiezen, als u nu op opslaan drukt zal de nieuwe firmware op het apparaat 
geprogrammeerd worden. 
Als u de tutorial volgt via de documentatie van OTA-drive staat er onderaan de eerste 
pagina een video tutorial. Als u deze tutorial wilt bekijken is het aan te raden een
andere video te gebruiken die u hier kunt vinden. De video op de documentatie 
pagina is gemaakt met de oude versie van OTA-drive.
Deze methode heb ik niet correct kunnen laten werken. Toen ik de voordbeeld code 
met de gekregen API op de controller plaatsten, werd mijn apparaat niet toegevoegd 
bij de apparaten bij OTA-drive. Ik heb hier geen oplossing voor gevonden omdat er 
buiten de documentatie van OTA zelf niet veel informatie is te vinden over deze 
technologie.

### Zelf opgebouwde code 
Omdat de methoden die ik tot hiertoe niet werkte voor de toepassing waar we ze 
willen voor gebruiken, ben ik opzoek gegaan naar een manier waarop we code 
kunnen doorsturen via een zelfgemaakte API. Tijdens mijn onderzoek hiernaartoe 
heb ik een stuk code gevonden van ene Derk Zomer , die met behulp van een nodeJs
API een stuk arduino code de microcontroller OTA kan updaten.
In de API-code staan er twee routes één voor het uploaden van een binair bestand 
dat op het geheugen van de server staat en één voor het controleren van de 
firmware versie die op een database is gezet.
Voor de microcontroller is er voordbeeld code voorzien. Deze code bestaat uit twee 
delen, om de werking te bevestigen gaan ze de code uitlezen en deel twee is om de 
OTA te initialiseren. 
De microcontroller wordt eerst verbonden met een netwerk op dezelfde manier als 
in de vorige methodes. Wanneer de code opstart wordt de netwerk connectie 
gecontroleerd. Als de controller een succesvolle connectie heeft kunnen maken, zal 
de controller aanvraag doen aan de API. De API zal bij deze post request het MACadres van de microcontroller als zoek term voor een MYSQL-query, deze query zoekt 
welke firmware versie er beschikbaar is. De request geeft als resultaat aan de 
microcontroller het MAC-adres van de microcontroller en de firmware versie. 
De microcontroller zal dan controleren of de versie afkomstig van de API groter is dan 
de huidige versie. Als er een hogere versie beschikbaar is zal de controller een 
aanvraag doen naar de API. De API zal hierbij het binair bestand naar de 
microcontroller doorsturen. Als de controller de request goed ontvangen heeft zal 
deze zijn firmware versie updaten. Als de huidige firmware versie groter is dan 
diegene van de API zal de controller melden dat er geen update nodig is.

![APP_Seqentie](/img/OTAUpdateStratagy/APP_DerkZomer_SequentieDiagram.png)

Omdat deze manier het alleen maar toelaat om eenmaal de microcontroller via OTA 
te programmeren, heb ik de code aangepast zodat er meermaals via OTA 
geprogrammeerd kan worden. 
Ik heb aan de arduino een check methode toegepast deze gaat periodiek een call 
doen naar de API die de beschikbare firmware versie opgeeft.

![APP_Seqentie](/img/OTAUpdateStratagy/API_SequentieDiagram.png)

## Conclusie
Bij dit onderzoek heb ik als conclusie gesteld dat om een herhaaldelijke OTA-update
mogelijk te maken, zal er voor de studenten een template voorzien moeten worden. 
Dit template zal ervoor zorgen dat er gecontroleerd kan worden of er een nieuwere 
firmware versie beschikbaar is. Voor Het opgeven van het passwoord en SSID van het 
netwerk, kan er bij initiele setup een config bestand op de controller opslaan met 
behulp van SPIFFS.