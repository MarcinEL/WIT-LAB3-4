***

***

# Cyfrowa Technika Foniczna 2024Z

### **LABORATORIUM 3** | Próbkowanie, kwantyzacja i kształtowanie widma szumu rekwantyzacji

#### Niezbędne oprogramowanie i sprzęt.
Przed przystąpieniem do wykonania ćwiczenia laboratoryjnego należy **pobrać i zainstalować** darmowe [oprogramowanie do wizualizcji, analizy i edycji plików dźwiękowych](https://www.sonicvisualiser.org/) w sekcji "Download" i dalej zgodnie z używanym system operacyjnym. Zalecane jest, aby odsłuchiwanie próbek dźwiękowych odbywało się za pomocą **słuchawek nausznych lub dousznych** (niezalecany jest odsłuch za pomocą wbudowanych lub zewnętrznych głośników komputerowych).

### Sprawozdania

Plik lub pliki ze sprawozdaniem (w dowolnym formacie: *.rtf, *.doc, *.docx, *.pdf, Markdown, LaTex) należy umieszczać w repozytorium [GitHub](https://github.com/). Po zalogowaniu się do systemu każdy powinien utworzyć nowe repozytorium o nazwie <CTF2024Z_SPR> i tam umieścić plik/pliki ze sprawozdaniem.

### Pliki dźwiękowe

Wszystkie niezbędne do wykonania ćwiczenia pliki dźwiękowe znajdują się w folderze `./Samples` w repozytorium.

***

***

### `Zadanie 1. Próbkowanie`

#### Teoria
> **Sygnał analogowy** jest sygnałem ciągłym w dziedzinie czasu i amplitudy. W celu przetworzenia takiego sygnału na **sygnał cyfrowy** najpierw należy dokonać próbkowania, czyli zamiany sygnału na sygnał dyskretny w czasie, a następnie kwantyzacji i kodowania tak, aby amplituda sygnału również była zmienną dyskretną.
> 
> Sygnał analogowy dźwiękowy jest zawsze próbkowany w stałych odstępach czasu (ze stałą częstotliwością próbkowania), co z matematycznego punktu widzenia oznacza mnożenie sygnału analogowego z ciągiem impulsów o określonym czasie trwania. Jest to tożsame ze splotem widm sygnałów w dziedzinie częstotliwości.
> 
> **Teoria o próbkowaniu** zakłada, że aby poprawnie zrekonstruować sygnał cyfrowy to sygnał analogowy musi być próbkowany przynajmniej z podwójną maksymalną częstotliwością występującą w sygnale. Można to wyjaśnić w dziedzinie czasu i częstotliwości:
> 
> - **W dziedzinie czasu** sygnał sinusoidalny może być w pełni określony cyfrowo za pomocą tylko dwóch punktów, co oznacza, że występuje tylko jeden sygnał sinusoidalny o częstotliwości mniejszej od połowy częstotliwości próbkowania, którego jeden okres przechodzi dokładnie przez te dwa punkty. Jest to oczywiście prawdą tylko wtedy, kiedy sygnałem próbkowanym jest sygnał sinusoidalny bez składowych harmonicznych, co oznacza, że pełna rekonstrukcja sygnału cyfrowego jest możliwa, gdy pasmo sygnału jest ograniczone do takiej częstotliwości, która określa jeden jego okres w dwóch punktach (sygnał sinusoidalny, którego jeden okres jest określony w dwóch punktach ma częstotliwość połowy częstotliwości próbkowania).
> - **W dziedzinie częstotliwości** w procesie próbkowania widmo sygnału próbkowanego jest powielane symetrycznie wokół wielokrotności częstotliwości próbkowania. Takie mnożenie ciągu impulsów próbkujących z sygnałem próbkowanym jest znane również jako modulacja PAM (*Pulse Amplitude Modulation*). W trakcie procesu próbkowania widmo ciągu impulsów próbkujących charakteryzującego się podstawową częstotliwością równą częstotliwości próbkowania i czasem trwania impulsu na tyle małym żeby zminimalizować błędy apertury jest splatane z widmem sygnału wejściowego. Oznacza to, że widmo sygnału wejściowego jest powielane na wielokrotnościach częstotliwości próbkowania. W celu rekonstrukcji takiego sygnału w przetworniku c/a należy odseparować od siebie część widma w paśmie podstawowym oraz powieleń tego widma. Jako, że pierwsze powielenie widma jest przesuniętym i lustrzanym odbiciem widma z pasma podstawowego na częstotliwości próbkowania to próbkowanie powinno odbywać się właśnie przynajmniej z podwójną częstotliwością pasma sygnału próbkowanego. 
> 
> Jeżeli sygnał analogowy nie jest próbkowany przynajmniej dwa razy szybciej niż wynika to z pasma sygnału próbkowanego lub odwrotnie - jeżeli sygnał wejściowy ma składowe częstotliwościowe większe niż wartość połowy częstotliwości próbkowania to widmo sygnału w paśmie podstawowym i przesunięte oraz lustrzane odbicia widma zachodzą na siebie. Po konwersji takiego sygnału z powrotem do sygnału analogowego będą słyszalne dodatkowe komponenty częstotliwościowe, które nie występowały w sygnale oryginalnym. Zjawisko to jest nazywane **aliasingiem**. W celu uniknięcia problemu aliasingu na wejściu przetwornika a/c stosuje się analogowy filtr antyaliasingowy, który ogranicza pasmo sygnału wejściowego do połowy częstotliwości próbkowania. Na wyjściu przetwornika c/a natomiast stosuje się filtr antylustrzany (rekonstruujący), który ma za zadanie stłumić zniekształcenia wynikające z działania praktycznego (nie idealnego) układu próbkująco-pamiętającego (wprowadzającego zniekształcenia typu sin(x)/x).

#### Polecenia
1. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [Oscillator_2_4_8_16kHz_PitchUp_and_PitchDown_Fs44100Hz.wav](/Samples/Oscillator_2_4_8_16kHz_PitchUp_and_PitchDown_Fs44100Hz.wav)*. Kółkiem myszy można zbliżać i oddalać widok w czasie, a przytrzymując lewy klawisz myszy i przesuwając w lewo i prawo można nawigować widokiem wczytanego sygnału. W panelu po prawej stronie można zmienić kolor zobrazowania próbek sygnału (karta nr 3 - `Waveform`).
2. Zobrazowanie widma sygnału proszę uruchomić dodając kolejny panel za pomocą polecenia `Pane -> Add Spectrum`. W panelu po prawej stronie w karcie nr 2 można zmienić parametry analizy widmowej (`Colour` - kolor, `Bins` - skala częstotliwościowa i sposób prezentacji wykresu, `Scale` - skala amplitudowa, `Window` - szerokość okna analizy, nakładanie się okien, nadpróbkowanie). Polecane ustawienia, jeśli są inne: skala logarytmiczna w częstotliwości i amplitudzie, okno analizy 4096, nakładanie 50%, zmiana kształtu okna -> `File -> Preferences... -> Analysis -> Spectral analysis window shape: Nutall`.
3. Dodatkowo zobrazowanie widma w czasie (spektrogram) proszę uruchomić w kolejnym panelu za pomocą polecenia `Pane -> Add Spectrogram`. W panelu po prawej stronie w karcie nr 3 proszę zmienić, jeśli ustawienia są inne, skala mocy dBV^2, szerokość okna analizy 2048 i nakładanie 50%.
4. Proszę odsłuchać plik dźwiękowy od początku do końca analizując zobrazowanie widma i korelując wrażenia słuchowe z tym, co można zauważyć na widmie.
5. W **sprawozdaniu** proszę zapisać wnioski i opisać zaobserwowane zjawisko.

    **plik dźwiękowy to suma sygnałów sinusoidalnych o częstotliwościach początkowych 2kHz, 4kHz, 8kHz i 16kHz o zmiennej liniowo wysokości dla wszystkich tonów w czasie (o 4 oktawy do góry - częstotliwości x2 dla każdej oktawy i później 4 oktawy w dół), częstotliwość próbkowania sygnału 44100Hz, rozdzielczość bitowa 32b (float).*
    
6. W oprogramowaniu Sonic Visualiser proszę utworzyć nową sesję (`File -> New Session`), otworzyć plik [Original_piano.wav](/Samples/Original_piano.wav), a następnie wczytać dwa kolejne pliki (`File -> Import More Audio...`), a mianowicie [Original_piano_sampled_at8kHz_sample1.wav](/Samples/Original_piano_sampled_at8kHz_sample1.wav) oraz [Original_piano_sampled_at8kHz_sample2.wav](/Samples/Original_piano_sampled_at8kHz_sample2.wav). W trakcie odsłuchiwania można zmieniać aktualnie odwtarzany plik włączając opcję `Playback -> Solo Current Pane` i klikając na panel z plikiem, który w danym momencie chcemy odsłuchiwać.
7. W **sprawozdaniu** proszę opisać czym różnią się pliki [Original_piano_sampled_at8kHz_sample1.wav](/Samples/Original_piano_sampled_at8kHz_sample1.wav) oraz [Original_piano_sampled_at8kHz_sample2.wav](/Samples/Original_piano_sampled_at8kHz_sample2.wav) i z czego może wynikać różnica brzmienia w porównaniu z oryginalną ścieżką [Original_piano.wav](/Samples/Original_piano.wav). Do analizy można wykorzystać zobrazowanie widma (jak w poprzednich punktach), jako oddzielne panele ALBO można nałożyć na siebie kilka wizualizacji za pomocą polecenia `Layer -> Add Spectrum` / `Layer -> Add Spectrogram`.

***

### `Zadanie 2. Kwantyzacja`

#### Teoria

> Kwantyzacja jest procesem przypisywania nieskończonej liczby amplitud sygnału analogowego do najbliższej wartości amplitudy ze skończonego zbioru dostępnych wartości (determinowanych rozdzielczością bitową docelowego sygnału cyfrowego). W przypadku operacji próbkowania, gdy spełni się założenia twierdzenia o próbkowaniu to sygnał próbkowany może być zrekonstruowany bez błędów (poza błędami wynikającymi z ograniczeń sprzętowych). W przypadku kwantyzacji - zawsze popełniany jest błąd. W zależności od dostępnej rozdzielczości bitowej, błąd kwantyzacji określa dynamikę sygnału i upraszczając pewne zależności można wykazać, że wynikowa wartość SNR sygnału po kwantyzacji jest równa
> 
> $`SNR = 6.02 dB \cdot liczbaBitów + 1.76 dB`$. 
> 
> Błąd kwantyzacji zawsze jest pewną funkcją sygnału wejściowego podawanego do kwantyzatora, a jego parametry zależą od parametrów tego sygnału, co oznacza, że nie można zakładać pełnej dekorelacji błędu kwantyzacji z sygnałem wejściowym. Zakres zmian błędu kwantyzacji może być wyrażony jako $`\pm 0.5 LSB`$. W przypadku, gdy istnieje korelacja błędu kwantyzacji z sygnałem wejściowym podawanym do kwantyzatora to można mówić o zniekształceniach błędu kwantyzacji, a nie o szumie kwantyzacji. Zniekształcenia są najbardziej wyraźne dla małych amplitud sygnału wejściowego, a mniejsze dla większych amplitud. Inaczej mówiąc proces kwantyzacji wprowadza do sygnału zniekształcenia (błędy zależne od sygnału wejściowego o charakterze harmonicznym i intermodulacyjne) oraz modulację szumu. Jak powiedziano wcześniej, błędy te są tym bardziej szkodliwe, im poziom sygnału jest bliższy pojedynczym krokom kwantyzacji.
> 
> Istnieją dwa podstawowe typy kwantyzatorów wykorzystywanych w przetwarzaniu dźwięku - kwantyzator tzw. *mid-tread* oraz *mid-rise*, których charakterystyki dla przypomnienia są zamieszczone poniżej. W technice audio najczęściej jest wykorzystywany kwantyzator typu *mid-tread*.
> 
> <img src="/img/midtread_midrise.jpg" width="800"/>
> 
> W literaturze przyjęto, że błąd kwantyzacji $`e`$ można traktować i analizować jako addytywne do sygnału wejściowego $`u`$ źródło szumu białego, a jego parametry traktować jako niezależne (nieskorelowane) z parametrami sygnału wejściowego. To założenie jest nazywane tzw. modelem liniowym (klasycznym) kwantyzatora i charakteryzuje się ono trzema właściwościami:
> - Błąd $`e`$ jest statystycznie niezależny od sygnału wejściowego $`u`$. Ta właściwość pozwala trakować kwantyzator jako system liniowy, co upraszcza analizę i zakłada, że widmo sygnału po kwantyzacji jest złożeniem widma sygnału wejściowego i szumu białego.
> - Błąd $`e`$ ma równomierny rozkład prawdopodobieństwa w zakresie [$`-\Delta/2`$, $`+\Delta/2`$]. Ta właściwość pozwala na oszacowanie mocy szumu jako prostego całkowania rozkładu równomiernego w zakresie [$`-\Delta/2`$, $`+\Delta/2`$] i stałej gęstości p-stwa równej $`1/\Delta`$, co daje w wyniku wartość $`\Delta^{2}/12`$.
> - Błąd $`e`$ jest szumem białym o stacjonarnych parametrach w czasie i równomiernej mocy w całym paśmie. Oznacza to brak jakichkolwiek korelacji z sygnałem wejściowym.
> 
> Kwantyzator może charakteryzować się powyższymi właściwościami tylko wtedy, kiedy spełnione są cztery warunki:
> - Sygnał wejściowy $`u`$ ma poziom zapewniający pracę kwantyzatora bez jego przesterowania.
> - Sygnał wejściowy $`u`$ ma wygładzoną funkcję rozkładu prawdopodobieństwa.
> - Liczba kroków kwantyzacji jest dostatecznie duża.
> - Krok kwantyzacji jest dostetecznie mały.
> 
> W praktyce spełnienie tych warunków dla sygnałów muzycznych i mowy nie zawsze jest możliwe, a wzajemne korelacje między błędem $`e`$ i sygnałem wejściowym $`u`$ rosną tym bardziej, im mniej jest kroków kwantyzacji (mniejsza rozdzielczość) i są one większe względem parametrów sygnału wejściowego.


#### Polecenia
1. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [quantization_sinus_mono_loweringBitDepth.wav](/Samples/quantization_sinus_mono_loweringBitDepth.wav). Proszę dokonać analizy w dziedzinie czasu (przybliżenie w czasie umożliwiające obserwację przebiegu czasowego próbek) oraz dziedzinie częstotliwości (zobrazowanie widma `Pane -> Spectrum`) i widma w czasie (`Pane -> Spectrogram`) z domyślnymi ustawieniami. Plik dźwiękowy rozpoczyna się od sygnału skwantowanego do 16 bitów i co pewien czas rozdzielczość bitowa jest zmniejszana o 1 bit, aż do docelowej. Następnie rozdzielczość jest ponownie zwiększana aż do 24 bitów.
2. W **sprawozdaniu** proszę zapisać, w której sekundzie trwania pliku dźwiękowego kwantyzacja jest 3 bitowa, w jaki sposób to określono oraz w jaki sposób objawia się błąd kwantyzacji w dziedzinie częstotliwości, czasu i wrażeniowo podczas odsłuchiwania?
2. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [Piano_16b_to_2b_to_16b_quantizer1.wav](/Samples/Piano_16b_to_2b_to_16b_quantizer1.wav). Proszę dokonać analizy podobnej jak w punkcie 1. Plik jest skonstruowany tak, że oryginalne nagranie partii fortepianu jest skwantowane do 16 bitów, następnie rozdzielczość kwantyzatora jest zmniejszana do 2 bitów i ponownie zwiększana do 16 bitów. 
3. W **sprawozdaniu** proszę określić, jakiego rodzaju kwantyzator został wykorzystany w przygotowaniu próbki dźwiękowej (mid-tread czy mid-rise?).
4. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [Piano_16b_to_2b_to_16b_quantizer2.wav](/Samples/Piano_16b_to_2b_to_16b_quantizer2.wav). Proszę dokonać analizy podobnej jak w punkcie 1. Plik jest skonstruowany tak, że oryginalne nagranie partii fortepianu jest skwantowane do 16 bitów, następnie rozdzielczość kwantyzatora jest zmniejszana do 2 bitów i ponownie zwiększana do 16 bitów.
5. W **sprawozdaniu** proszę określić, jakiego rodzaju kwantyzator został wykorzystany w przygotowaniu próbki dźwiękowej (mid-tread czy mid-rise?).
6. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [quantization_music_1_8bit_fade_error_compensated.wav](/Samples/quantization_music_1_8bit_fade_error_compensated.wav). Proszę dokonać analizy podobnej jak w punkcie 1. Plik jest skonstruowany tak, że oryginalne nagranie muzyki jest skwantowane do 8 bitów i w miarę trwania utworu jest zmniejszany poziom sygnału przed kwantyzatorem (docelowo do -28dB) i jednocześnie za kwantyzatorem poziom sygnału jest kompensowany tak, aby było wyraźnie słychać błąd kwantyzacji na tle sygnału oryginalnego.
7. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [quantization_music_2_8bit_fade_error_compensated.wav](/Samples/quantization_music_2_8bit_fade_error_compensated.wav). Proszę dokonać analizy podobnej jak w punkcie 1. Plik jest skonstruowany tak, że oryginalne nagranie muzyki jest skwantowane do 8 bitów i w miarę trwania utworu jest zmniejszany poziom sygnału przed kwantyzatorem (docelowo do -28dB) i jednocześnie za kwantyzatorem poziom sygnału jest kompensowany tak, aby było wyraźnie słychać błąd kwantyzacji na tle sygnału oryginalnego.
8. W **sprawozdaniu** proszę opisać wrażenia słuchowe oraz wnioski dot. tego czy błąd kwantyzacji może być traktowany jako addytywny i niezależny od sygnału wejściowego o parametrach niezmiennych w czasie.
9. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [quantization_music_3_8bit_to_16b_downto_3_andback_to_24b.wav](/Samples/quantization_music_3_8bit_to_16b_downto_3_andback_to_24b.wav). Proszę dokonać analizy podobnej jak w punkcie 1. Plik jest skonstruowany tak, że oryginalne nagranie muzyki jest skwantowane do 8 bitów, od pewnego momentu w czasie kwatyzator jest ustawiony od 16 bitów i rozdzielczość jest zmniejszana do 3 bitów. Następnia rozdzielczość jest zmieniana do 24 bitów.
10. W **sprawozdaniu** proszę opisać wrażenia słuchowe oraz wnioski dot. tego czy błąd kwantyzacji może być traktowany jako addytywny i niezależny od sygnału wejściowego o parametrach niezmiennych w czasie. Proszę również wyjaśnić skąd bierze się dodatkowa informacja wysokoczęstotliwościowa, której w pewnych momentach w czasie nie ma w sygnale oryginalnym.

***

### `Zadanie 3. Dithering i kształtowanie szumu rekwantyzacji`

### Teoria

> Jak wspomniano wcześniej działanie kwantyzatora dla sygnałów dźwiękowych nie może być traktowane jako proces liniowy bez daleko idących założeń, które nie są prawdziwe w określonych warunkach. Błąd kwantyzacji zawsze jest w większym lub mniejszym stopniu zależny od parametrów sygnału wejściowego, co jest słyszalne przez człowieka jako nieprzyjemne zniekształcenia harmoniczne czy błędy modulacyjne, a ogólniej - pogorszenie jakości odbieranego dźwięku.
> 
> W celu dekorelacji parametrów błędu kwantyzacji z parametrami sygnału kwantowanego stosuje się sygnał tzw. dither'a. Dither jest sygnałem losowym dodawanym do sygnału fonicznego w celu poprawy liniowości amplitudowej charakterystyki przejściowej układów do przetwarzania analogowo-cyfrowego i rekwantyzacji sygnału cyfrowego. Stosowanie dither’a pozwala zredukować poziom zniekształceń harmonicznych w widmie skwantowanego sygnału i zmniejszenia modulacji progu szumowego, kosztem pogorszenia stosunku sygnału do szumu. Dither może być sygnałem zarówno analogowym (dodawanym do sygnału fonicznego przed próbkowaniem) lub cyfrowym (dodawanym do cyfrowego sygnału fonicznego przy zmianie poziomu kwantyzacji lub przy przetwarzaniu sygnału cyfrowego na sygnał analogowy).
> 
> Dodanie pewnej wartości losowego sygnału szumu sprawia, że kwantyzator zaczyna zachowywać się również w pewien sposób losowo (sygnał kwantowany, które amplituda znajduje się między poziomami kwantowania będzie losowo przyjmował wartość wyższego lub niższego progu rozpraszając tym samym popełniany błąd). Patrząc na charakterystykę wejściowo-wyjściową (statyczną) kwantyzatora z zastosowaniem techniki dither'ingu można uzyskać po uśrednieniu liniową charakterystykę. Na obrazku poniżej jest przedstawiona charakterystyka kwantyzatora z sygnałem dither'a o prostokątnej (równomiernej) funkcji rozkładu prawdopodobieństwa.
> 
> <img src="/img/ditherRPDF_transfer_function.jpg" width="600"/>
> 
> Taki rodzaj sygnału dither'a dodany do sygnału wejściowego kwantyzatora skutecznie dekoreluje pewne parametry błędu kwantyzacji z sygnałem, a konkretnie jego wartość średnią. Nie eliminuje jednak problemu modulacji szumu (wariancja błędu nadal jest skorelowana z parametrami sygnału wejściowego i powoduje słyszalne pogorszenie jakości dźwięku). Skuteczna eliminacja modulacji szumu spowodowanej błędami kwantyzacji może być uzyskana za pomocą innej funkcji rozkładu p-stwa sygnału dither'a, a mianowicie rozkładu trójkątnego (złożenia ze sobą dwóch rozkładów równomiernych). Dodatkowo, oprócz odpowiednio dobranej funkcji rozkładu p-stwa sygnału dither'a należy jeszcze odpowiednio dobrać jego amplitudę żeby skutecznie uniezależnić statystycznie błąd kwantyzacji od parametrów sygnału wejściowego (patrz rysunki poniżej).
> 
> | <img src="/img/ditherRPDF_TPDF_1.jpg" width="500"/> | <img src="/img/ditherRPDF_TPDF_2.jpg" width="500"/> |

> Widmo mocy błędu kwantyzacji powstającego w procesie kwantowania z oraz bez udziału sygnału dither'a jest rozłożone równomiernie w całym paśmie fonicznym. W celu dodatkowego tłumienia błędów w paśmie wykorzystywane są proste algorytmy układów kształtowania widma błędów (rysunek poniżej).
> 
> <img src="/img/noise_shaper.jpg" width="600"/>
> 
> Funkcja $`H(z)`$ może mieć różne charakterystyki filtracji sygnału błędu zaczynając od prostego filtru 1-szego rzędu, a kończąc na specjalnych filtrach o charakterystykach ważonych tak, aby tłumione były fragmenty pasma fonicznego, w którym ludzkie ucho wykazuje największą czułość.

#### Polecenia
1. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [quantization_sinus_dth_noiseShaping_mono.wav](/Samples/quantization_sinus_dth_noiseShaping_mono.wav). Proszę dokonać analizy w dziedzinie czasu (przybliżenie w czasie umożliwiające obserwację przebiegu czasowego próbek) oraz dziedzinie częstotliwości (zobrazowanie widma `Pane -> Spectrum`) i widma w czasie (`Pane -> Spectrogram`) z domyślnymi ustawieniami. Plik dźwiękowy rozpoczyna się od sygnału skwantowanego do 8 bitów i w miarę trwania jest zmniejszany poziom sygnału przed kwantyzatorem (docelowo do -28dB) i jednocześnie za kwantyzatorem poziom sygnału jest kompensowany tak, aby było wyraźnie słychać błąd kwantyzacji na tle sygnału oryginalnego. Następnie włączany jest pierwszy typ sygnału dither'a, potem kolejny, a następnie zostawiony zostaje dither pierwszy, a zmianie ulegają ustawienia kształtowania błędów kwantyzacji - najpierw jest to ustawienie łagodnego kształtowania, potem większego i na końcu błąd kwantyzacji jest kształtowany za pomocą najbardziej stromego filtru $`H(z)`$.
2. W **sprawozdaniu** proszę zapisać wnioski i obserwacje dotyczące tego, co zmienia się w sygnale w trakcie dodawania różnych rodzajów sygnału dither'a oraz różnych ustawień 
kształtowania błędu kwantyzacji.
3. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [sinus_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav](/Samples/sinus_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav). Proszę dokonać analizy jak w punkcie 1. Plik dźwiękowy zawiera sygnał sinusoidalny o czętotliwości 300Hz skwantowany do 8 bitów z wykorzystaniem dither'a o równomiernym rozkładzie RPDF i amplitudzie zmienianej od 0 do 1LSB i z powrotem do 0. Dla lepszego zobrazowania efektu plik dźwiękowy [error_sinus_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav](/Samples/error_sinus_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav) zawiera tylko sygnał błędu kwantyzacji.
4. W **sprawozdaniu** proszę zapisać wnioski i obserwacje dotyczące tego przy jakiej amplitudzie sygnału dither'a można zauważyć skuteczną eliminację zniekształceń harmonicznych.
5. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [piano_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav](/Samples/piano_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav). Proszę dokonać analizy jak w punkcie 1. Plik dźwiękowy zawiera nagranie fortepianu skwantowane do 8 bitów z wykorzystaniem dither'a o równomiernym rozkładzie RPDF i amplitudzie zmienianej od 0 do 1LSB i z powrotem do 0. Dla lepszego zobrazowania efektu plik dźwiękowy [error_piano_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav](/Samples/error_piano_8bit_9LSBp-p_RPDF_0_to_1LSB_to_0.wav) zawiera tylko sygnał błędu kwantyzacji.
6. W **sprawozdaniu** proszę zapisać wnioski i obserwacje dotyczące tego przy jakiej amplitudzie sygnału dither'a można zauważyć skuteczną eliminację zniekształceń harmonicznych w przypadku sygnału muzycznego.
7. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [piano_faded_8bit_RPDF1LSB_rampDCoffset_changing.wav](/Samples/piano_faded_8bit_RPDF1LSB_rampDCoffset_changing.wav). Proszę dokonać analizy jak w punkcie 1. Plik dźwiękowy zawiera nagranie fortepianu skwantowane do 8 bitów z wykorzystaniem dither'a o równomiernym rozkładzie RPDF i amplitudzie 1LSB. Dodatkowo do sygnału jest dodany sygnał wolnozmienny trójkątny o zmiennej amplitudzie od 0 do +1 z okresem 2 sekund. Dla lepszego zobrazowania efektu plik dźwiękowy [error_piano_faded_8bit_RPDF1LSB_rampDCoffset_changing.wav](/Samples/error_piano_faded_8bit_RPDF1LSB_rampDCoffset_changing.wav) zawiera tylko sygnał błędu kwantyzacji.
8. W **sprawozdaniu** proszę zapisać wnioski i obserwacje.
9. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [piano_faded_8bit_TPDF1LSB_rampDCoffset_changing.wav](/Samples/piano_faded_8bit_TPDF1LSB_rampDCoffset_changing.wav). Proszę dokonać analizy jak w punkcie 1. Plik dźwiękowy zawiera nagranie fortepianu skwantowane do 8 bitów z wykorzystaniem dither'a o trójkątnym rozkładzie TPDF i amplitudzie 2LSB. Dodatkowo do sygnału jest dodany sygnał wolnozmienny trójkątny o zmiennej amplitudzie od 0 do +1 z okresem 2 sekund. Dla lepszego zobrazowania efektu plik dźwiękowy [error_piano_faded_8bit_TPDF1LSB_rampDCoffset_changing.wav](/Samples/error_piano_faded_8bit_TPDF1LSB_rampDCoffset_changing.wav) zawiera tylko sygnał błędu kwantyzacji.
10. W **sprawozdaniu** proszę zapisać wnioski i obserwacje. Czy inny rodzaj dither'a skutecznie eliminuje błędy modulacji szumu?
11. Uruchom oprogramowanie Sonic Visualiser i wczytaj plik [noise_shaping_floor.wav](/Samples/noise_shaping_floor.wav). Proszę dokonać analizy jak w punkcie 1. Plik dźwiękowy zawiera cyfrową ciszę zapisaną na 8 bitach w 5-sekundowych blokach, z których w kolejności: dither TPDF 2LSB, filtrowany górnoprzepustowo dither TPDF 2LSB, dither TPDF 2LSB kształtowany filtrem 1-szego rzędu i dither TPDF 2LSB kształtowany funkcją 9-tego rzędu ważoną charakterystykiami odwrotnymi do krzywych izofonicznych. Taka sekwencja jest powtórzona 2 razy. 
12. W **sprawozdaniu** proszę zapisać wnioski i obserwacje.

***

### `Zadanie 4. Jitter i błędy synchronizacji zegarów`

### Teoria

> Sygnał analogowy w przetworniku a/c jest przetwarzany na sygnał cyfrowy poprzez pomiar amplitudy w stałych odstępach czasu i w takich samych odstępach czasu w przetworniku c/a sygnał cyfrowy jest przetwarzany na poziom napięcia lub prądu. Założenie prawidłowego działania systemu przetwarzania jest takie, że odległość między impulsami ciagu próbkującego w przetworniku a/c i odwtarzającego próbki w przetworniku c/a jest stała i niezmienna w czasie.
> 
> <img src="/img/jitter1.jpg" width="500"/>
> 
> Jednak w rzeczywistych warunkach układy generacji sygnałów zegarowych nie są idealne, połączenia urządzeń mogą wprowadzać dodatkowe zakłócenia, a układy synchronizacji zegarowej między urządzeniami również mogą prowadzić do rozchwiania momentów próbkowania. Nieregularność taktowania zegara próbkującego w przetworniku a/c i odwtarzającego w przetworniku c/a jest nazywana jitter'em sygnału zegarowego. Podsumowując istnienie jitter'a może być związane również z następującymi czynnikami:
> - Niestabilnością częstotliwości sygnału taktującego zegara.
> - Niesynchroniczną pracą urządzeń.
> - Zmiennym czasem opadania/narastania sygnału taktującego.
> - Modulacją amplitudy sygnału taktującego przez sygnał foniczny, zakłócenia napięcia zasilania lub sieci energetycznej, itp.
> 
> Należy również zauważyć, że błędy spowowodowane jitter'em są tym większe, im większa jest amplituda sygnału oraz większa jest jego częstotliwość (rysunek poniżej).
> 
> <img src="/img/jitter2.jpg" width="800"/>
> 
> Pogorszenie jakości sygnału dźwiękowego związanego z jitter'em jest zatem zależna od zawartości częstotliwościowej sygnału, jego amplitudy oraz widma i poziomu błędu jitter'a. Jitter można traktować jako modulację, gdzie sygnałem modulowanym jest sygnał dźwiękowy, a modulującym - sygnał jitter'a. Zniekształcenia mają więc charakter dodatkowych komponentów harmonicznych w widmie sygnału dźwiękowego (w przypadku jitter'a o charakterze okresowym) oraz podniesienia poziomu szumu (w przypadku jitter'a o charakterze losowym).
> 
> Błędy synchronizacji zegarów są problem jeżeli zachodzi potrzeba przesyłania cyfrowego sygnału dźwiękowego między urządzeniami ze względu na to, że urządzenia te muszą pracować synchronicznie. Oznacza to, że albo urządzenia są zsynchronizowane z tym samym źródłem sygnału zegarowego albo jedno z urządzeń jest zsynchronizowane do zegara drugiego urządzenia. Jeżeli urządzenia nie pracują synchronicznie to wzajemne relacje czasowe sygnałów zegarowych mogą w pewnych momentach być na tyle różne, że niektóre próbki dźwiękowe nie będą poprawnie przesłane i nie zostanie zachowana ciągłość sygnału. Będzie to skutkowało słyszalnymi kliknięciami dźwięku na wyjściu przetwornika c/a, a jest to najbardziej słyszalne dla wyższych częstotliwości, gdzie próbek na okres przypada mało i strata jednej próbki (nawet raz na sekundę) powoduje słyszalne zniekształcenie.


### Polecenia

1. Uruchom oprogramowanie Sonic Visualiser i wczytaj pliki [jitter1.wav](/Samples/jitter1.wav), [jitter2.wav](/Samples/jitter2.wav) i [jitter3.wav](/Samples/jitter3.wav). Pliki dźwiękowe to zarejestrowane sinusoidy (o częstotliwości 13kHz) za pomocą przetwornika a/c, w którym zegar taktujący został zmodulowany sygnałem prostokątnym o częstotliwości 8kHz (jitter1), sygnałem szumowym (jitter2) oraz sygnałem o niskiej częstotliwości (jitter3). Sygnał sinusoidy 13kHz został stłumiony tak, aby lepiej były słyszalne zniekształcenia.
2. W **sprawozdaniu** proszę zapisać wnioski i obserwacje.
3. Uruchom oprogramowanie Sonic Visualiser i wczytaj pliki [jitter4.wav](/Samples/jitter4.wav) - oryginał bez jitter'a, [jitter5.wav](/Samples/jitter5.wav), [jitter6.wav](/Samples/jitter6.wav) i  [jitter7.wav](/Samples/jitter7.wav). Pliki dźwiękowe to sygnał fletu zarejestrowany za pomocą przetwornika a/c, w którym zegar taktujący został zmodulowany tak samo jak w poprzednim punkcie.
4. W **sprawozdaniu** proszę zapisać wnioski i obserwacje.
5. Uruchom oprogramowanie Sonic Visualiser i wczytaj pliki [sync1.wav](/Samples/sync1.wav), [sync2.wav](/Samples/sync2.wav) i [sync3.wav](/Samples/sync3.wav). Pliki dźwiękowe to sinusoidy (o częstotliwości 19kHz i 13kHz) przetworzone za pomocą konsoli mikserskiej bez synchronizacji z zegarem przetwornika a/c oraz sygnał nagranego fletu. Sygnały sinusoidy zostały stłumione tak, aby lepiej były słyszalne zniekształcenia.
6. W **sprawozdaniu** proszę zapisać wnioski i obserwacje. W przypadku której sinusoidy zniekształcenia są bardziej słyszalne i dlaczego?
