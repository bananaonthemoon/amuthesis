---
title: "Porównanie technik przestrzennej wizualizacji wyników wyborów w Polsce"
titleeng: "2020 presidential election results in Poland - comparison of spatial visualisation techniques"
degreetype: "Praca inżynierska"
author: "THILDAAAAAAA"
major: "YORKETOOOON"
albumid: "431977"
year: "2021"
output: bookdown::pdf_book
site: bookdown::bookdown_site
link-citations: yes
knit: "bookdown::render_book"
---



<!--chapter:end:index.Rmd-->

---
knit: "bookdown::render_book"
---


\newpage
\setlength\parindent{24pt}

\hfill Poznań, dnia ..........

\begin{center}
\large{\textbf{OŚWIADCZENIE}}
\end{center}

\indent Ja, niżej podpisany/a  student/ka Uniwersytetu im. Adama Mickiewicza w Poznaniu oświadczam, że przedkładaną pracę dyplomową napisałem/napisałam samodzielnie. Oznacza to, że przy pisaniu pracy, poza niezbędnymi konsultacjami, nie korzystałem/am z pomocy innych osób, a w szczególności nie zlecałem/am opracowania rozprawy lub jej części innym osobom, ani nie odpisywałem/am tej rozprawy lub jej części od innych osób. \newline
\indent Oświadczam również, że egzemplarz pracy dyplomowej w wersji drukowanej jest całkowicie zgodny z egzemplarzem pracy dyplomowej w wersji elektronicznej. \newline
\indent Jednocześnie przyjmuję do wiadomości, że przypisanie sobie, w pracy dyplomowej, autorstwa istotnego fragmentu lub innych elementów cudzego utworu lub ustalenia naukowego stanowi podstawę stwierdzenia nieważności postępowania administracyjnego w sprawie nadania tytułu zawodowego.

[\hspace{0.6cm}]* - wyrażam zgodę na udostępnianie mojej pracy w czytelni Archiwum UAM

[\hspace{0.6cm}]* - wyrażam zgodę na udostępnianie mojej pracy w zakresie koniecznym do ochrony mojego prawa do autorstwa lub praw osób trzecich

\vspace{5mm}

\begin{footnotesize}
*Należy wpisać TAK w przypadku wyrażenia zgody na udostępnianie pracy w czytelni Archiwum UAM, NIE w przypadku braku zgody. Niewypełnienie pola oznacza brak zgody na udostępnianie pracy.
\end{footnotesize}

\vspace{20mm}


\hfill.............................................. \newline
\null\hfill\begin{scriptsize}(czytelny podpis studenta)\end{scriptsize}


\newpage



<!--chapter:end:00-oswiadczenie.Rmd-->


## Streszczenie {-}

Niniejsza praca porusza kwestie dotyczące najpopularniejszej techniki wizualizacji w historii polskich map wyborczych - kartogramu. Praca opisuje również alternatywne formy wizualizacji przestrzennych - kartogramy geometryczne oraz anamorfozy powierzchniowe, zostały zanalizowane ich wady i zalety w porównaniu do kartogramu właściwego. Przeprowadzone zostały ankiety na 68 studentach w celu zbadania czytelności każdej z technik. Praca została oparte o dane z wyborów prezydenckich w Polsce z 2020 roku, do ich opracowania wykorzystano język programowania R. Wizualizacje kartograficzne zostały wygenerowane za pomocą pakietów cartogram oraz geogrid. Wyniki sugerują, że kartogramy geometryczne są najlepiej odbierane, kiedy są używane w celu oszacowania zjawiska ogółem, a kartogramy nieciągłe stanowią problem dla użytkowników. Kartodiagram Dorlinga jest nieodpowiedni dla danych względnych oraz wąskim zakresem wartości. W pracy nie udało się wyciągnąć jednoznacznych wniosków w kwestii anamorfoz ciągłych i sugerowana jest dalsza praca w tym temacie.


Słowa kluczowe: kartogram geometryczny, mapy anamorficzne, anamorfoza ciągła, anamorfoza nieciągła, kartodiagram Dorlinga 

## Abstract {-}

This work raises the issue of the most popular visualization technique in the history of Polish election maps - the choropleth map. The work also covers alternative forms of spatial visualization - hexagonal and rectangular tile maps and area cartograms were analysed in comparison to the choropleth map. 68 students were surveyed to test the legibility of each technique. The work and its visualisations were based on the 2020 Polish presidential elections data. R packages cartogram and geogrid were used to generate cartographic visualisations. The results suggest that tile maps are best received when used to estimate the overall phenomenon, and that noncontiguous cartograms are problematic for users. Dorling cartogram is’t suitable for relative data with narrow value range. It was not possible to draw unequivocal conclusions in the study regarding continuous cartograms and further work on this topic is suggested.

Keywords: tile map, cartograms, contiguous cartogram, non-contiguous cartogram, Dorling cartogram

\newpage

\setstretch{1.2}\sf\tighttoc\doublespacing

<!--chapter:end:00-abstrakt.Rmd-->


# Wprowadzenie {#wprowadzenie}

Wybory są jednym z podstawowych narzędzi współczesnych demokracji. 
Demokracja pośrednia, znana również jako przedstawicielska, jest dominującą formą demokracji na świecie, funkcjonuje ona również w Polsce.
Encyklopedia PWN (2020) definiuje wybory jako \textit{„sposób powoływania obywateli do pełnienia funkcji publicznych w organach państwowych, a także w organach samorządowych, partii politycznych i in. organizacji społecznych, przez głosowanie na wysuniętych kandydatów lub ich listy.”}

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc11} 

}

\caption{Mapa wyborów prezydenckich w Stanach Zjednoczonych w 1880 roku. Źródło: http://www.mappingthenation.com/blog/the-nations-first-electoral-map/}(\#fig:ryc11)
\end{figure}

Historia map wyborczych sięga ponad 200 lat, kiedy w 1869 roku odbyły się wybory parlamentarne w Paryżu. 
Mapa pokazuje obrazuje zmieniający się nastrój polityczny w stolicy, który doprowadził do zamieszek wewnętrznych, a ostatecznie do wielkiej wojny międzynarodowej i upadku Drugiego Cesarstwa Francuskiego [@cartographia2008]. 
Najstarsza znana mapa wyborów prezydenckich pochodzi jednak z Atlasu Statystycznego Stanów Zjednoczonych opublikowanego w 1883 roku i przedstawia wyniki na poziomie stanów i hrabstw z wyborów prezydenckich w 1880 roku [@schulten2013]. 
Mapa nie tylko pokazuje, która partia wygrała w każdym z hrabstw, ale także ukazuje przewagę partii za pomocą cieniowania gradientowego (Ryc. \@ref(fig:ryc11)).

Postęp w technikach kartograficznych nabrał tempa wraz z rozwojem drukarstwa oraz możliwością tworzenia niestandardowych grafik do gazet [@kongres2013]. 
Pozwoliło to na spopularyzowanie mapy jako formy reprezentacji danych wyborczych oraz w konsekwencji, rozwój technik tworzenia map (Ryc. \@ref(fig:ryc12)-\@ref(fig:ryc13)).

Pomimo swojej długiej historii, mapy wyborcze stały się popularne dopiero w ciągu ostatnich 30 lat. 
W połączeniu z rozwojem technologii mapy stały się jednymi z najbardziej efektywnych sposobów uwieczniania informacji o charakterze przestrzennym, w tym danych wyborczych. 
Pozwalają one nam szybko i łatwo przeanalizować informacje.
Główną zaletą wizualizacji przestrzennych jest możliwość odnoszenia ich do wybranych lokalizacji lub jednostek administracyjnych. 
Możliwość iteracji pozwala na tworzeniu wielu wizualizacji za pomocą tych samych danych.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc12} 

}

\caption{Mapa wyborów prezydenckich w Stanach Zjednoczonych w 1896 roku. Źródło: https://mode.com/blog/presenting-data-election-maps}(\#fig:ryc12)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=200px]{figures/ryc13} 

}

