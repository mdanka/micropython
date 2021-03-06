Képek
------

A MicroPython körülbelül olyan jól rajzol, mint te, ha csak egy 5x5-ös, piros LED-ekből álló rács áll rendelkezésedre (LED: Light-Emitting Diode, vagyis fényt kibocsátó dióda - a kis cuccok, amik az eszközöd elején világítanak). A MicroPythonnal lehetőséged van szabályozni a kijelzőt, ezáltal sokféle különböző effektust tudsz előidézni.

A MicroPython sok előre beépített képet tartalmaz, amit meg tudsz jeleníteni a kijelzőn. Például, ha szeretnéd, hogy a kijelző vidámnak nézzen ki, a következő kódot kell beírni::

    from microbit import *
    display.show(Image.HAPPY)

Gondolom emlékszel mit csinál a kód első sora. A második sor a ``display`` (magyarul *kijelző*) objektum segítségével mutat (``show``) egy beépített képet. A mosolygós kép, amit ki szeretnénk jelezni, az ``Image`` (kép) objektum tagja, a neve ``HAPPY`` (vidám). Az ``Image.HAPPY`` kódrészletet zárójelek közé rakjuk, ezzel utasítjuk a ``show`` metódust, hogy ezt a képet mutassa.

.. image:: happy.png

A beépített képek listája:

    * ``Image.HEART``
    * ``Image.HEART_SMALL``
    * ``Image.HAPPY``
    * ``Image.SMILE``
    * ``Image.SAD``
    * ``Image.CONFUSED``
    * ``Image.ANGRY``
    * ``Image.ASLEEP``
    * ``Image.SURPRISED``
    * ``Image.SILLY``
    * ``Image.FABULOUS``
    * ``Image.MEH``
    * ``Image.YES``
    * ``Image.NO``
    * ``Image.CLOCK12``, ``Image.CLOCK11``, ``Image.CLOCK10``, ``Image.CLOCK9``,
      ``Image.CLOCK8``, ``Image.CLOCK7``, ``Image.CLOCK6``, ``Image.CLOCK5``,
      ``Image.CLOCK4``, ``Image.CLOCK3``, ``Image.CLOCK2``, ``Image.CLOCK1``
    * ``Image.ARROW_N``, ``Image.ARROW_NE``, ``Image.ARROW_E``,
      ``Image.ARROW_SE``, ``Image.ARROW_S``, ``Image.ARROW_SW``,
      ``Image.ARROW_W``, ``Image.ARROW_NW``
    * ``Image.TRIANGLE``
    * ``Image.TRIANGLE_LEFT``
    * ``Image.CHESSBOARD``
    * ``Image.DIAMOND``
    * ``Image.DIAMOND_SMALL``
    * ``Image.SQUARE``
    * ``Image.SQUARE_SMALL``
    * ``Image.RABBIT``
    * ``Image.COW``
    * ``Image.MUSIC_CROTCHET``
    * ``Image.MUSIC_QUAVER``
    * ``Image.MUSIC_QUAVERS``
    * ``Image.PITCHFORK``
    * ``Image.XMAS``
    * ``Image.PACMAN``
    * ``Image.TARGET``
    * ``Image.TSHIRT``
    * ``Image.ROLLERSKATE``
    * ``Image.DUCK``
    * ``Image.HOUSE``
    * ``Image.TORTOISE``
    * ``Image.BUTTERFLY``
    * ``Image.STICKFIGURE``
    * ``Image.GHOST``
    * ``Image.SWORD``
    * ``Image.GIRAFFE``
    * ``Image.SKULL``
    * ``Image.UMBRELLA``
    * ``Image.SNAKE``

There's quite a lot! Why not modify the code that makes the micro:bit look
happy to see what some of the other built-in images look like? (Just replace
``Image.HAPPY`` with one of the built-in images listed above.)

Elég sok van! Miért ne változtassuk meg a micro:bitet mosolygóssá tevő kódot, hogy az egy másik beépített képet mutasson? (Csak cseréld ki az ``Image.HAPPY`` kódrészletet az egyik fent találhatóval.)

Saját készítésű képek
++++++++++

Ugye szeretnéd megjeleníteni a micro:bit képernyőjén a saját képedeit is?

Ez elég egyszerű.

A képernyőn lévő összes LED pixel tíz különböző értéket vehet fel. Ha egy pixel ``0``-ra van állítva, akkor nem világít. A fényereje nulla. Amikor viszont ``9``-esre van állítva, akkor van a legnagyobb fényereje. Az értékek ``1``-től ``8``-ig egy-egy fényerő-szintet jelölnek, a kikapcsolt állapot (``0``) és a maximális fényerő között.

Armed with this information, it's possible to create a new image like this::
Ennek az információnak a segítségével lehet készíteni új képet::

    from microbit import *

    hajó = Image("05050:"
                 "05050:"
                 "05050:"
                 "99999:"
                 "09990")

    display.show(hajó)

(Futtatás után az eszköz egy ódivatú vitorlást fog mutatni, aminek az árbocai halványabbak, mint a hajó teste.)

