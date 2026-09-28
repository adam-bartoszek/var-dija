Porównanie metod szacowania Value at Risk — spółki DJIA

Kod i wyniki do pracy magisterskiej „Porównanie metod szacowania Value at Risk na przykładzie spółek wchodzących w skład Dow Jones Industrial Average" (Uniwersytet Ekonomiczny we Wrocławiu, 2026).

Praca porównuje siedem metod jednodniowego VaR — Variance-Covariance, Historical Simulation, bootstrap blokowy, Monte Carlo, GARCH(1,1), ARMA(1,1)-GARCH(1,1) oraz GARCH-Filtered Quantile Regression (GFQR) — na 30 spółkach indeksu DJIA w latach 2010–2025, w jednolitej ramie okna kroczącego (W = 750). Ocena obejmuje testy Kupca, Christoffersena i Pérignon-Smith, miarę pinball loss oraz testy Diebolda-Mariano i procedurę Model Confidence Set.

Struktura repozytorium
notebooks/VaR_calculations.ipynb — główny kod: pobranie danych, prognozy VaR wszystkich metod, backtesting (Kupiec, Christoffersen, Pérignon-Smith, pinball), eksport wyników do Excela i wykresy.
scripts/analiza_istotnosci.py — analiza istotności różnic między metodami: odtworzenie dziennych strat pinball z prognoz VaR, walidacja względem Tabeli 3.3, test Diebolda-Mariano (HAC/Newey-West + poprawka HLN) parami oraz procedura Model Confidence Set (Hansen-Lunde-Nason) — Tabela 3.4. Wejście: results/wyniki_var_predykcje.xlsx.
scripts/ — pozostałe skrypty pomocnicze (diagnostyka GARCH: α+β, ARCH-LM, Ljung-Box; statystyki opisowe i test Jarque-Bera; odsetek przecięć kwantyli GFQR). [uzupełnij, jeśli te obliczenia były w osobnych plikach]
results/wyniki_var_predykcje.xlsx — prognozy VaR na poziomie spółka × metoda × poziom α × dzień oraz zrealizowane stopy zwrotu (30 spółek × 3273 dni).
results/var_verification_all.xlsx — wyniki testów backtestingowych per spółka (cały okres i cztery podokresy) oraz arkusz zbiorczy.
requirements.txt — wersje bibliotek.
Dane

Notowania dzienne 30 spółek DJIA pobierane są automatycznie z Yahoo Finance przez bibliotekę yfinance (auto_adjust=True — ceny skorygowane o splity i dywidendy), zakres 2010-01-01 – 2026-01-01. Dane pobierane są w kodzie i nie są przechowywane w repozytorium. Data pobrania użyta w pracy: [UZUPEŁNIJ, np. 27.07.2026].

Jak odtworzyć wyniki
python -m venv venv i aktywacja: Linux/Mac source venv/bin/activate, Windows venv\Scripts\activate
pip install -r requirements.txt
Otwórz i uruchom notebooks/VaR_calculations.ipynb (zmienna QUICK = False dla pełnego przebiegu: 30 spółek, W=750, B=5000, 2010–2026).
Wyniki zapiszą się do wyniki_var_predykcje.xlsx oraz var_verification_all.xlsx.
Test Diebolda-Mariano i MCS (Tabela 3.4): uruchom python scripts/analiza_istotnosci.py (wcześniej ustaw w pliku ścieżkę XLSX do results/wyniki_var_predykcje.xlsx).

Reprodukowalność: generatory liczb pseudolosowych są deterministycznie seedowane (skrót MD5 indeksu czasu), więc ponowne uruchomienie na tych samych danych daje identyczne wyniki. W pełnym przebiegu żadna estymacja nie zawiodła (0 braków na 98 190 estymacji na metodę), więc wszystkie metody oceniono na identycznym zbiorze dni.