\caption{Mapa wyborów parlamentarnych w Wielkiej Brytanii w 1895 roku. Źródło: http://www.ericson.net/content/2010/11/first-nyt-election-map/}(\#fig:ryc13)
\end{figure}

Jedną z rozwijających się kierunków badań w zakresie kartografii jest wizualizacja. 
Gałąź ta powstała w latach 90. XX wieku wskutek rozwoju oraz upowszechnienia się technologii komputerowych. 
W porównaniu do kartografii, wizualizacja jest elementem procesu poznawczej analizy danych przestrzennych, a jej celem jest odkrywanie prawidłowości i informacji w danych o charakterze przestrzennym. [@maceachren1994].

W Polsce wybory są regulowane przez ustawę z dnia 5 stycznia 2011 r. - [Kodeks wyborczy](https://pkw.gov.pl/uploaded_files/1598525869_kodeks-wyborczy-2020-lipiec.pdf). 
Ustawa ta weszła w życie 1 sierpnia 2011 roku i zawiera przepisy dotyczące m.in. przeprowadzania wyborów prezydenckich. 
Znajdują się w niej również przepisy o warunkach ważności wyborów i przepisy karne za wykroczenia i niektóre przestępstwa popełnione przeciwko wyborom. 
Za organizację i przebieg wyborów odpowiada w Polsce Państwowa Komisja Wyborcza (PKW) z Krajowym Biurem Wyborczym (KBW), które jest jej organem wykonawczym.
Zadaniem Państwowej Komisji Wyborczej jest również gromadzenie oraz udostępnianie informacji wyborczych, w tym wyników wyborów z poziomu obwodów wyborczych oraz jednostek administracyjnych. 

Powszechne, w pełni demokratyczne wybory prezydenckie III Rzeczypospolitej odbyły się po raz pierwszy 25 listopada 1990 roku. 
Wybory prezydenckie odbywają się na zarządzenie Marszałka Sejmu, a kadencja trwa 5 lat. 
Ostatnie wybory na prezydenta RP zostały przeprowadzone 28 czerwca 2020 roku [@marszalek2020].

W przypadku Polski historyczne mapy wyborcze znajdują się m.in. w Atlasie Rzeczypospolitej Polskiej, gdzie przedstawione są wybory prezydenckie z 1990 (Ryc. \@ref(fig:ryc14)) i 1995 roku (Ryc. \@ref(fig:ryc15)). W obu przypadkach przedstawione są wyłącznie kartogramy skokowe, pola odniesienia ograniczono do województw oraz gmin. 

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc14} 

}

\caption{Mapa wyborów prezydenckich w Polsce w 1990 roku. Źródło: Atlas Rzeczypospolitej Polskiej}(\#fig:ryc14)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc15} 

}

\caption{Mapa wyborów prezydenckich w Polsce w 1995 roku. Źródło: Atlas Rzeczypospolitej Polskiej}(\#fig:ryc15)
\end{figure}

Jak wspomniano wyżej, wizualizacja map wyborczych w Polsce ogranicza się w znacznej części do kartogramów skokowych. 
Istnieją inne formy wizualizacji, które przykładają mniejszą wagę do powierzchni i pozwalają na dokładniejsze przedstawienie wartości. 
Są to, m.in., kartogramy geometryczne oraz anamorfozy (kartogramy odwrócone). 
Niska popularność tych form jest związana z przyzwyczajeniem społeczeństwa do analizowania map opartych o jednostki administracyjne jak powiaty lub województwa. 
Trudność potrafią sprawić również zniekształcenia związane z anamorfozą, w skrajnych przypadkach powierzchnia jednostki odniesienia może być nie do rozpoznania. 
Do prawidłowej interpretacji powyżej wspomnianych dwóch rodzajów map niezbędna jest również wiedza o rozmiarach i rozmieszczeniu jednostek.

Celem pracy jest porównanie różnych technik wizualizacji na przykładzie wyborów prezydenckich w 2020 roku w Polsce. 
Nastąpiło to poprzez przygotowanie map używając metod kartogramu właściwego, kartogramu ciągłego, kartogramu geometrycznego, anamorfozy ciągłej, nieciągłej i kartodiagramu Dorlinga oraz oceniono pod względem stopnia ich czytelności. 
Podjęto również próbę porównania właściwości rozpatrywanych technik oraz określenia zakresu ich zastosowania; szukano odpowiedzi na pytanie o to, jaką i na ile dokładną informację można uzyskać na podstawie każdej z technik. 
W tym celu zostały zebrane oraz opracowane dane z Państwowej Komisji Wyborczej, które następnie posłużyły do stworzenia wizualizacji - do tego użyto dwa pakiety z języka R: *cartogram* [@r-cartogram] oraz *geogrid* [@r-geogrid]. 
Opracowane zostały dwie wersje ankiety mające na celu ocenę stopnia trudności interpretacji wizualizacji. 
Ankiety została przeprowadzone z udziałem studentów trzeciego oraz czwartego roku studiów na Wydziale Nauk Geograficznych i Geologicznych UAM, a w oparciu o jej wyniki przeprowadzono analizę czytelności każdej z technik wizualizacji.

<!--chapter:end:01-roz1.Rmd-->


# Przegląd literatury {#lit}

## Kartogramy właściwe oraz ciągłe {#kartogramy1}

Popularną metodą stosowaną do przedstawiania i analizowania zależności zjawisk jest kartogram. 
Jego popularność można zawdzięczyć prostocie oraz łatwości wykonania. Jest to ilościowa metoda średniej intensywności, tzn. ukazuje natężenie, gęstość czy odchylenia od średniej danego zjawiska. 
Odniesieniem dla zjawisk jest powierzchnia pola podstawowego/jednostki przestrzennej, którą wykorzystujemy [@ratajski1989]. 
Najczęściej są to granice administracyjne lub inne, wcześniej przyjęte granice. 
Zmiany w intensywności barw lub szrafów są ściśle związane z natężeniem wartości, tj. odbiorca odbiera pole/jednostkę przestrzenną z intensywniejszym lub ciemniejszym odcieniem jako tą z wyższą wartością.

Wartości badanego zjawiska można wyrazić za pomocą przedziałów klasowych lub w sposób ciągły. 
Ten drugi jest znacznie rzadziej wykorzystywany [@ratajski1989]. 
Tworzenie przedziałów klasowych polega na grupowaniu wartości w grupy. 
Dobór zależy w dużej mierze od charakterystyki rozkładu danych, jednak najczęściej spotykane są:

* przedziały interwałowe (normatywne), których rozpiętość jest uzależniona od zjawiska i jego charakteru funkcjonalnego,

* przedziały o jednakowej rozpiętości. Mogą one powstać np. poprzez podzielenie ekstremalnych wartości zbiorowości przez liczbę planowanych przedziałów;

* przedziały analityczne, które wyznaczane są poprzez analizę danych, np. wyznaczanie przedziałów według postępu arytmetycznego lub geometrycznego.

Chociaż kartogram jest powszechnie używany, jest on często nieadekwatny i prowadzi do mylnej interpretacji [@leonowicz2006]. 
Dobrym przykładem jest kartogram przedstawiający udział głosów w wyborach prezydenckich w Stanach Zjednoczonych w 2016 roku, przedstawiony na Ryc. \@ref(fig:ryc21). 
Użyta została rozbieżna paleta kolorów, gdzie czerwony kolor oznacza przewagę głosów oddanych na kandydata Partii Republikańskiej, a kolor niebieski – Partii Demokratycznej. 
Im ciemniejszy kolor, tym większy udział partii na danym obszarze.

(ref:linkwiki) https://commons.wikimedia.org/wiki/File:United_States_presidential_election_results_by_county,_2020.svg

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc21} 

}

\caption{Mapa wyborów prezydenckich w Stanach Zjednoczonych w 2020 roku. Źródło: (ref:linkwiki)}(\#fig:ryc21)
\end{figure}

Na pierwszy rzut oka można wywnioskować, że Partia Republikańska dominuje w znacznym stopniu na mapie nad Partią Demokratyczną.
Można nawet przypuścić, że kandydat Partii Republikańskiej zdecydowanie wygrał pod względem głosów na niego oddanych. 
Nie jest to jednak prawda, bowiem kolory i ich rozkład przestrzenny nie uwzględnia w tym przypadku powierzchni i częściowo zmylają odbiorcę jakoby rozmieszczenie ludności było równe. 

Obszar, który ma 100 wyborców, z których 90 głosowało na Republikanów, jest pokazany jako ciemnoczerwony z 90% udziałem. 
Dokładnie ten sam kolor jest użyty dla obszaru, który ma 10 000 wyborców, z których 9 000 głosowało na Republikanów. 
Takie wykorzystanie kartogramu zniekształca nasze postrzeganie wyniku wyborów, wpływając na naszą percepcję sugerując, że dominacja czerwieni oznacza więcej głosów i przewagę Partii Republikańskiej. 
Gdyby jednak uwzględnić gęstość zaludnienia, okazałoby się, że znaczna część kraju, w tym obszary pokryte kolorem czerwonym, są słabo zaludnione. 

## Kartogramy geometryczne

W kartogramach geometrycznych jednostki przestrzenne zostają zastąpione polami o jednakowym kształcie i wielkości. 
Najczęściej do tego używane są sześcioboki (heksagony) oraz prostokąty, których przykład jest widoczny na Ryc. \@ref(fig:ryc22), w mniejszym stopniu trójkąty. 
Kartogramy geometryczne są wyjątkowo przydatne przy porównaniach pomiędzy latami, kiedy istnieje szansa, że granice jednostek się zmieniły [@ratajski1989]. 
Kartogramy geometryczne pozwalają nam również ograniczyć stronniczość związany z powierzchnią jednostki. 
Dobrym przykładem dla zastosowania takich pól są Stany Zjednoczone, gdzie większość stanów jest słabo zaludnionych, a jednocześnie są znaczną częścią łącznej powierzchni kraju.

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc22} 

}

