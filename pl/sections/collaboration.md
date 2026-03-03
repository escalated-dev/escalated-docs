# Współpraca agentów

Utrzymuj synchronizację zespołu wsparcia dzięki wskaźnikom obecności w czasie rzeczywistym i przypiętym notatkom wewnętrznym. Nie są potrzebne zewnętrzne narzędzia.

## Wykrywanie kolizji

Gdy wielu agentów otwiera to samo zgłoszenie, każdy agent widzi wskaźnik avatara pokazujący, kto jeszcze aktualnie je przegląda. Zapobiega to podwójnym odpowiedziom i marnowaniu wysiłku.

- Stos avatarów z inicjałami pozostałych przeglądających
- Tooltip „Also viewing" po najechaniu
- Odpytywanie co 30 sekund -- lekkie, oparte na cache (nie wymaga tabeli w bazie danych)

## Wskaźniki pisania

Agenci mogą nadawać stan aktywnego pisania podczas tworzenia odpowiedzi, aby współpracownicy mogli unikać nakładających się odpowiedzi.

- Stan pisania w czasie rzeczywistym dla każdego zgłoszenia
- Uzupełnienie wykrywania kolizji dla szybszego przekazywania

## Przypięte notatki wewnętrzne

Ważne notatki wewnętrzne mogą być przypięte na górze widoku szczegółów zgłoszenia. Przypięte notatki są wyróżnione w bursztynowej karcie nad wątkiem konwersacji, aby agenci nie przeoczyli istotnego kontekstu.

- Przypięcie lub odpięcie dowolnej notatki wewnętrznej jednym kliknięciem
- Przypięte notatki wyświetlane na górze zgłoszenia, zawsze widoczne
- Tylko notatki wewnętrzne mogą być przypinane -- odpowiedzi publiczne nie

## Panel wiedzy

Pasek boczny zgłoszenia zawiera kontekstowy panel wiedzy, dzięki któremu agenci mogą odwoływać się do powiązanych treści pomocy bez opuszczania widoku zgłoszenia.
