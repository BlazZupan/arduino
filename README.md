Prižiganje LED diod
===================
1. Priklopiš Arduino in [instaliraš programsko opremo](https://www.arduino.cc/en/Guide/MacOSX). Med instalacijo pregledaš, ali lahko zaženeš programček blink, kot piše v [navodilih](https://www.arduino.cc/en/Guide/MacOSX). Če povezava dela, ti bo na Arduionu utripala majhna ledica L.
2. Vzami protoboard in na arduino na pin 13 [priklopi LED diodo](https://www.arduino.cc/en/Tutorial/Blink). Upornost upora odčitaj z barvne kode ter preveri, ali je odčitek pravi tako, da upornost izmeriš z digitalnim multimetrom. Spiši [program](https://www.arduino.cc/en/Tutorial/Blink), ki prižiga in ugaša to LED diodo. Pazi, gre za programski jezik C, ki je malce drugačen od Pythona. 
3. Spremeni program tako, da bo dioda stalno prižgana. Z digitalnim merilnikom napetosti izmeri, kakšen je padec napetosti na LED diodi. Sedaj spremeni upor, preko katerega je LED dioda povezana na Arduino. Med upori izbiraš take, ki imajo upornost med 220 ohmov in 1K ohmov. Ali se napetost na LED diodi spremeni? Izmeri še padec napetosti na uporu in seštej oba padca (torej, padca napetosti na LED diodi in na uporu). Kaj dobiš kot vsoto?
4. Spremeni program tako, da priklopiš LED diodo na pin 2. Spremeni ga potem tako, da uvedeš novo spremenljivko delayTime, v katero zapišeš, koliko časa naj bo dioda prižgana in ugasnjena.
5. Na Arduino priklopi dve diodi, eno naprimer na pin 2 in drugo na pin 3. Spremeni sedaj zgornji program tako, da izmenično prižigaš zdaj eno zdaj drugo diodo.

Nizi in for zanke
=================
1.    Priklopi pet LED diod na Arduino. Uporabiš lahko pine 2, 3, 4, 5, 6. Napiši program za vlak, ki ugaša in prižiga LED diode v vrsti. A pri tem nujno uporabi niz ([Array](https://www.arduino.cc/en/Reference/Array)) in LED diode prižigaj in ugašaj v <for> zanki. Niz lahko uvedeš na vrhu programa, na primer z:

   ~~~
  int myPins[] = {2, 4, 8, 3, 6};
   ~~~

   Primer <for> zanke pa je:

   ~~~
  int i;
  for (i = 0; i < 5; i = i + 1) {
    Serial.println(myPins[i]);
  }
   ~~~

2.   Čas, ko je ena dioda prižgana, zapiši v spremenljivko <delayTime> in to spremenljivko uporabi v stavku <delay>. To najbrž tvoj program že tako ali tako počne (če ne, spremeni). Spreminjaj vrednost te spremenljivke, da so diode prižgane 100 ms ali pa 500 ms.
3. Bi znal v program dodati še eno <for> zanko tako, da prižigaš vlak diod zdaj v eno in nato v drugo smer? S tako imenovanim efektom Darth Vader?
4. Zdaj pa naredi tako, da se hitrost prižiganja in ugašanja LED diod spreminja med 100 ms in 500 ms, v koraku po 100 ms. To lahko narediš tako, da oviješ for zanke za prižiganje diod v novo for zanko, ki spreminja spremenljivko <delayTime>.

Tipka
=====
1.   Odpri nov program. Počisti protoboard in na nanj priključi stikalo, kot kaže spodnja shema.

![tipka](https://www.arduino.cc/en/uploads/Tutorial/button_sch.png "Vezava")

2.   Izpiši stanje tipke z enostavnim programom, ki to stanje [izpiše na serijskem monitorju](https://www.arduino.cc/en/Tutorial/DigitalReadSerial). Program bo stalno izpisoval stanje tipke. Povečaj čas, ko arduino čaka (funkcija <delay>) na 100 ms. Drži tipko pritisnjeno, tako da vidiš, ali se je stanje res spremenilo.
3. Zgornji program spremeni tako, da izpišeš stanje tipke samo takrat, ko se to spremeni. Se pravi, izpišeš stanje 1 takrat, ko je bilo prej stanje 0. Za to boš moral uvesti spremenljivko, ki si ti zapomni stanje tipke. Na primer:

    ~~~
  int state = 0;
    ~~~

    Stanje je na začetku 0 ker predpostaviš, da na začetku tipka ni pritisnjena. Potem pa morda v funkciji <loop()> uporabiš naslednjo kodo:

    ~~~
  int buttonState = digitalRead(pushButton);
  if buttonState != state:
    Serial.println(buttonState);
    state = buttonState;
    ~~~

    Oznaka <!=> pomeni "ni enak" in je eden od operatorjev, ki jih lahko uporabiš v programske jeziku C. Podobne opreatorje si že uporabljal, ko si pisal <for> stavke. Tam si uporabljal operatorje "večji" ali pa "manjši in je enak". Seznam operatorjev, ki jih pozna C, imaš na [wikipediji](https://en.wikipedia.org/wiki/Operators_in_C_and_C%2B%2B). Aha, da ne pozabim: v kodi v tej nalogi lahko odstraniš <delay>. Sedaj, ko ti vse dela, malce poskusi, kaj dobiš. Ali se ti vedno pravilno izpiše ena vrstica z "1" takrat, ko pritisneš tipko? Morda lahko opaziš, zakaj pri branju tipk potrebuješ "debouncing".

4.   Najbolje bi bilo, če bi se ob spremembi stanja tipke poklicala neka tvoja C-jevska funkcija. Torej, ko bi pritisnil tipko, bi se poklicala funkcija <pressed()>. Ko pa bi tipko spet spustil, bi se poklicala funkcija <pressed()>. Na tak način bi bilo dobro spremljati stanja vseh tipal (tole zadnje je slovenski izraz za senzorje). V bistvu moramo programu naročiti, da ob pritisku na tipko prekine s tem, kar trenutno počne, in pokliče funkcijo <released()>. Zedevi torej pravimo "prekinitev" ali angleško "interrupt". Prekinitve določimo kar v funkciji <setup()>. Ardoino Uno ima samo dva vhoda, ki jih stalno spremlja in jih lahko uporabimo za prekinitve. To sta vhoda na priključkih 2 in 3, ki sta na Arduinu poimenovana kot prekinitev z oznako 0 (na pinu 2) in prekinitev z oznako 1 (na pinu 3). Za eno samo tipko zato lahko napišeš funkcijo <setup> kot:

    ~~~
  void setup()
  {
    Serial.begin(9600);
    attachInterrupt(0, pressed, RISING); // pin 2, tipko pritisnemo, napetost se dvign
    attachInterrupt(1, released, FALLING); // digital pin 3 // down
  }
    ~~~

    Vrstico <Serial.begin(9600);> si moral vključiti v zgornjo kodo zato, da boš s <Serial> izpisovala kakšne stvari in na ta način preverjal delovanje programa. V kodo moraš sedaj dodati še funkciji <pressed> in <released>. Ti dve funkciji lahko dodaš po funkciji <setup()>. Na začetku bomo samo izpisali, ali je bila tipka pritisnjena ali pa smo jo spustili. Kakšnih posebnih spremenljivk ne bomo nastavljali.

    ~~~
  void pressed()
  {
    Serial.println("Button pressed");
  }
  
  void released()
  {
    Serial.println("Button released");
  }
    ~~~

    Najkrajša bo sedaj funkcija <loop()>, ki jo dodaš čisto na koncu:

    ~~~
  void loop()
  {
  }
    ~~~

    Zakaj je lahko taka? Zakaj, kljub temu, da je prazna, zadeve še vedno delajo in se stanje tipke izpisuje?

5.   Tole zgoraj je bilo bolj samo sebi namen. Pravzaprav je bilo čisto uporabno, saj smo na ta način preverili, ali nam osnovni program za detekcijo stanja tipke deluje. Sedaj pa zares. Spremeni vezje tako, da dodaš rdečo in zeleno LED diodo. V tvojem programu čisto zgoraj lahko dodaš konstante, ki povedo, na katerih priključkih sta ti dve diodi:

    ~~~
  const int led_red = 5;
  const int led_red = 6;
    ~~~

    Ko je tipka pritisnjena, sedaj želimo prižgati rdečo diodo (zeleno diodo takrat ugasnemo), ko pa je dvignjena, naj gori zelena (rdečo diodo ugasnemo). To boš seveda naredil tako, da spremeniš funkciji <pressed()> in <released()> in tam dodaš stavke za prižiganje in ugašanje diod.