\caption{Mapy geometryczne (heksagonalna oraz kwadratowa) na przykładzie Stanów Zjednoczonych. Źródło: https://blog.apps.npr.org/2015/05/11/hex-tile-maps.html}(\#fig:ryc22)
\end{figure}

## Kartogramy eumorficzne

Kartogramy eumorficzne, w przeciwieństwie do tradycyjnych kartogramów pozwalają nam na wizualizację wartości bezwzględnych. 
Różnią się również sposobem wyrażania zmiennych – powierzchnia oraz geometria jednostki zmienia się proporcjonalnie do zmiennej, tj. wysokie wartości powiększają jednostkę, a niskie pomniejszają. 
Skutkiem tego są nienaturalnie zniekształcone i „napęczniałe” kształty. 
Popularność tego rodzaju kartogramów jest niska ze względu na trudności, które odbiorca napotyka [@lamparski2018]. W polskiej literaturze pojawiają się one w kilku wariantach: jako kartogramy eumorficzne lub odwrócone [@ratajski1989], mapy anamorficzne, które następnie dzielone są na mapy anamorficzne styczne i niestyczne [@zyszkowska2012] lub ciągłe i nieciągłe (najczęściej używane w artykułach naukowych, np. @lamparski2018, tłum. z języka angielskiego – *contiguous* oraz *non contiguous*). Warto zaznaczyć, że w języku angielskim kartogram nazywany jest choropleth map i nie należy go mylić z metodą nazwaną cartogram, która odnosi się do map anamorficznych. W tej pracy używane jest pojęcie mapa anamorficzna, mapa anamorficzna ciągła lub nieciągła.

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc23} 

}

\caption{Cartogram Cube - bryła przedstawiająca właściwości anamorfoz powierzchniowych. Anamorfozy ciągłe zaznaczono na niebiesko, na zielono - anamorfozy nieciągłe, na fioletowo - tradycyjną mapę, a na czerwono - idealną anamorfozę. Źródło: Rycina powstała na podstawie artykułu R.E. Roth i in. 2010 (Markowska, 2019)}(\#fig:ryc23)
\end{figure}

Własności anamorfoz została podsumowana na Rycinie \@ref(fig:ryc23) [@roth2010]. 
Przedstawia ona *Cartogram Cube* - jest to graficzna metoda przedstawiania zależności między cechami wpływającymi na atrybuty informacyjne map [@markowska2019].

Anamorfoza ciągła, w przeciwieństwie do anamorfozy nieciągłej, zachowuje swoją topologię, natomiast zmianom ulega zarówno kształt jak i powierzchnia jednostki. 
Jest to także najtrudniejsza forma anamorfozy do skonstruowania, a jednocześnie najbardziej atrakcyjne i skuteczne anamorfozy pod względem graficznego przedstawienia danych niegeometrycznych (Ryc. \@ref(fig:ryc24)). 
Rezultatem tego są opracowane algorytmy, m.in. Gastnera i Newmana [@gastner2004], Dougenika [@dougenik1985] oraz Gusein-Zade’a i Tikunova [@guseinzade1993]. Różnią się one m.in. stopniem zachowania kształtu oraz poprawnością topologii.

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc24} 

}

