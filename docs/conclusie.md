# Conclusie
___

In dit document vind u informatie waar rekening gehouden moet worden wanneer er verder aan deze oplssing wordt gewerkt.

## Software

### OTA Update system

Op dit moment kunnen verschillende microcontrollers geprogrameerd worden via het internet. Om dit te realiseren moet er ten allen tijde gebruikgemaakt worden van het Arduino template. de code die op de microcontroller geprogrameerd moet worden moet omgevormd worden naar een binair bestand. Dit bestant wordt upgeload met de versie nummer van de firmware en naar welke controller de code precies gestuurt moet worden. Wanneer al deze informatie is ingegeven kan een microcontroller OTA geupdate worden.

### Arduino Template

Bij het testen van de sensoren/actuatoren is er waargenomen dat bij het combineren van code met MQTT en code met een delay dat de code met de delay niet uitgevoerd wordt. Wanneer Deze twee acties voorkomen in een labo is het aangeraden om een van de acties te laten uitvoeren op een aparte thread.

## Hardware

### Smart Tile's 

Door het onbreken van van bepaalde hardware componenten zijn deze componenten nog niet getest.

> PCB USB-C Power Delivery (PD)

Door Het onbreken van de USB porwer controller is deze PCB nog niet getest kunnen worden.

> Magnetiche connectoren

Door Het onbreken van de magnetiche connectoren is er nog geen houder ontworpen. Bij het ontwerpen van deze houder moet er rekening gehouden worden dat deze voorzien moet worden van magneten. zo kunnnen de tegels onderling met elkaar verbonden kunnen worden.

> Sensoren/actuatoren

Als in verdere fase van de oplossing de studenten een visuele feedback hebben zouden er leds gebruikt worden met een hogere lumen.
Door de demo te filmen is er ondervonden dat normale led's slecht zichtbaar zijn op video.

### Robotplatform

Om de werking van het robotplatform te optimaliseren is aangeraden om bepaalde hardware compnenten aan te passen of te optimaliseren.

>motoren 

Voor de motoren moeten er moeren voorzien worden zodat de motoren steviger in de motor houder vast zit. De aandrijfas van de huidige motoren is zeer kort , dit kan voor problemen zorgen als de moeren worden ingeschroeft. Hiervoor wordt aangeraden om een component te creeren of bestellen die de aandrijfas verlengt.

>PCB

De huidige PCB bevat nog enkele problemen die de werking van de PCB in gedrang brengt. Pin 8 van de H-brug is niet verbonden  met VCC, Dit probleem is opgelost in alle schemas en de gerber files. Het tweede probleem in de PCB is dat de spanningsregelaar aan zijn uitgang geen stabiele spanning levert. De spanning aan de uitgang start op vijf volt en verlaagt tot nul volt. 

Bij het controleren van alle verbindingen heb ik ondervonden dat bepaalde pads op de toplaag in het schema verbonden zijn met de ground. In realiteit zijn deze niet verbonden met de ground. ik weet dit of dit het specifieke probleem is maar dit kan wel een van de redenen zij.

Dit porbleem heb ik niet kunnen oplossen.

