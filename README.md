Prižiganje LED diod
===================
1. Priklopiš Arduino in [instaliraš programsko opremo](https://www.arduino.cc/en/Guide/MacOSX). Med instalacijo pregledaš, ali lahko zaženeš programček blink, kot piše v [navodilih](https://www.arduino.cc/en/Guide/MacOSX). Če povezava dela, ti bo na Arduionu utripala majhna ledica L.
2. Vzami protoboard in na arduino na pin 13 [priklopi LED diodo](https://www.arduino.cc/en/Tutorial/Blink). Upornost upora odčitaj z barvne kode ter preveri, ali je odčitek pravi tako, da upornost izmeriš z digitalnim multimetrom. Spiši [program](https://www.arduino.cc/en/Tutorial/Blink), ki prižiga in ugaša to LED diodo. Pazi, gre za programski jezik C, ki je malce drugačen od Pythona. 
3. Spremeni program tako, da bo dioda stalno prižgana. Z digitalnim merilnikom napetosti izmeri, kakšen je padec napetosti na LED diodi. Sedaj spremeni upor, preko katerega je LED dioda povezana na Arduino. Med upori izbiraš take, ki imajo upornost med 220 ohmov in 1K ohmov. Ali se napetost na LED diodi spremeni? Izmeri še padec napetosti na uporu in seštej oba padca (torej, padca napetosti na LED diodi in na uporu). Kaj dobiš kot vsoto?
4. Spremeni program tako, da priklopiš LED diodo na pin 2. Spremeni ga potem tako, da uvedeš novo spremenljivko delayTime, v katero zapišeš, koliko časa naj bo dioda prižgana in ugasnjena.
5. Na Arduino priklopi dve diodi, eno naprimer na pin 2 in drugo na pin 3. Spremeni sedaj zgornji program tako, da izmenično prižigaš zdaj eno zdaj drugo diodo.

Nizi in for zanke
=================
1. Priklopi pet LED diod na Arduino. Uporabiš lahko pine 2, 3, 4, 5, 6. Napiši program za vlak, ki ugaša in prižiga LED diode v vrsti. A pri tem nujno uporabi niz ([Array](https://www.arduino.cc/en/Reference/Array)) in LED diode prižigaj in ugašaj v <for> zanki. Niz lahko uvedeš na vrhu programa, na primer z:

  int myPins[] = {2, 4, 8, 3, 6};
  
...Primer <for> zanke pa je:

  int i;
  for (i = 0; i < 5; i = i + 1) {
    Serial.println(myPins[i]);
  }

2. Čas, ko je ena dioda prižgana, zapiši v spremenljivko <delayTime> in to spremenljivko uporabi v stavku <delay>. To najbrž tvoj program že tako ali tako počne (če ne, spremeni). Spreminjaj vrednost te spremenljivke, da so diode prižgane 100 ms ali pa 500 ms.
3. Bi znal v program dodati še eno <for> zanko tako, da prižigaš vlak diod zdaj v eno in nato v drugo smer? S tako imenovanim efektom Darth Vader?
4. Zdaj pa naredi tako, da se hitrost prižiganja in ugašanja LED diod spreminja med 100 ms in 500 ms, v koraku po 100 ms. To lahko narediš tako, da oviješ for zanke za prižiganje diod v novo for zanko, ki spreminja spremenljivko <delayTime>.

Tipka
=====
1. Odpri nov program. Počisti protoboard in na nanj priključi stikalo, kot kaže spodnja shema.

![vezava tipke](https://www.arduino.cc/en/uploads/Tutorial/button_sch.png =200x)

2. Izpiši stanje tipke z enostavnim programom, ki to stanje [izpiše na serijskem monitorju](https://www.arduino.cc/en/Tutorial/DigitalReadSerial).