\caption{Anamorfoza projekcji podczas wyborów prezydenckich w USA. Wielkość każdego stanu jest zgodna z liczbą głosów. Źródło: https://www.reddit.com/r/dataisbeautiful/comments/jomi6h/}(\#fig:ryc24)
\end{figure}

W anamorfozie nieciągłej kształt poszczególnych jednostek zostaje zachowany, a rozmiar powierzchni jest modyfikowany w zależności od wartości zjawiska [@olson1976]. 
W celu zachowania kształtu jednostek odniesienia nie jest możliwe zachowanie ciągłości przestrzennej (topologii) na takich mapach.
Ta klasa anamorfozy jest uważana za najłatwiejszą do opracowania, ponieważ jedynymi przekształceniami mapy podstawowej są te związane ze zmianą rozmiaru pola powierzchni jednostek. 
Pierwszym krokiem w tworzeniu tej wizualizacji jest przekształcenie każdej z jednostek do tego samego rozmiaru. 
Następnie, jeżeli przypisana wartość jest powyżej średniej, to jednostka jest powiększana, a jeśli jest poniżej średniej - pomniejszana. 
Jeżeli różnice między wartościami są niewielkie, tak też zmiany w rozmiarze będą małe. 
W niektórych przypadkach, np. nakładania się jednostek na siebie możliwe jest również przesunięciem centroidów jednostek.

Ostatnim rodzajem anamorfoz, na której skupia się praca, są kartodiagramy anamorficzne Dorlinga. 
Jest to powszechnie stosowana forma wizualizacji w kartografii brytyjskiej [@dorling1996]. 
Technika ta zastępuje rzeczywisty kształt jednostek na rzecz wyeksponowania wartości zjawiska za pomocą kół lub rzadziej heksagonów [@faliszewska2010]. 
Domyślnie środki kół są zlokalizowane centralnie w obrębie jednostek terytorialnych, jednak w przypadku nachodzenia na siebie jednostek podstawowych zalecane jest odsunięcie kół od siebie. 

Porównując mapy anamorficzne z klasycznymi metodami jak kartogramy i kartodiagramy, można zauważyć, że takie wizualizacje wydają się być lepsze z punktu widzenia semiotycznego, jako że kształt pola odniesienia zmieni się wraz wartością zmienną [@krzywickablum2009].
W przypadku map anamorficznych niezbędna jest umiejętność prawidłowego rozpoznania jednostek odniesienia przez odbiorcę zarówno w ich oryginalnym kształcie jak i zdeformowanym, ważna jest również dokładność w szacowaniu ich rozmiaru. 
Aby anamorfoza była skuteczna, człowiek musi być w stanie szybko zrozumieć wyświetlane dane oraz odnieść je do oryginalnego modelu geograficznego. 
Rozpoznawanie z kolei zależy od zachowania podstawowych właściwości, takich jak kształt, orientacja i ciągłość.


<!--chapter:end:02-roz2.Rmd-->


# Metody {#metody}

## Dane {#dane}

Praca została oparta o dane ze strony internetowej Państwowej Komisji Wyborczej, z zakładki dotyczącej wyborów prezydenckich RP w czerwcu 2020 roku [@pkw_2020].
Na stronie dostępne są dane w rozszerzeniach *.csv* oraz *.xlsx* – w pracy skorzystano z plików z rozszerzeniem .csv ze względu na łatwość ich obsługi w środowisku *R*. 
Wyniki głosowania są dostępne w formie wartości bezwzględnych oraz procentowej, z podziałem na obwody, gminy, powiaty oraz województwa. 
Każda z tabel zawiera m.in. kod TERYT, nazwę jednostki, frekwencję, liczbę głosów nieważnych wraz z ich powodami, liczbę lub procent głosów ważnych oraz liczbę lub procent głosów oddanych na danego kandydata. Tabela\@ref(tab:tabela31) przedstawia wybrane kolumny z danych pobranych od Państwowej Komisji Wyborczej.

\begin{table}

\caption{(\#tab:tabela31)Fragment surowych danych wyborczych z II tury Źródło: opracowanie własne na podstawie danych PKW}
\centering
\resizebox{\linewidth}{!}{
\begin{tabular}[t]{>{\centering\arraybackslash}m{1cm}>{\centering\arraybackslash}m{4cm}>{\centering\arraybackslash}m{3cm}>{\centering\arraybackslash}m{3cm}>{\centering\arraybackslash}m{3cm}}
\toprule
TERYT & Województwo & Liczba wyborców uprawnionych do głosowania & Andrzej Sebastian Duda & Rafał Kazimierz Trzaskowski\\
\midrule
20000 & dolnośląskie & 2240376 & 663831 & 824109\\
40000 & kujawsko-pomorskie & 1572933 & 476728 & 542472\\
60000 & lubelskie & 1671659 & 725453 & 368630\\
80000 & lubuskie & 770309 & 199589 & 296849\\
100000 & łódzkie & 1909980 & 718404 & 600673\\
\bottomrule
\end{tabular}}
\end{table}

Do wizualizacji wykorzystano wyniki z pierwszej i drugiej tury wyborów z podziałem dla województw, powiatów oraz gmin w województwie wielkopolskim. 
Na podstawie danych obliczono m.in. frekwencję, odsetek głosów dla dwóch najpopularniejszych kandydatów oraz różnicę w liczbie i odsetku głosów między nimi (Tab.\@ref(tab:tabela32)).

\begin{table}[!h]

\caption{(\#tab:tabela32)Fragment wyczyszczonych danych wyborczych z II tury Źródło: opracowanie własne na podstawie danych PKW}
\centering
\resizebox{\linewidth}{!}{
\begin{tabular}[t]{>{\centering\arraybackslash}m{1cm}>{\centering\arraybackslash}m{3cm}>{\centering\arraybackslash}m{3cm}>{\centering\arraybackslash}m{3cm}>{\centering\arraybackslash}m{3cm}}
\toprule
TERYT & t1\_Andrzej Sebastian Duda & t1\_Rafał Kazimierz Trzaskowski & t2\_Andrzej Sebastian Duda & t2\_Rafał Kazimierz Trzaskowski\\
\midrule
02 & 545001 & 512357 & 663831 & 824109\\
04 & 380190 & 322961 & 476728 & 542472\\
06 & 591234 & 201571 & 725453 & 368630\\
08 & 161894 & 174894 & 199589 & 296849\\
10 & 589185 & 363209 & 718404 & 600673\\
\bottomrule
\end{tabular}}
\end{table}

Dane z granicami administracyjnymi uzyskano ze strony GIS Support [@gissupport]. 
Oryginalne dane pochodzą z Głównego Urzędu Geodezji i Kartografii, jednak nie jest możliwe pobranie stamtąd danych z podziałem na wybrane jednostki administracyjne (tj. powiaty, województwa). 
Wynikiem pobierania są skompresowane foldery z plikami w formacie ESRI Shapefile. 
Każdy plik .shp posiada kolumny *'JPT_SJR_KO'*, *'JPT_KOD_JE'* oraz *'JPT_NAZWA_'*. Kolumna *'JPT_KOD_JE'* jest niezbędna do przeprowadzenia pomyślnego łączenia danych geograficznych z danymi wyborczymi.

Czyszczenie danych zostały przeprowadzone w języku R [@R-base], konieczne jednak były poprawki geometrii na poziomie powiatowym – naprawiono je w programie QGIS. 
Poniższy proces przebiegał praktycznie tak samo w każdym z arkuszy, pojedyncze dodatkowe kroki zostały przeprowadzone przy danych na poziomie gmin, gdzie niezbędne było wyszczególnienie jednostek wyłącznie z województwa wielkopolskiego. 
Pierwszym etapem czyszczenia było usunięcie zbędnych informacji w obu turach, m.in. typ jednostki, % głosów nieważnych oraz powody, przez które stały się nieważne. 
Poprawiono również kody TERYT tak, aby była odpowiedniej długości dla każdej jednostki. 
Za pomocą wspólnej kolumny *TERYT* złączono obie tury.

Dane geograficzne po załadowaniu zostały przekonwertowane do układu współrzędnych 1992, a zbędne kolumny wykluczono. 
Uproszczono geometrię tak, aby zmniejszyć rozmiar pliku i ułatwić jego późniejszą obsługę, ale jednocześnie zmiany nie były widoczne dla odbiorcy. 
Dane dla gmin zostały ograniczone do województwa wielkopolskiego.

Poprzez kolumny *TERYT* złączono dane tekstowe z danymi geograficznymi do jednego pliku. 
Dodatkowo obliczono m.in. wyniki procentowe obu kandydatów oraz frekwencji, liczbową różnicę między kandydatami w II turze oraz różnicę frekwencji (Tab.\@ref(tab:tabela33)). 
Złączony plik zapisano w formacie GeoPackage (rozszerzenie *.gpkg*).

\begin{table}

\caption{(\#tab:tabela33)Fragment wyczyszczonych danych geograficznych oraz danych wyborczych z II tury Źródło: opracowanie własne na podstawie danych PKW}
\centering
\resizebox{\linewidth}{!}{
\begin{tabular}[t]{>{\centering\arraybackslash}m{4cm}>{\centering\arraybackslash}m{2cm}>{\centering\arraybackslash}m{2cm}>{\centering\arraybackslash}m{3cm}>{\centering\arraybackslash}m{2cm}}
\toprule
JPT\_KOD\_JE & t2\_frek & t1\_duda & t2\_roznica\_glosow & roznica\_frek\\
\midrule
dolnośląskie & 66.99291 & 38.20833 & 160278 & 3.526836\\
kujawsko-pomorskie & 65.31378 & 39.54299 & 65744 & 4.283935\\
lubelskie & 66.05695 & 56.66732 & 356823 & 3.739306\\
lubuskie & 64.95134 & 34.19460 & 97260 & 3.545386\\
łódzkie & 69.67905 & 46.62723 & 117731 & 4.028397\\
\bottomrule
\end{tabular}}
\end{table}

Przedziały klas w mapach zostały ustawione ręcznie. 
Kierowano się tym, aby każdy z przedziałów miał podobną liczbę obiektów, środkowa klasa mieściła w sobie wartość średnią, a skrajne przedziały zawierały wartości wychodzące poza jedno odchylenie standardowe. 

## Biblioteki języka R {#biblioteki}

Głównym narzędziem stosowanym w pracy inżynierskiej był język *R*. 
Łącznie użytych zostało 9 pakietów, z czego najważniejszymi były pakiety *cartogram* oraz *geogrid*, które umożliwiały wizualizację danych przestrzennych (Tab. \ref(tab:tabela34)). 
Innymi ważnymi pakietami użytymi w pracy były m.in.: dplyr [@r-dplyr], sf [@r-sf], tmap [@r-tmap] oraz tmaptools [@r-tmaptools].

\begin{table}

\caption{(\#tab:tabela34)Spis użytych bibliotek języka R na każdym etapie tworzenia pracy. Źródło: opracowanie własne}
\centering
\begin{tabular}[t]{>{\raggedright\arraybackslash}m{8cm}>{\raggedright\arraybackslash}m{5cm}}
\toprule
\multicolumn{1}{c}{Etap pracy} & \multicolumn{1}{c}{Użyte biblioteki}\\
\midrule
Wczytanie danych wyborczych & dplyr, stringr, utils\\
Czyszczenie i agregowanie danych wyborczych & dplyr\\
Wczytanie danych przestrzennych & dplyr, sf, utils\\
Uproszczenie geometrii oraz czyszczenie & dplyr, rmapshaper, stringr\\
Łączenie, uzupełnianie i zapisywanie danych & sf\\
\addlinespace
Wczytanie danych oraz tworzenie wizualizacji przy użyciu pakietu cartogram & cartogram, dplyr, sf, tmap, tmaptools\\
Wczytanie danych oraz tworzenie wizualizacji przy użyciu pakietu geogrid & geogrid, dplyr, sf, tmap, tmaptools\\
\bottomrule
\end{tabular}
\end{table}

Pakiet *cartogram* składa się z trzech funkcji: *cartogram_cont(), cartogram_ncont(), oraz cartogram_dorling()*.
*Cartogram_cont()* służy do tworzenia kartogramu anamorficznego ciągłego za pomocą algorytmu zniekształcenia arkusza gumy - gubbersheetingu [@dougenik1985].
*Cartogram_ncont()* tworzy kartogram anamorficzny nieciągły, którego algorytm jest oparty o pracę J. Olson [@olson1976]. 
Przy pomocy argumentu *k* możliwe jest określenie współczynnika ekspansji dla jednostek o większej wartości.
*Cartogram_dorling()* tworzy kartodiagram anamorficzny, opracowany pierwotnie przez D. Dorlinga [@dorling1996]. 
Wizualizacje z tego pakietu tworzone były w połączeniu z pakietem *tmap.* 
Manipulując argumentem *k* mamy wpływ na udział obwiedni jednostki wypełnionej większym okręgiem, a argumentem *m_weight* - wagę ruchomości kół, tj. ustalając w argumencie *m_weight* wartość 0 uniemożliwiamy ruch jednostkek z przypisanego miejsca. Wartość 1 jest domyślną odległością ruchomości jednostki od przypisanego miejsca obliczoną przez algorytm.

W pakiecie *geogrid* przy pomocy funkcji *calculate_grid()* nadawany jest kształt pola odniesienia (tj. heksagon, kwadrat). Następnie generowane są siatki pól (gridy), które oparte są o analizy granic oryginalnych jednostek odniesienia. Kolejnym etapem jest przypisanie gridu do oryginalnych granic za pomocą funkcji *Assign_polygons()*. Ostatnim krokiem jest zwizualizowanie danych przy pomocy pakietu tmap.

<!--chapter:end:03-roz3.Rmd-->


# Wizualizacje {#wizualizacje}

W tym rozdziale przedstawione zostały przykładowe mapy wyborcze używając technik wizualizacji, które można stworzyć za pomocą bibliotek *geogrid* oraz *cartogram.*

## Kartogram właściwy {#kartogramwlasciwy}

Kartogramy właściwe jest najpopularniejszą techniką wizualizacji w Polsce. 
Jest ona prosta w wykonaniu, a odbiorca jest w stanie bez problemu przeanalizować informacje na niej zawarte. 
W Atlasie Rzeczypospolitej Polskiej kartogram zastosowano dla prawie 80% map, a w Narodowym Atlasie Polski jest to 64% map [@debowska2010].
W Polsce najczęściej stosowanych jest pięć przedziałów klasowych, jednak w zależności od liczby jednostek odniesienia można je modyfikować (Ryc. \@ref(fig:ryc41)-\@ref(fig:ryc42)).

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc41} 

}

\caption{Przykład kartogramu właściwego na poziomie województw - poparcie dla Andrzeja Dudy w I turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc41)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc42} 

}

\caption{Przykład kartogramu właściwego na poziomie gmin w województwie wielkopolskim - poparcie dla Rafała Trzaskowskiego w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc42)
\end{figure}

## Kartogramy ciągłe {#kartogramyciagle}

Kartogramy ciągłe są rzadziej stosowane w wizualizowaniu zjawisk społeczno-ekonomicznych. 
Ze względu na ograniczenia percepcyjne kartogramy ciągłe są stosowane głównie, kiedy mamy na celu oszacowanie wartości jednostek, a nie odczytywanie konkretnych wartości (Ryc. \@ref(fig:ryc43)). 

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc43} 

}

\caption{Przykład kartogramu ciągłego na poziomie powiatów - frekwencja w I turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc43)
\end{figure}

## Kartogramy geometryczne {#kartogramygeometryczne}

W polskiej literaturze kartogramy geometryczne są najczęściej tworzone poprzez podzielenie całego badanego obszaru na pola o równym kształcie i wielkości [@ratajski1989]. 
W pracy została użyta zmodyfikowana metoda, w której jednostki odniesienia zostały zmienione na jednakowe pola (heksagonalne lub kwadratowe). 
Pozwala to na łatwiejsze porównywanie wartości różnych obszarów (Ryc. \@ref(fig:ryc44)). 
Tak jak w przypadku kartogramu ciągłego, taki rodzaj wizualizacji jest szczególnie przydatny do szacowania wartości jednostek. 
Wadą tej techniki jest ograniczona możliwość identyfikacji prawdziwych jednostek odniesienia, można to szczególnie na Ryc. \@ref(fig:ryc45), gdzie pomimo małej liczby pól, trudno jest rozpoznać np. województwo wielkopolskie. 

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc44} 

}

\caption{Przykład kartogramu geometrycznego na poziomie województw - poparcie dla Rafała Trzaskowskiego w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc44)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc45} 

}

