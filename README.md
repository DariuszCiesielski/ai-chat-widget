# AI Chat Widget

Nowoczesny widget chatu HTML z integracją webhooków n8n do komunikacji z agentami AI.

![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 🎯 Funkcje

- 💬 **Nowoczesny interfejs** - Design w stylu popularnych aplikacji czatowych
- 🔄 **Integracja n8n** - Komunikacja przez WebHook z automatyzacją n8n
- 📱 **Responsywny** - Działa świetnie na mobile i desktop
- ⛶ **Pełny ekran** - Możliwość powiększenia na cały ekran
- ✨ **Animacje** - Płynne animacje i efekty wizualne
- 🎨 **Gradient** - Elegancki gradient w kolorach fioletowo-niebieskich
- 💾 **Sesje** - Automatyczne zarządzanie sesjami użytkowników
- ⌨️ **Skróty klawiszowe** - Enter wysyła, Shift+Enter nowa linia
- 🔔 **Wskaźniki** - Animowany wskaźnik pisania
- 🎯 **Standalone** - Jeden plik HTML gotowy do wdrożenia

## 📸 Podgląd

Widget zawiera:
- Przycisk czatu w prawym dolnym rogu
- Okno czatu z nagłówkiem i avatarem
- Obszar wiadomości z animacjami
- Pole do wpisywania wiadomości
- Przyciski pełnego ekranu i zamknięcia

## 🚀 Szybki start

### 1. Skonfiguruj n8n webhook

W n8n utwórz workflow z webhook node:

1. Dodaj node **Webhook**
2. Ustaw metodę na **POST**
3. Skopiuj URL webhooka
4. Dodaj node AI (OpenAI, Claude, itp.)
5. Dodaj node **Respond to Webhook**

### 2. Skonfiguruj widget

Otwórz `chat-widget.html` i znajdź:

```javascript
const CONFIG = {
    webhookUrl: 'YOUR_N8N_WEBHOOK_URL_HERE',
    headers: {
        'Content-Type': 'application/json'
    }
};
```

Zamień `'YOUR_N8N_WEBHOOK_URL_HERE'` na URL swojego webhooka.

### 3. Dodaj do strony

**Opcja A: Bezpośrednio w HTML**

Skopiuj cały kod z `chat-widget.html` i wklej przed `</body>`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Twoja Strona</title>
</head>
<body>
    <!-- Twoja treść -->

    <!-- Chat Widget - wklej tutaj cały kod -->

</body>
</html>
```

**Opcja B: Jako iframe**

```html
<iframe
    src="chat-widget.html"
    style="border:none; position:fixed; bottom:0; right:0; width:100%; height:100%; pointer-events:none;"
></iframe>
```

**Opcja C: Przez JavaScript**

```javascript
fetch('chat-widget.html')
    .then(response => response.text())
    .then(html => {
        const container = document.createElement('div');
        container.innerHTML = html;
        document.body.appendChild(container);
    });
```

## 📡 API - Komunikacja z n8n

### Request (Widget → n8n)

Widget wysyła POST request z następującymi danymi:

```json
{
    "message": "Tekst wiadomości od użytkownika",
    "timestamp": "2025-11-06T12:34:56.789Z",
    "sessionId": "session_1699273456789_abc123xyz"
}
```

**Pola:**
- `message` - Treść wiadomości użytkownika
- `timestamp` - Znacznik czasu ISO 8601
- `sessionId` - Unikalny ID sesji (zachowywany w sessionStorage)

### Response (n8n → Widget)

n8n powinien zwrócić JSON w formacie:

```json
{
    "response": "Odpowiedź od AI"
}
```

lub

```json
{
    "message": "Odpowiedź od AI"
}
```

Widget automatycznie wyświetli treść z pola `response` lub `message`.

## 🔧 Przykładowy workflow n8n

```
┌─────────────────┐
│ Webhook (POST)  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Function Node   │  ← Opcjonalne: Przygotuj dane
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ OpenAI/Claude   │  ← Node AI
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Function Node   │  ← Formatuj odpowiedź
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Respond to      │
│ Webhook         │
└─────────────────┘
```

### Przykład Function Node (Formatuj odpowiedź)

```javascript
return [
  {
    json: {
      response: $input.item.json.output,
      sessionId: $input.item.json.sessionId
    }
  }
];
```

## 🎨 Personalizacja

### Zmiana kolorów

Znajdź w CSS gradienty i zmień kolory:

```css
/* Z fioletowego na różowy */
background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);

/* Z fioletowego na zielony */
background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);

/* Z fioletowego na niebieski */
background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
```

### Zmiana tekstów

W HTML:

```html
<!-- Nagłówek -->
<h3>Asystent AI</h3>
<p>Online</p>

<!-- Powitanie -->
<h4>Witaj! 👋</h4>
<p>Jestem Twoim asystentem AI. Jak mogę Ci dzisiaj pomóc?</p>

