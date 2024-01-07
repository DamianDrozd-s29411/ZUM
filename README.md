# ZUM

Wykorzystano zestaw danych z UCI ML Drug Review dataset dostępny na Kaggle. Zawiera on recenzje leków wraz z ocenami użytkowników. Recenzje są klasyfikowane na podstawie oceny: pozytywna (ocena >= 7), neutralna (ocena 4-6) lub negatywna (ocena < 4).

Przetwarzanie danych:
Oczyszczanie tekstu: Recenzje są normalizowane poprzez konwersję na małe litery, usunięcie znaków specjalnych i słów o długości 1-2 znaków oraz eliminację słów nieistotnych (stop words).
Tokenizacja i dopełnianie: Tekst recenzji jest konwertowany na sekwencje liczbowe za pomocą tokenizera, a następnie sekwencje te są dopełniane do jednolitej długości 100.
Budowa modeli:
1. LSTM (Long Short-Term Memory):
Warstwa osadzania: Przekształca indeksy słów na gęste wektory o długości 50.
Warstwa LSTM: Z 64 jednostkami, do analizy sekwencji danych.
Warstwa gęsta: 3 jednostki z funkcją aktywacji 'softmax', klasyfikująca recenzje.
2. CNN (Convolutional Neural Network):
Warstwa osadzania: Tak samo jak w modelu LSTM.
Warstwa konwolucyjna 1D: Z 128 filtrami i rozmiarem jądra 5, do wydobywania cech lokalnych.
Warstwa GlobalMaxPooling1D: Do redukcji wymiarowości danych.
Warstwa gęsta: Identyczna jak w modelu LSTM.
3. Pre-trained Word Embeddings (GloVe):
Pre-trained embeddings: Wykorzystanie glove.6B.100d.txt.gz od GloVe dla bogatszych reprezentacji semantycznych słów.
Warstwa osadzania: Z pre-trained embeddings GloVe, zamrożona (bez dodatkowego treningu).
Warstwa LSTM: Identyczna jak w pierwszym modelu.
Warstwa gęsta: Tak samo jak w poprzednich modelach.


Trenowanie i walidacja:
Modele są trenowane na danych treningowych z monitorowaniem na zestawie walidacyjnym. Optymalizator 'adam' i funkcja straty 'categorical_crossentropy' są używane we wszystkich modelach, a jako metryka wybrano 'accuracy'.