\caption{Przykład kartogramu geometrycznego na poziomie gmin w województwie wielkopolskim - wzrost frekwencji w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc45)
\end{figure}

## Anamorfoza ciągła {#anamorfozaciagla}

Poniższa technika wizualizacji jest przedmiotem badań kartografów w Polsce, jednak nie zyskała popularności poza tym kręgiem [@krzywickablum2009] [@markowska2018] [@markowska2019] [@lamparski2018]. 
Zaletą tej techniki jest wykorzystanie jednostek administracyjnych, co ułatwia odbiorcy lokalizację oraz rozpoznanie ich. 
Przykład województw jest przystępny do odbioru dla użytkownika nawet, kiedy różnice między jednostkami są duże (Ryc. \@ref(fig:ryc46)). 
Sprawy inaczej się mają w przypadku zastosowania powiatów lub gmin - duża liczba jednostek oraz skrajne wartości powodują znaczną deformację mapy, co zostało zaprezentowane na Ryc. \@ref(fig:ryc47). 
Podsumowując, taka forma wizualizacji jest użyteczna, kiedy prezentowana jest ograniczona liczba jednostek.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc46} 

}

\caption{Przykład anamorfozy ciągłej na poziomie województw - wzrost poparcia dla Andrzeja Dudy w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc46)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc47} 

}

\caption{Przykład kartogramu geometrycznego na poziomie gmin w województwie wielkopolskim - różnica głosów między kandydatami w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc47)
\end{figure}

## Anamorfoza nieciągła {#anamorfozanieciagla}

Podobne zastosowanie do anamorfoz ciągłych mają anamorfozy nieciągłe. 
Mała liczba jednostek oraz różnice między wartościami sprawiają, że mapa jest czytelna dla odbiorcy. 
Zaletą tej techniki jest zachowanie oryginalnej geometrii i lokalizacji, co ułatwia użytkownikowi zlokalizowanie jednostek, np. województw (Ryc. \@ref(fig:ryc48)). 
Zmiana powierzchni jednostek wiąże się jednak z przerwaniem topologii między jednostkami - jest to szczególnie uciążliwe, kiedy mamy jednostkę wewnątrz drugiej i utrudnia odczytanie informacji, np. miasta wewnątrz gmin miejsko-wiejskich (Ryc. \@ref(fig:ryc49)). 
W tym przypadku autor nie zaleca stosowania tej techniki. 
Ważne w tej technice jest również dopasowanie argumentów funkcji tak, aby jednostki na siebie nie nachodziły. 
Możliwości dopasowania zostały omówione w rozdziale \@ref(biblioteki).

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc48} 

}

\caption{Przykład anamorfozy ciągłej na poziomie województw - różnica głosów między kandydatami w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc48)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc49} 

}

\caption{Przykład kartogramu geometrycznego na poziomie gmin w województwie wielkopolskim - frekwencja w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc49)
\end{figure}

## Kartodiagram Dorlinga {#kartodiagramdorlinga}

Kartodiagram Dorlinga wykorzystuje koła jako pola podstawowe, a ich powierzchnia jest zależna od reprezentowanej wartości. 
Atutem tej techniki jest możliwość wyróżnienia obszarów o dużej intensywności zjawiska. 
Tak jak w przypadku dwóch powyższych technik, zalecane jest użycie danych, który mają szeroki zakres wartości. 
Przykładem na to jest Ryc. \@ref(fig:ryc410) - wygenerowana wizualizacja wyraźnie reprezentuje wysokie wartości. 
Na poziomie gmin jednego województwa różnice są również widoczne, nawet przy użyciu wąskiego zakresu wartości (Ryc. \@ref(fig:ryc411)). 
W przypadku powiatów dla całego kraju jednak można napotkać się na problem z natłokiem oraz rozmieszczeniem kół, co wpływa na ocenę wizualną użytkownika. Tak jak wspomniano w rozdziale \@ref(biblioteki), poprzez manipulację argumentami możemy m.in. określić udział obwiedni jednostki wypełnionej większym okręgiem (Ryc. \@ref(fig:ryc412)). Przekłada się to na częściowe zachowanie kształtu wizualizacji i ułatwienie odbioru informacji z mapy.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc410} 

}

\caption{Przykład anamorfozy ciągłej na poziomie województw - wzrost poparcia dla Andrzeja Dudy w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc410)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc411} 

}

\caption{Przykład kartogramu geometrycznego na poziomie gmin w województwie wielkopolskim - poparcie dla Rafała Trzaskowskiego w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc411)
\end{figure}

\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc412} 

}

\caption{Przykłady kartogramu geometrycznego na poziomie powiatów z trzema wariantami argumentu k - różnica głosów między kandydatami w II turze wyborów.Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc412)
\end{figure}

<!--chapter:end:04-roz4.Rmd-->


# Ankieta {#ankieta}

## Ankiety dotyczące map wyborczych {#ankietyintro}

W ramach pracy zostały przeprowadzone dwie ankiety w celu zbadania czytelności wybranych technik wizualizacji. 
Każda z ankiet zawierała siedem pytań z dołączonymi do nich wizualizacjami. 
Pytania były takie same dla obu grup, różniły je jednak użyte wizualizacje. 
Podział na grupy miał na celu określenie, która z technik pozwala na lepszą ocenę zjawiska. 
Do każdego pytania znano prawidłową odpowiedź. 
Osoby wypełniające ankietę były studentami drugiego, trzeciego i czwartego roku studiów na Wydziale Nauk Geograficznych i Geologicznych UAM, można więc przyjąć, że ich wiedza kartograficzna i geograficzna była na podobnym poziomie. 
Na każdą z ankiet poprzez platformę Google Forms odpowiedziały 34 osoby. 
Skale barw dla map zostały wybrane w taki sposób, aby każdy przedział był dobrze rozróżnialny i nie sugerował partii politycznej (tj. czerwony i niebieski). 
W anamorfozie ciągłej oraz nieciągłej zastosowano tylko jeden kolor - celem tego było sprawdzenie w jakim stopniu zmiana w kształcie jednostek ma wpływ na percepcję oraz czytelność mapy. 
Przy wyborze skali barw pod uwagę wzięto również osoby z daltonizmem, aby zmniejszyć szansę przypadkowego wybierania odpowiedzi.

