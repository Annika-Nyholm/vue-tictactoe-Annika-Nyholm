# Tre-i-rad (Tic Tac Toe)

Ett Tre-i-rad-spel byggt med Vue.js och SCSS, med hjälp av Vite för snabb utveckling och byggning. Detta projekt uppfyller VG-nivåns krav från uppgiften och erbjuder en modern, interaktiv spelupplevelse.

## 🎮 Funktioner
- **Spelarnamn**: Spelare kan ange namn för X och O innan spelet startar.
- **Spel-logik**: Spelet avgör vinnare eller oavgjort baserat på spelarnas drag.
- **Spelstatus**: Inga drag kan göras efter att spelet avslutats.
- **Nytt spel**: Möjlighet att återställa brädet och börja om.
- **Poänghistorik**: Spelstatistik över vunna matcher sparas och kan visas.
- **Återuppta spel**: Pågående spel och statistik sparas med LocalStorage, så att du kan stänga och öppna webbläsaren utan att förlora data.
- **Nollställning**: Möjlighet att nollställa all statistik och börja om med nya spelare.

## 🛠 Teknologier
Projektet är byggt med:
- [Vue.js 3](https://vuejs.org/) för användargränssnitt och komponentbaserad utveckling.
- [Vite](https://vitejs.dev/) för snabb utveckling och byggning av projektet.
- [SCSS](https://sass-lang.com/) för modulär och effektiv styling.
- LocalStorage API för att spara spelstatus och statistik.

## 📸 Demo
*(Lägg till en länk till en live-demo här, eller skärmdumpar som visar spelets utseende och funktioner.)*

## 🚀 Installation och användning
För att köra projektet lokalt:

1. **Klona detta repository**:
   ```bash
   git clone https://github.com/Medieinstitutet/vue-tictactoe-Annika-Nyholm
2. **Navigera till projektmappen:**
   ```bash
   cd vue-tictactoe-Annika-Nyholm
3. **Installera beroenden:**
    ```bash
   npm install
4. **Starta utvecklingsservern:**
   ```bash
   npm run dev
   Applikationen kommer att köras på http://localhost:5173.
5. **Bygg produktionen (valfritt):**
   ```bash
   Kopiera kod
   npm run build
