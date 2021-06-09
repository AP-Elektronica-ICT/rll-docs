# Handleiding voor docenten
___

## Inleiding 

Het opzetten van de labo's bestaat uit twee delen, Het opzetten van de hardware systemen en het opzetten van een Node-RED flow.

## Hardware 
    
> wifi-inloggegevens opslaan op de microcontroller

Note: De inloggegevens moeten één maal op de microcontroller geplaatst worden, Hierna kunnen de gegevens herhardelijk gebruikt worden.
De informatie code kun je vinden in de onderstaande reposetory.

[wifi inloggegevens Reposetory](https://github.com/glcr/RemoteLabsArduinoTemplates)

Alle in het labo gebruikte microcontrollers dienen voorzien te worden van wifi-inloggegevens.  Deze gegevens worden in het geheugen van de microcontroller aangebracht in de vorm van een “wifiConfig.ino” bestand en een “config.txt” bestand.

De inloggegevens worden opgeslagen in het SPIFF-geheugen van de microcontroller. Om het gebruik te kunnen maken van het SPIFF-geheugen moet de LittleFD bibliotheek geïnstalleerd worden. Onder het bibliotheek beheer in de Arduino IDE kun je de “LittleFS_esp32” bibliotheek instaleren.

![Spiff library](/img/ReleasePlan/SpiffLibrary.png)

Om de gegevens op te slaan moet er gebruik gemaakt worden van de “arduino-esp32fs-plugin” (Loro, 2021). Onder de release pagina van de reposetory kan je de plug-in downloaden. De plug-in moet geinstaleerd worden binnen de schetsboek locatie deze kun je vinden onder bestand -> voorkeuren en schetsboek locatie.

![Arduino sketchbook location](/img/ReleasePlan/SketchbookLokatie.png)

Binnen de schetsboek locatie moeten de volgende mappen aangemaakt worden.in de tool map worden alle bestanden afkomstig van de reposetory geplaatst.

![sketchbook mappen](/img/ReleasePlan/sketchbook_mapen.png)
![execute files](/img/ReleasePlan/executeFiles.png)

In de “RemoteLabsArduinoTemplates” repesotory bevindt zich een data map. In de map bevindt zich het “config.txt” bestand, hier zullen de inloggegevens in geplaatst worden.
De inloggegevens moeten in het onderstaande formaat toegevoegd worden in het bestand.

    ```
    SSID,PASSWORD
    ```

Om de gegevens op de microcontroller te plaatsen druk je op data uploaden on der hulpmiddelen. 

![Uploaden](/img/ReleasePlan/IDE_SketchDataUpload.png)
![explorer](/img/ReleasePlan/FileSystem.png)

Om te controleren of de gegevens correct zijn opgeslagen kan het “wifiConfig.ino” bestand op de microcontroller geprogrammeerd worden.

![wifi config repository](/img/ReleasePlan/WifiConfig_Repo.png)

In de serieel monitor kan je controleren of de microcontroller verbonden is met het netwerk.

![wifi config IP](/img/ReleasePlan/WifiConfig_IP.png)

Als deze gegevens correct uitgelezen kunnen worden betekent dit dat ze in het geheugen zijn opgeslagen en bruikbaar zijn in eigen geschreven code.

> Template

Voor elk labo moeten alle labo's fisiek voorzien worden van het template.
De studenten moeten binnen de RemoteLabs oplossing altijd gebruikmaken van een arduino template.

[Template](https://github.com/glcr/RemoteLabsArduinoTemplates)

### Smart Tiles

> Sensoren

Wanneer de nodige gegevens op de microcontroller is geplaatst kan deze in de smart Tile PCB geplaatsd worden. Hiernaa kunnen de gebruikte sensoren/actuatoren op de smart Tiles gemonteerd worden en aangesloten worden op de PCB.

> Positioneren / aansluiten 

De smart Tiles kunnen in verschillende configuratie tegen elkaar geplaatst worden. Plaats de tegels tegen elkaar in de configuratie specifiek aan het labo. Kijk dat de tegels goed onderling aangesloten zijn aan de magnetiche connectoren.

Om het smart tile systeem te voeden moet een USB-C Power Delivery (PD) connector aangesloten worden aan de USB-C connector van de Central Tile.

### Robot platform

> Sensoren

Wanneer de nodige gegevens op de microcontroller is geplaatst kan deze in de smart Tile PCB geplaatsd worden. Op het robot platform kunnnen verschillende sensoren/actuatoren gemonteerd worden. deze worden aangesloten op de PCB.

> Positioneren / aansluiten 

Het robot platform moet bij aanvang van het labo aangesloten worden aan de batterij.
Afhankelijk van het labo zal het robot platform op een bepaalde locatie op de smart tiles geplaatst worden.


## Software

### Node-RED

De studenten hun interactie met de hardware zal gebeuren via het Node-Red dabhboard.Voor elk labo kan het dashboard aangepast worden via de Node-RED flow erdior. Als het labo ontworpen is moet je om deploy drukken om de studenten toegang te geven tot de nieuwe configuratie.

De connectie tussen het Node-RED dashboard en de microcontroller gebeurd met het MQTT-protocol.De MQTT configuratie moet bij elke MQTT block worden toegevoed.

> flow editor

```
https://DomainName:8881-8889
```
> dashboard

```
https://DomainName:8881-8889/ui
```