### Pytanie pierwsze {#pyt1}

**Pytanie: Jaki odsetek powiatów miało frekwencję powyżej 60%?**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc51} 

}

\caption{Anamorfoza ciągla oraz kartogram ciągły - frekwencja w II turze wyborów. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc51)
\end{figure}
**Poprawna odpowiedź: 66%**

W pierwszym pytaniu osoby miały za zadanie odpowiedzieć na pytanie dot. odsetka powiatów z frekwencją powyżej 60% (Ryc. \@ref(fig:ryc51)).
W grupie pierwszej w celu wizualizacji została używa anamorfoza ciągła, a w drugiej kartogram ciągły. 
Wyniki w grupach były podobne - w każdej z grup dwie osoby uważały, że *mniej niż 20%* powiatów miało wysoką frekwencję. 
Niewiele więcej osób wybrało odpowiedź, iż wynik oscyluje *między 20 a 40%* - były to cztery osoby w pierwszej grupie, w drugiej sześć osób (Ryc. \@ref(fig:ryc52)). 
W pierwszej grupie najwięcej osób (14 os.) wybrało wariant *40-60%*, w drugiej grupie było to 11 osób. 
Poprawną odpowiedź, czyli *60-80%* wybrało po 12 osób w każdej z grup. 
Tylko dwie osoby z grupy pierwszej, a trzy z drugiej uważały, że odsetek jest *wyższy niż 80%*. 

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc52} 

}

\caption{Wykres z wynikami do pytania pierwszego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc52)
\end{figure}

### Pytanie drugie {#pyt2}

**Pytanie: W jakim % gmin kandydat B wygrał w II turze?**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc53} 

}

\caption{Kartodiagram Dorlinga oraz kartogram geometryczny - poparcie dla kandydata B w II turze. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc53)
\end{figure}
**Poprawna odpowiedź: 36,3%**

Kartodiagram Dorlinga oraz kartogram geometryczny (heksagonalny) wykorzystano w pytaniu drugim (Ryc. \@ref(fig:ryc53)). 
Mapy różnią się od siebie wartościami przedziałów, mimo tego w pytaniu drugim osiem osób w obu grupach wybrało prawidłową odpowiedź. 
W grupie pierwszej tylko cztery osoby wybrało pierwszą odpowiedź - dwa razy więcej osób wybrało tą opcję w grupie drugiej. 
Na podstawie rycin w grupie drugiej dziewięć osób uważało, że kandydat B zdobył *pomiędzy 20 a 30%* głosów, w pierwszej grupie było to 11 osób (Ryc. \@ref(fig:ryc54)). 
Czwarty wariant, czyli *40-50%*, wybrało pięć osób w pierwszej i osiem osób w drugiej grupie. 
Sześć osób z pierwszej oraz jedna osoba z drugiej grupy wywnioskowała, że kandydat B wygrał *ponad 50%* gmin w II turze wyborów.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc54} 

}

\caption{Wykres z wynikami do pytania drugiego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc54)
\end{figure}

### Pytanie trzecie {#pyt3}

**Pytanie: W ilu % gmin zaobserwowano wzrost frekwencji w II turze o co najmniej 5%?**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc55} 

}

\caption{Kartogram właściwy oraz kartogram geometryczny - wzrost frekwencji w II turze. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc55)
\end{figure}
**Poprawna odpowiedź: 21,6%**

Trzecie pytanie dotyczyło wzrostu frekwencji II turze (Ryc. \@ref(fig:ryc55)).
W grupie pierwszej ankietowani najczęściej uważali, że wzrost frekwencji dotyczył więcej niż 20% powiatów w Polsce (15 os.). 
Niewiele mniej, czyli 14 osób wybrało odpowiedź *15-20%*. Wariant trzeci, czyli *10-15%* wybrało osiem osób, a *5-10%* - 11 osób ankietowanych (Ryc. \@ref(fig:ryc56)).
Nikt w grupie pierwszej nie sądził, że wzrost frekwencji zaobserwowano w *mniej niż 5%* gmin.

W grupie drugiej tą samą opcję wybrała tylko jedna osoba, a sześć osób wybrało przedział *5-10%*. 
Wariant *10-15%* wybrało najwięcej ankietowanych, czyli 12 osób. 
11 osób zinterpretowało na mapie, że znaczny wzrost frekwencji zaobserwowano w *15-20%* gmin. 
Tylko cztery osoby najwyższą opcję, czyli *> 20%*.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc56} 

}

\caption{Wykres z wynikami do pytania trzeciego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc56)
\end{figure}

### Pytanie czwarte {#pyt4}

**Wymień 3 województwa z najwyższą frekwencją**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc57} 

}

\caption{Kartogram geometryczny oraz anamorfoza nieciągła - frekwencja w II turze. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc57)
\end{figure}
**Poprawna odpowiedź: woj. mazowieckie, woj. małopolskie, woj. pomorskie**

W pytaniu 4 ankietowani mieli za zadanie wymienić trzy województwa z najwyższą frekwencją (Ryc. \@ref(fig:ryc57)). 
W pierwszej grupie do wizualizacji został użyty kartogram geometryczny (heksagonalny), a w drugiej - anamorfoza nieciągła. 
Było to jedno z najtrudniejszych pytań dla ankietowanych, bowiem tylko 20,6% (siedem osób) w pierwszej grupie udało się na nie odpowiedzieć prawidłowo.
Najwięcej osób wybierało województwo mazowieckie oraz wielkopolskie jako te, które mają najwyższą frekwencję. 
W grupie drugiej nikomu nie udało się poprawnie odpowiedzieć na to pytanie - tylko siedem osób wybrało województwo małopolskie, a dziesięć osób województwo pomorskie (Ryc. \@ref(fig:ryc58)). 
Najczęstszą odpowiedzią drugiej grupy było *woj. mazowieckie, woj. pomorskie, woj. wielkopolskie*. 
W pierwszej grupie poza prawidłową odpowiedzią, popularna była również odpowiedź *woj. mazowieckie, woj. pomorskie, woj. śląskie* (sześć osób) oraz *woj. małopolskie, woj. mazowieckie, woj. zachodniopomorskie* (pięć osób).

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc58} 

}

\caption{Wykres z wynikami do pytania czwatego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc58)
\end{figure}

### Pytanie piąte {#pyt5}

**Pytanie: Jaki ogólnie % głosów kandydat A uzyskał w woj. wielkopolskim?**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc59} 

}

\caption{Anamorfoza ciągła oraz kartogram właściwy - poparcie dla kandydata A w I turze. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc59)
\end{figure}
**Poprawna odpowiedź: 37,8%**

W pytaniu 5 ankietowani mieli za zadanie oszacować odsetek głosów, które kandydat A uzyskał w województwie wielkopolskim (Ryc. \@ref(fig:ryc59)). 
W grupie pierwszej zastosowano anamorfozę ciągłą, a w grupie drugiej kartogram właściwy. 
Żadna z grup nie uważała, że poparcie było *mniejsze niż 35%*. Osiem osób uważało, że wynik wynosił *między 35 a 42%* - były to dwie osoby w grupie pierwszej oraz sześć w grupie drugiej (Ryc. \@ref(fig:ryc510)). 
Poprawną odpowiedź, czyli 37,8%, znajdowała się w zakresie, który wybrała połowa pierwszej grupy (17 osób) oraz dziewięć osób w grupie drugiej. 
W przedziale *40-50%* było za to odwrotnie - połowa grupy drugiej wybrała ten przedział, a z grupy pierwszej - 13 osób. 
Dwie osoby z każdej z grup uważało, że kandydat B uzyskał *ponad 50% głosów* w województwie wielkopolskim.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc510} 

}

\caption{Wykres z wynikami do pytania piątego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc510)
\end{figure}

### Pytanie szóste {#pyt6}

**Pytanie: O ile średnio % wzrosło poparcie dla kandydata B w II turze w porównaniu do I tury?**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc511} 

}

\caption{Kartogram geometryczny oraz anamorfoza ciągła - wzrost poparcia dla kandydata B w II turze. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc511)
\end{figure}
**Poprawna odpowiedź: 17,6%**