<!-- Placeholder -->
<textarea placeholder="Wpisz wiadomość..."></textarea>
```

### Zmiana pozycji

Domyślnie: prawy dolny róg

```css
.chat-widget {
    position: fixed;
    bottom: 20px;
    right: 20px;
}
```

Lewy dolny róg:

```css
.chat-widget {
    position: fixed;
    bottom: 20px;
    left: 20px;
}
```

### Zmiana rozmiaru

```css
.chat-window {
    width: 380px;  /* Szerokość */
    height: 600px; /* Wysokość */
}
```

### Zmiana avatara

```html
<!-- Bot -->
<div class="chat-avatar">🤖</div>

<!-- Zamień na inną emoji lub literę -->
<div class="chat-avatar">💬</div>
<div class="chat-avatar">AI</div>
```

## 🔒 Bezpieczeństwo

### Zalecenia

1. **CORS** - Skonfiguruj CORS w n8n dla swojej domeny
2. **Rate Limiting** - Dodaj ograniczenia w n8n workflow
3. **Walidacja** - Waliduj dane wejściowe w n8n
4. **HTTPS** - Używaj tylko HTTPS w produkcji
5. **Sanityzacja** - Zabezpiecz się przed XSS

### Ustawienia CORS w n8n

Dodaj nagłówki w node "Respond to Webhook":

```javascript
{
  "Access-Control-Allow-Origin": "https://twoja-domena.pl",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
  "Access-Control-Allow-Headers": "Content-Type"
}
```

### Rate Limiting w n8n

Dodaj node "Code" przed AI:

```javascript
// Sprawdź liczbę żądań z sesji
const sessionId = $input.item.json.sessionId;
const maxRequests = 10; // max na godzinę

// Implementuj logikę rate limiting
// np. używając Redis lub pamięci tymczasowej
```

## 🐛 Rozwiązywanie problemów

### ❌ "Webhook URL nie został skonfigurowany"

**Przyczyna:** Nie zmieniono URL webhooka w konfiguracji.

**Rozwiązanie:**
```javascript
webhookUrl: 'https://twoj-n8n.com/webhook/abc123'
```

### ❌ "Wystąpił błąd podczas wysyłania wiadomości"

**Możliwe przyczyny:**
- Błędny URL webhooka
- n8n nie jest uruchomiony
- Problemy z CORS
- Webhook nie zwraca JSON

**Rozwiązanie:**
1. Sprawdź konsolę przeglądarki (F12)
2. Sprawdź logi n8n
3. Przetestuj webhook w Postman/curl:

```bash
curl -X POST https://twoj-n8n.com/webhook/abc123 \
  -H "Content-Type: application/json" \
  -d '{"message":"test","timestamp":"2025-11-06T12:00:00Z","sessionId":"test123"}'
```

### ❌ Widget nie wyświetla się

**Rozwiązanie:**
1. Sprawdź czy kod jest przed `</body>`
2. Sprawdź konsolę na błędy JavaScript
3. Sprawdź konflikty z-index w CSS
4. Sprawdź czy JavaScript jest włączony

### ❌ Brak odpowiedzi AI

**Rozwiązanie:**
1. Sprawdź format odpowiedzi z n8n
2. Odpowiedź musi zawierać `response` lub `message`
3. Sprawdź network tab w DevTools
4. Sprawdź workflow w n8n

## 📊 Monitoring i Analytics

### Dodanie Google Analytics

```javascript
// Po wysłaniu wiadomości
gtag('event', 'chat_message_sent', {
    'event_category': 'Chat',
    'event_label': 'User Message'
});

// Po otrzymaniu odpowiedzi
gtag('event', 'chat_response_received', {
    'event_category': 'Chat',
    'event_label': 'AI Response'
});
```

### Logowanie w n8n

W Function node dodaj:

```javascript
console.log('Chat request:', {
    sessionId: $input.item.json.sessionId,
    message: $input.item.json.message,
    timestamp: $input.item.json.timestamp
});

return [$input.item];
```

## 🧪 Testowanie

### Test lokalny

1. Otwórz `chat-widget.html` w przeglądarce
2. Otwórz DevTools (F12)
3. Skonfiguruj webhook URL
4. Wyślij testową wiadomość
5. Sprawdź network tab

### Test CORS

```javascript
// W konsoli przeglądarki
fetch('https://twoj-n8n.com/webhook/abc123', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({message: 'test', timestamp: new Date().toISOString(), sessionId: 'test'})
}).then(r => r.json()).then(console.log);
```

## 📚 Dodatkowe zasoby

- [n8n Documentation](https://docs.n8n.io/)
- [Webhook Node Docs](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/)
- [OpenAI Node Docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.lmchatopenai/)

## 📝 Licencja

MIT License - Wolne do użytku w projektach komercyjnych i niekomercyjnych.

## 🤝 Wsparcie

Jeśli napotkasz problemy:

1. Sprawdź sekcję "Rozwiązywanie problemów"
2. Sprawdź konsolę przeglądarki (F12)
3. Sprawdź logi n8n
4. Przetestuj webhook osobno

## 🎉 Changelog

### v1.0.0 (2025-11-06)
- Pierwsza wersja
- Pełna integracja z n8n
- Tryb pełnoekranowy
- Responsywny design
- Obsługa sesji
- Animacje i efekty wizualne
