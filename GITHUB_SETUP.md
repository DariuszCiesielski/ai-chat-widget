# 🚀 Jak wrzucić projekt na GitHub

Projekt został przygotowany jako osobne repozytorium Git. Oto instrukcje jak umieścić go na GitHubie.

## Sposób 1: Przez GitHub UI (Najłatwiejszy)

### Krok 1: Utwórz nowe repozytorium na GitHub

1. Przejdź na https://github.com/new
2. Nazwij repozytorium: **ai-chat-widget**
3. Dodaj opis: "Modern AI chat widget with n8n webhook integration"
4. **NIE** inicjalizuj z README, .gitignore ani licencją (już je mamy!)
5. Kliknij "Create repository"

### Krok 2: Dodaj remote i wypchnij kod

Po utworzeniu repozytorium GitHub pokaże Ci instrukcje. Użyj poniższych komend:

```bash
cd /home/user/ai-chat-widget

# Dodaj remote (zamień TWOJA-NAZWA na swoją nazwę użytkownika GitHub)
git remote add origin https://github.com/TWOJA-NAZWA/ai-chat-widget.git

# Wypchnij kod
git push -u origin main
```

### Krok 3: Gotowe! 🎉

Twoje repozytorium jest teraz na GitHubie pod adresem:
`https://github.com/TWOJA-NAZWA/ai-chat-widget`

## Sposób 2: Przez GitHub CLI (gh)

Jeśli masz zainstalowane GitHub CLI:

```bash
cd /home/user/ai-chat-widget

# Utwórz repozytorium i wypchnij w jednej komendzie
gh repo create ai-chat-widget --public --source=. --remote=origin --push

# Lub prywatne repozytorium
gh repo create ai-chat-widget --private --source=. --remote=origin --push
```

## Sposób 3: Import do istniejącego repo

Jeśli chcesz dodać to do istniejącego repozytorium:

```bash
cd /home/user/ai-chat-widget

# Dodaj remote istniejącego repo
git remote add origin https://github.com/TWOJA-NAZWA/NAZWA-REPO.git

# Pobierz istniejący kod
git fetch origin

# Zmerguj jeśli potrzeba
git merge origin/main --allow-unrelated-histories

# Wypchnij
git push -u origin main
```

## Struktura projektu

```
ai-chat-widget/
├── .git/                           # Git repository
├── .gitignore                      # Git ignore rules
├── LICENSE                         # MIT License
├── README.md                       # Main documentation
├── GITHUB_SETUP.md                 # This file
├── chat-widget.html                # Main widget file
├── example.html                    # Demo page
└── example-n8n-workflow.json       # Sample n8n workflow
```

## Następne kroki po wrzuceniu na GitHub

### 1. Zaktualizuj README.md

Zamień przykładowe linki na prawdziwe:

```markdown
[View Demo](https://twoja-nazwa.github.io/ai-chat-widget/example.html)
```

### 2. Włącz GitHub Pages

Aby demo działało online:

1. Przejdź do Settings → Pages
2. Source: Deploy from a branch
3. Branch: main, folder: / (root)
4. Zapisz

Twój widget będzie dostępny pod:
`https://twoja-nazwa.github.io/ai-chat-widget/example.html`

### 3. Dodaj Topics

W głównym widoku repozytorium kliknij ⚙️ i dodaj topics:
- `ai`
- `chat`
- `chatbot`
- `n8n`
- `webhook`
- `widget`
- `javascript`
- `html`

### 4. Dodaj badges do README

Na początku README.md dodaj:

```markdown
![GitHub stars](https://img.shields.io/github/stars/twoja-nazwa/ai-chat-widget)
![GitHub forks](https://img.shields.io/github/forks/twoja-nazwa/ai-chat-widget)
![GitHub issues](https://img.shields.io/github/issues/twoja-nazwa/ai-chat-widget)
![License](https://img.shields.io/badge/license-MIT-blue.svg)
```

### 5. Dodaj Social Preview

1. Przejdź do Settings
2. Przewiń do "Social preview"
3. Kliknij "Edit"
4. Dodaj screenshot widgetu (1280x640px)

## Aktualizacje w przyszłości

Gdy będziesz chciał dodać zmiany:

```bash
cd /home/user/ai-chat-widget

# Sprawdź zmiany
git status

# Dodaj pliki
git add .

# Commit
git commit -m "Opis zmian"

# Push
git push origin main
```

## Problemy?

### Błąd: "remote origin already exists"

```bash
git remote remove origin
git remote add origin https://github.com/TWOJA-NAZWA/ai-chat-widget.git
```

### Błąd: "failed to push some refs"

```bash
git pull origin main --rebase
git push origin main
```

### Błąd: Authentication failed

Użyj Personal Access Token zamiast hasła:

1. Przejdź na https://github.com/settings/tokens
2. Generate new token (classic)
3. Zaznacz: repo, workflow
4. Skopiuj token
5. Użyj tokena jako hasła podczas push

Lub skonfiguruj SSH:

```bash
# Wygeneruj klucz SSH
ssh-keygen -t ed25519 -C "twoj@email.com"

# Dodaj klucz na GitHub
cat ~/.ssh/id_ed25519.pub
# Skopiuj output i dodaj w GitHub Settings → SSH Keys

# Zmień remote na SSH
git remote set-url origin git@github.com:TWOJA-NAZWA/ai-chat-widget.git
```

## Gotowe do udostępnienia!

Po wrzuceniu na GitHub, możesz:
- Udostępnić link znajomym
- Dodać do swojego portfolio
- Opublikować na Reddit/Twitter
- Dodać do awesome lists
- Stworzyć blog post o projekcie

Powodzenia! 🚀