Na pytanie piąte udało się odpowiedzieć poprawnie obu grupom (Ryc. \@ref(fig:ryc511)). 
Ponad 50% grupy pierwszej (18 osób) oraz 12 osób z grupy drugiej poprawnie wywnioskowało, że poparcie kandydata B w II turze wzrosło o *mniej niż 20%* (Ryc. \@ref(fig:ryc512)). 
Dziewięć osób z każdej z grup wybrało odpowiedź, że poparcie wzrosło *między 20 a 40%*. 
Pięć osób z pierwszej grupy oraz dziesięć z drugiej grupy uważa, że odpowiedź *40-60%* była poprawna. 
Przedostatnią odpowiedź, wybrały dwie osoby z pierwszej oraz trzy osoby z drugiej grupy. 
Żadna z grup nie uważała, że poparcie wzrosło o *więcej niż 80%*.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc512} 

}

\caption{Wykres z wynikami do pytania szóstego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc512)
\end{figure}

### Pytanie siódme {#pyt7}

**Pytanie: Mapa przedstawia różnicę głosów między kandydatami w II turze. W którym z województw była najmniejsza różnica wyników?**
\begin{figure}[h]

{\centering \includegraphics[width=400px]{figures/ryc513} 

}

\caption{Anamorfoza nieciągła oraz anamorfoza ciągła - róznica głosów między kandydatami w II turze. Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc513)
\end{figure}
**Poprawna odpowiedź: woj. opolskie**

W ostatnim pytaniu zadaniem było wybranie województwa, w którym była najmniejsza różnica wyników w II turze (Ryc. \@ref(fig:ryc513)). 
W pierwszej grupie zastosowano anamorfozę nieciągłą, a w drugiej - anamorfozę ciągłą. 
W obu grupach największą liczbę głosów zdobyło *województwo opolskie* - zostałaona wybrana przez 11 osób z grupy pierwszej oraz dziewięć z grupy drugiej (Ryc. \@ref(fig:ryc514)). 
Drugim najczęściej wybieranym województwem było *województwo podkarpackie* - sześć osób w każdej z grup uważało, że ta odpowiedź jest poprawna. 
W grupie pierwszej *województwo mazowieckie* oraz *kujawsko-pomorskie* uzyskało po cztery głosy. 
Pięć osób z drugiej grupy wybrało *województwo zachodniopomorskie*, a następne pięć - *lubelskie*. 
Pozostałe województwa uzyskały od zera do trzech głosów.

\begin{figure}[h]

{\centering \includegraphics[width=300px]{figures/ryc514} 

}