Kitaláltad, hogy kell képet rajzolni? Észrevetted, hogy a kijelző minden sorát egy-egy számsor jelöl, ami egy kettősponttal végződik, és idézőjelek (``"``) között van? Minden szám egy fényerőt határoz meg. 5 sor van, mindegyikben van 5 szám, így a kijelző mind az 5 sorának mind az 5 pixelének fényerejét be lehet állítani. Így kell új képet létrehozni.

Egyszerű!

Valójában ezt nem muszáj több sorba írni. Ha úgy gondolod, hogy számon tudod tartani a sorokat, írhatod így is::

    hajó = Image("05050:05050:05050:99999:09990")

Animáció
+++++++++

Az állóképek menők, de sokkal érdekesebb, ha mozognak is. Ez szintén meglepően egyszerű a MicroPythonnal: csak használjunk egy képekből álló listát!

Itt egy bevásárlólista::

    Tojás
    Bacon
    Paradicsom

Ezt a listát így jelenítjük meg Pythonban::

    vásárlás = ["Tojás", "Bacon", "Paradicsom"]

Létrehoztam egy ``vásárlás`` nevű listát, ami három elemet tartalmaz. A Python onnan tudja, hogy ez lista, hogy szögletes zárójelek közé írjuk (``[]``). A lista tagjait vesszővel választjuk el. Ebben az esetben a lista elemei sztringek (a sztring karakterek halmaza): "Tojás", "Bacon" és "Paradicsom". Tudjuk, hogy sztringek, mivel idézőjelek közé írjuk őket.

Pythonban bármit tárolhatsz egy listában. Itt van egy számokból álló lista::

    prímek = [2, 3, 5, 7, 11, 13, 17, 19]


.. note::
    
    Számokat nem kell idézőjelbe rakni, mivel azok egy értéket jelölnek, nem karakterek halmazát. Ez a különbség a ``2`` (a 2-es szám értéke) és a ``"2"`` (a karakter, ami a 2-es számot jelöli) között. Ne aggódj, ha ennek még nem igazán látod értelmét. Hamarosan hozzá fogsz szokni.
    
Egy listában akár különböző fajta dolgokat is tárolhatsz::

    vegyes_lista = ["helló!", 1.234, Image.HAPPY]

Figyelted az utolsó elemet? Az egy kép volt!

A MicroPythont utasíthatjuk egy képekből álló lista animálására. Szerencsére van néhány képekből álló lista előre beépítve. Ezek az ``Image.ALL_CLOCKS`` és az ``Image.ALL_ARROWS``::

    from microbit import *

    display.show(Image.ALL_CLOCKS, loop=True, delay=100)

Mint egy önmagában álló képnél, itt is a ``display.show`` kóddal mutatjuk a képernyőn. Megmondjuk a MicroPythonnak, hogy használja az ``Image.ALL_CLOCKS``-ot, és tudja, hogy mutatnia kell egymás után a listában található összes képet. A ``loop=True`` (magyarul ciklus=Igaz) kóddal azt mondjuk meg, hogy ciklikusan ismétlődjenek a képek (így az animáció örökké tart). A ``delay=100`` (magyarul késleltetés=100) argumentum azt jelenti, hogy a képek közötti késleltetés 100 milliszekundum legyen (100/1000 mp, vagyis 1/10 mp).

Ki tudod találni, hogyan animáld meg az ``Image.ALL_ARROWS`` listát? Hogyan kell kikerülni, hogy az animáció öröké tarson (segítség: a ``True`` (Igaz) ellentéte a ``False`` (Hamis), bár a ``loop`` argumentum alapértelmezett értéke egyébként is ``False``)? Meg tudod változtatni az animáció sebességét?

Végül lássuk, hogyan készítsd el a saját animációdat. Ebben a példában el fogom süllyeszteni a hajómat::

    from microbit import *

    hajó1 = Image("05050:"
                  "05050:"
                  "05050:"
                  "99999:"
                  "09990")

    hajó2 = Image("00000:"
                  "05050:"
                  "05050:"
                  "05050:"
                  "99999")

    hajó3 = Image("00000:"
                  "00000:"
                  "05050:"
                  "05050:"
                  "05050")

    hajó4 = Image("00000:"
                  "00000:"
                  "00000:"
                  "05050:"
                  "05050")

    hajó5 = Image("00000:"
                  "00000:"
                  "00000:"
                  "00000:"
                  "05050")

    hajó6 = Image("00000:"
                  "00000:"
                  "00000:"
                  "00000:"
                  "00000")

    összes_hajó = [hajó1, hajó2, hajó3, hajó4, hajó5, hajó6]
    display.show(összes_hajó, delay=200)

Így működik a kód:

* Készítek hat hajós képet a fent leírt módszerrel.
* Utána belerakom őket egy ``összes_hajó`` nevű listába.
* Végül a ``display.show`` kóddal animációt készítek a lista képeiből. A késleltetés 0,2 másodperc.
* Mivel nem állítottam be a ciklikus ismétlődést (``loop=True``), ezért a hajóm csak egyszer fog elsüllyedni (ezáltal az animációm tudományosan is helytálló lesz). :-)

Te milyen animációt készítenél? Tudsz csinálni különleges effektusokat? Hogyan oldanád meg, hogy egy kép elhalványodjon, majd újra előtűnjön?
