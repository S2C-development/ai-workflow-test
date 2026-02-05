# Hello World HTML Design

## Doel

Een simpele, standalone HTML pagina maken die "Hello World" toont aan de gebruiker.

## Requirements

- Eén HTML bestand
- Geen externe dependencies
- Moet werken in alle moderne browsers
- Clean en leesbare code

## File Structuur

```
/
├── src/
│   └── hello.html
```

## HTML Structuur

### Basis Opzet

```html
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

### Elementen

1. **DOCTYPE**: HTML5 declaratie
2. **html lang**: Taal attribuut voor toegankelijkheid
3. **meta charset**: UTF-8 encoding voor internationale karakters
4. **meta viewport**: Responsive design support voor mobiel
5. **title**: Browser tab titel
6. **h1**: Hoofdkop met "Hello World" tekst

## Optionele Uitbreidingen

### Met Styling

```html
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
        h1 {
            color: white;
            font-size: 3rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
    </style>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```

### Met Interactiviteit

```html
<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
</head>
<body>
    <h1 id="greeting">Hello World</h1>
    <button onclick="changeGreeting()">Klik mij!</button>

    <script>
        function changeGreeting() {
            const greetings = ['Hello World', 'Hallo Wereld', 'Bonjour Monde', 'Hola Mundo'];
            const h1 = document.getElementById('greeting');
            const randomIndex = Math.floor(Math.random() * greetings.length);
            h1.textContent = greetings[randomIndex];
        }
    </script>
</body>
</html>
```

## Implementatie Aanpak

### Stap 1: Basis HTML
- Maak `src/hello.html`
- Voeg basis HTML5 structuur toe
- Test in browser (open bestand direct)

### Stap 2: Styling (Optioneel)
- Voeg `<style>` tag toe in `<head>`
- Centreer content
- Voeg kleuren/gradient toe

### Stap 3: Interactiviteit (Optioneel)
- Voeg button element toe
- Implementeer JavaScript functie
- Test onclick functionaliteit

## Testing

- Open `hello.html` in verschillende browsers:
  - Chrome
  - Firefox
  - Safari
  - Edge
- Test op verschillende devices:
  - Desktop
  - Tablet
  - Mobiel
- Valideer HTML met W3C validator

## Deployment

Meerdere opties:
1. **Lokaal**: Open bestand direct in browser
2. **GitHub Pages**: Push naar gh-pages branch
3. **Netlify**: Drag-and-drop deployment
4. **Vercel**: Connect repository

## Voordelen van Deze Aanpak

- **Simpel**: Één bestand, geen build process
- **Snel**: Onmiddellijk te testen
- **Portable**: Werkt overal waar een browser is
- **Geen dependencies**: Volledig standalone

## Conclusie

Een Hello World HTML pagina is de meest straightforward manier om te beginnen met web development. Het vereist geen tooling, geen dependencies en geen build process - gewoon een teksteditor en een browser.

De basis versie is minimalistisch, maar kan eenvoudig uitgebreid worden met styling en interactiviteit naarmate de requirements groeien.