\caption{Wykres z wynikami do pytania siódmego (obie grupy). Źródło: opracowanie własne na podstawie danych PKW}(\#fig:ryc514)
\end{figure}

## Wnioski {#wnioski}

Wnioski uzyskane z ankiety sugerują, że forma, w jakiej informacja jest przedstawiana, ma znaczny wpływ na odbiór informacji o rozmieszczeniu oraz zależności zjawisk przez użytkownika. 
Dotyczy to zarówno metody wizualizacji oraz pól odniesienia. 
Należy jednak pamiętać, że poprawność odczytywania informacji z map zależy również od doświadczenia oraz umiejętności odbiorców w zakresie interpretacji map.

Pytania, w których użyte były kartogramy właściwe pokazują, że pomimo swoich wad, jest najbardziej przystępną formą wizualizacji dla ankietowanych. 
W pytaniu 3 ta wizualizacja była bardziej czytelna od kartogramu heksagonalnego - zdecydowana większość głosów była skupiona w zakresie poprawnej odpowiedzi. 
Odpowiedzi do pytania 5 były mniej trafne, jednak równie skupione między dwoma wariantami bliskimi poprawnej odpowiedzi (37,8%). 
W obu przypadkach poprawne odpowiedzi były blisko granicy swojego przedziału, co miało wpływ na rozkład wyników.

Kartogram ciągły został użyty raz, w Pytaniu 1, gdzie większość ankietowanych nie była w stanie odpowiedzieć poprawnie. 
Bazując na tym wyniku oraz zasadzie kartograficznej, która nie zaleca używania więcej niż siedem lub osiem podobnych odcieni [@ratajski1989], można wyciągnąć wniosek, że używanie wielu gradacji jednej barwy dla dużej liczby jednostek odniesienia znacznie utrudnia użytkownikowi odczytanie prawidłowych informacji. 
Ludzkie oko nie jest w stanie rozróżnić oraz zidentyfikować tak wielu odcieni jednej barwy na mapie. 
Prostym rozwiązaniem byłoby zastosowanie kartogram właściwego oraz przedziałów klasowych.

W pytaniu, gdzie użyto kartogramu heksagonalnego dla gmin województwa wielkopolskiego, nie uzyskano jednoznacznej odpowiedzi u ankietowanych - 98% głosów zostało podzielonych między trzy odpowiedzi, w zakresie od *< 20%* do *40-50%*. 
Może to sugerować kilka wniosków. 
Po pierwsze, że mapa nie jest wystarczająco czytelna dla odbiorców. 
Po drugie, że zastosowanie takich samych pól odniesienia utrudnia ankietującym oszacowanie wyniku. 

W przypadku wizualizacji użytej w pytaniu 6 u grupy pierwszej, można zauważyć, że ponad połowa osób ankietowanych odpowiedziała poprawnie na to pytanie i wybrała pierwszą odpowiedź. 
Im większa różnica od poprawnej odpowiedzi, tym mniej osób ją wybierało. 
Może to sugerować, że jednorodność jednostek odniesienia jest pomocna w oszacowaniu proporcji.

Jednakowe jednostki odniesienia są kartogramów geometrycznych również wadą, co można zaobserwować w pytaniu 4 w grupie pierwszej. 
W zadaniu, którego celem było wskazanie trzech województw z najwyższą frekwencją, tylko 20,6% ankietowanych było w stanie poprawnie zlokalizować województwa. 
Należy zauważyć, że tylko trzy jednostki odniesienia należą do przedziału z najwyższymi wartościami. 
Można więc wyciągnąć wniosek, że najtrudniejszą częścią tego zadania było wskazanie konkretnych województw, co zostało w znacznym stopniu utrudnione właśnie przez użycie takiej samej geometrycznej dla wszystkich jednostek. 
Wiedza o tym, które z województw jest bardziej na wschód lub które są bardziej wewnątrz Polski (bliżej środkowego punktu Polski) mogą pomóc w ich zlokalizowaniu, jednak nie jest to wiedza, po którą użytkownik sięga odruchowo.

Podsumowując, kartogramy geometryczne sprawdzają się, jeśli odbiorca nie musi rozróżniać każdej z jednostek (tak jak w przypadku pytania 4). 
Takie rozwiązanie może być alternatywą dla technik, które używają niejednorodnych pól odniesienia. 
Dodatkowo wyniki pytań, w których użyte były kartogramy heksagonalne oraz kartogram kwadratowy tak jak powyższych przykładach potwierdzają, że różnice w kolorze między klasami jest istotnym czynnikiem w odbiorze mapy.

Anamorfoza ciągła na przykładzie ostatniego pytania wypada gorzej od anamorfozy nieciągłej, jednak w obu przypadkach udało się w znacznej mierze odpowiedzieć poprawnie. 
Wyniki również sugerują, że część ankietowanych nie przeczytała dokładnie pytania, bowiem sześć osób z każdej grup wybrało województwo, w którym była największa różnica liczby głosów (zadanie miało na celu wskazanie województwa z najmniejszą różnicą głosów - przypomina autorka). 
Być może znaczne zniekształcenie niektórych z województw utrudniło ankietowanym określenie ich rozmiaru wobec sąsiadujących jednostek. 
W zadaniu 6 anamorfoza ciągła dała gorsze wyniki w porównaniu z kartogramem geometrycznym, bowiem nie udało się uzyskać jednoznaczne poprawnej odpowiedzi. 
Warianty *< 20%, 20-40%* i *40-60%* różniły się między sobą jednym lub dwoma głosami. 
Całkowicie inaczej było w pytaniu 5, gdzie znaczna część ankietowanych wybrała poprawny zakres, w mniejszym stopniu ankietowani wybrali sąsiadujący zakres (poprawna odpowiedź wynosiła 37,8%, a przedziały dzieliły się na zakresy *30-40%* oraz *40-50%*, przez co można podejrzewać, że ta mniejsza część ankietowanych nieznacznie przeszacowała wynik). 
Wyniki sugerują te same wnioski przy pytaniu 1.

Najtrudniejsza w interpretacji użytkowników była wizualizacja anamorfozy nieciągłej w pytaniu 5 w grupie drugiej. 
Żadna z osób ankietowanych nie była w stanie odpowiedzieć poprawnie. 
Mogło to być związane z niewystarczającą znajomością województw lub brakiem wiedzy o mechanizmie działania anamorfoz nieciągłych. 
Dodatkowym utrudnieniem dla osób ankietowanych było zastosowanie odsetku frekwencji zamiast np. liczby ważnych głosów. 
Różnica między najmniejszym a największym odsetkiem frekwencji wynosiła tylko 13,9%. 
Skutkiem tego były mało wyraźne różnice między jednostkami.

W pytaniu 7 w grupie pierwszej również została użyta anamorfoza nieciągła, zastosowane jednak zostały wartości bezwzględne, a różnice wartości między każdym polem odniesienia wynosiły dziesiątki tysięcy - pozwoliło to na wyraźne zaznaczenie województw. 
Pomimo tego, tylko 30,6% osób wybrało prawidłową odpowiedź, a 17,6% wybrało *województwo podkarpackie*, które było jednostką z największą różnicą głosów. 
Sugeruje to, że część ankietowanych mogło źle zrozumieć pytanie, tak jak w przypadku anamorfozy ciągłej.

Z zadania, w którym został użyty kartodiagram Dorlinga wynika, że 23% ankietowanych odpowiedziało poprawnie i wybrało odpowiedź *30-40%*. 
Nie była to jednak najczęściej wybierana odpowiedź (jest to *20-30%* wybrane przez 11 os.). 
W tym pytaniu wyniki nie wykazały wyraźnie jednej dominującej odpowiedzi, każda miała podobną liczbę głosów. 
Opierając się o wyniki z pytania 2, kartodiagram Dorlinga okazuje się być nieadekwatny dla wizualizacji, w których zjawisko ma mały zakres wartości (np. odsetek frekwencji. Duże różnice między jednostkami umożliwiają nam na wyraźne zaznaczenie). 
Duża liczba pól podstawowych również utrudnia osobom zebranie i oszacowanie informacji z mapy. 
W przypadku, gdy mamy zmniejszą liczbę jednostek odniesienia oraz dane są przedstawiane w wartościach bezwzględnych, można łatwiej przekazać użytkownikowi informacje.

Biorąc pod uwagę wyniki ogółem, autorka śmie stwierdzić, że znaczna część ankietowanych w obu grupach nie potrafi odróżnić niektórych województw, np. pomorskiego i zachodniopomorskiego (Pytanie 4).

<!--chapter:end:05-roz5.Rmd-->


# Podsumowanie {#podsumowanie}

W niniejszej pracy podjęto próbę porównania różnych technik wizualizacji na przykładzie wyborów prezydenckich w Polsce. 
Określono, czym są wybory oraz przedstawiono historię map wyborczych na przykładzie map wyborów prezydenckich w Stanach Zjednoczonych oraz wyborach parlamentarnych w Wielkiej Brytanii. 
Omówiono również krótką historię map wyborczych w Polsce oraz jej przykłady. 
Następnie wskazano brak różnorodności w wizualizacjach tych map. 
Na podstawie literatury przedstawiono charakterystykę istniejących metod wizualizacji oraz ich przykłady. 
Opisano proces zbierania i opracowywania danych. 
Przedstawiono przykłady każdej badanej techniki wizualizacji na przykładzie jednostek administracyjnych Polski. 
Zanalizowane zostały również wyniki ankiet przeprowadzonych w ramach niniejszej pracy i oparto o nie wnioski.

W rozdziale 4 zaprezentowano każdą z badanych technik wizualizacji w kontekście odniesienia dla Polski oraz jej jednostek administracyjnych. 
Omówiono zalety oraz ograniczenia każdej z map oraz możliwe sposoby na optymalną reprezentację każdej z jednostek.

Najpopularniejsza technika wizualizacji danych wyborczych w kontekście przestrzennym należy do kartogramu właściwego. 
Często nie jest to jednak adekwatna metoda, ponieważ uwzględniona powierzchnia nie zawsze jest proporcjonalna do intensywności zjawiska. 
W celu znalezienia alternatywnej techniki wizualizacji, zbadano inne rodzaje kartogramów, m.in. kartogram ciągły, geometryczny oraz kartogramy odwrócone, tzw. anamorfozy. 
Badanie przeprowadzono w postaci ankiety - została ona udostępniona w dwóch wariantach 68 studentom trzeciego oraz czwartego roku Wydziału Nauk Geograficznych i Geologicznych UAM.

Wyniki ankiety pokazują, że ankietowani mieli problemy zarówno z szacowaniem odsetków prezentowanych zjawisk oraz wskazywaniem konkretnych województw. 
Na ich podstawie udało się jednak się jednak ustalić, kiedy techniki wizualizacji nie powinny być stosowane. 
Na podstawie wyników ankiety można stwierdzić, że kartogramy ciągłe nie są odpowiednie do prezentowania danych wyborczych. 
Zdaniem autorki podobne mogą wystąpić również w przypadku wizualizacji innych zjawisk, w szczególności społeczno-ekonomicznych.

Wyniki z map zawierających kartogramy geometryczne niewątpliwie pokazują, że taki rodzaj kartogramu nie powinien być używany, jeśli mamy na celu wyszczególnienie pojedynczych jednostek. 
Nie mamy możliwości, że odbiorca będzie w stanie dokładnie je zlokalizować pośród jednakowo wyglądających pól odniesienia. 
Kartogramy geometryczne mogą mieć jednak zastosowanie, kiedy chcemy, aby użytkownik był w stanie oszacować odsetek zjawiska ogółem, bez wskazywania pojedynczych jednostek lub jeśli dokładna lokalizacja każdej pojedynczej z jednostek nie jest ważnym elementem mapy (np. specyfika tego kartogramu niemożliwa jest umiejscowienie miasta Poznań wewnątrz powiatu poznańskiego).

Z odpowiedzi dla anamorfozy ciągłej na przykładzie powiatów wynika, że ankietowani nie byli w stanie dostatecznie doszacować wyniku. 
W obu przypadkach (Podozdziały \@ref(pyt1) oraz \@ref(pyt6)) wyniki były podobne do poprawnej odpowiedzi lub odsetek do większości odpowiedzi był podobny. 
Za to w podrozdziale \@ref(pyt5) połowa ankietowanych odpowiedziała poprawnie (odpowiedź *30-40%*), na sąsiedni wariant *40-50%* zagłosowało 38,2%. 
W przypadku tej techniki wizualizacji nie można wyciągnąć jednoznacznego wniosku w kwestii jej czytelności i sugerowana jest dalsza praca w tym temacie.

Wyniki jednoznacznie pokazują, że anamorfozy nieciągłe stanowią problem dla ankietowanych. 
W przypadku, kiedy różnice w wartościach są nieznaczne, mechanizm działania tej techniki czyni niemożliwym prawidłowe wybranie odpowiedzi bez wcześniejszego zaznajomienia się z nią. 
Jednak gdy użyte zostają dane, które znacznie różnią się od siebie, są one o wiele bardziej zrozumiałe dla odbiorcy (sugerowana jest różnica wartości na poziomie kilku, kilkunastu tysięcy. 
Zalecane są wartości bezwzględne, tak jak w podrozdziale \@ref(pyt7)).

Kartodiagram Dorlinga wydaje się być nieodpowiedni dla wizualizacji, gdzie mamy do czynienia z małą różnicą w wartościach oraz z dużą liczbą pól odniesienia. 
Wizualizacja, w której użyte jest wiele kół o podobnym rozmiarze utrudnia lub nawet uniemożliwia odczytanie informacji. 
Zalecane w tym przypadku jest zastosowanie danych w formie wartości bezwzględnych oraz z szerokim zakresem wartości.

Istotnym czynnikiem w analizie map jest również liczba kolorów oraz odcieni użytych do przedstawienia zmienności zjawiska. 
Ludzkie oko nie jest w stanie rozróżnić zbyt wielu odcieni jednego koloru na mapie, czego rezultatem może być niedoszacowanie intensywności zjawiska. 
Rozwiązaniem jest m.in. użycie kartogramu właściwego, który wykorzystuje skalę skokową.

Pomimo określenia szeregu prawidłowości wymienionych powyżej, warto jest także wykazać kilka sugestii do podobnych badań. 
Wśród tych sugestii szczególne znaczenie ma równe podzielenie technik wizualizacji w ankietach. 
Pozwoli to na lepsze analizowanie wyników oraz wyciąganie wniosków. 
Sugerowane jest również powtarzanie pytań przy jednoczesnym użyciu innych jednostek odniesienia lub/i technik wizualizacji. 
Informacje zwrotne od osób ankietowanych pozwoliłoby na rozstrzygnięcie hipotez dotyczących wyników. 




<!--chapter:end:06-roz6.Rmd-->

