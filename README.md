# Stadstrafiken — reseplanerare (mobil)

## Läget

Vi har tagit över den här appen från en utvecklare som slutade. Mobillayouten är faktiskt **gjord och den sitter bra** — den ser ut som den ska på en telefon. Problemet är allt annat.

Hen hann aldrig göra den tillgänglig, och hann heller aldrig få den att fungera på något större än en telefon. Arbetet ligger kvar på branchen `dev`.

En tillgänglighetsgranskning har gjorts och resultatet ligger som tickets längre ner. **Er uppgift är att beta av dem.** Ni rör inte designen — mobillayouten ska se likadan ut när ni är klara.

Appen är en kopia av en riktig reseplanerares startsida, med utbytt logotyp och påhittat trafikbolag. Bilderna är platshållare.

Desktopvyn är inte byggd alls. Den finns som **[designskiss](img/designskiss-desktop.png)** och ska byggas enligt den.

---

## Kom igång

```bash
git clone <repo-url>
cd workshop-reseplaneraren

# Hämta hem den tidigare utvecklarens arbete
git fetch origin
git switch dev

# Skapa er egen branch utifrån dev. Byt ut N mot ert gruppnummer.
git switch -c fix/grupp-N
```

Öppna `index.html` med Live Server. Jobba bara på **er egen branch** — aldrig direkt på `dev`.

Committa ticket för ticket, inte allt på slutet. Skriv ticket-id först i meddelandet:

```bash
git commit -m "A11Y-1: kopplar label till varje fält i sökformuläret"
```

Det gör granskningen mycket lättare för gruppen som får er PR.

---

## Tickets

Prioritet: **Blockerande** måste vara klar, **Hög** ska hinnas med, **Medel** om ni får tid.

### A11Y-1 · Formuläret är inget formulär — Blockerande

Sökrutan består av fyra `input` som ligger löst i en `div`. Det finns inget `<form>`. "Från", "Till", "Datum" och "Tid" ser ut som etiketter men är `<div class="etikett">` — de är alltså inte kopplade till något fält.

**Klart när:** fälten ligger i ett `<form>` och varje fält har en riktig `<label>` kopplad med `for`/`id`. Utseendet ska inte ändras.

### A11Y-2 · Allt klickbart är `div`-ar — Blockerande

"Sök resa", växlaknappen, de två flikarna, "Sök" och "Meny" i toppen samt alla fyra genvägar är `div`. Inget av det går att nå med Tab. Hela sidan har **fyra fokuserbara element** — de fyra inputfälten. Formuläret går inte att skicka utan mus.

**Klart när:** knappar är `<button>`, genvägar och menyval är `<a>`, hela sidan går att använda med enbart tangentbord, och den valda fliken är utpekad i koden och inte bara med färg.

### A11Y-3 · Fokusmarkeringen är bortsläckt — Blockerande

`outline: none` ligger på `.input:focus`.

**Klart när:** alla fokuserbara element har synlig fokusmarkering via `:focus-visible`. Den ska synas mot både vit, ljusgrå och blå bakgrund.

### A11Y-4 · Felmeddelandet är en röd remsa utan text — Hög

`.fel` är tre pixlar hög och röd. Den säger inte vad som är fel och en skärmläsare märker inte att den dykt upp.

**Klart när:** felet har text som säger vad som är fel och hur man rättar det, signaleras med mer än färg, och aviseras med `role="alert"`.

### A11Y-5 · Fel `type` på fälten — Hög

Alla fyra fälten är `type="text"`. Telefonen ger fullt tangentbord i stället för datum- och tidväljare.

**Klart när:** datum- och tidfälten har rätt `type`, och från/till-fälten har vettig `autocomplete`.

### A11Y-6 · Sidan saknar rubriker och landmärken — Hög

Det finns **noll** rubriker på sidan. "Vart vill du åka?" och "Trafikläget just nu" är `div`-ar som bara är stora och feta. Det finns heller ingen `header`, `nav`, `main` eller `footer`.

**Klart när:** sidan har en `h1`, rubriknivåerna följer strukturen utan hopp, och de fyra landmärkena finns.

### A11Y-7 · Kontrast under kraven på tre ställen — Hög

Uppmätt med WCAG-formeln:

| Var | Färger | Uppmätt | Krav |
|---|---|---|---|
| "Uppdaterad idag 13:26" | `#9a9a9a` på `#ffffff` | **2,81:1** | 4,5:1 |
| Länkarna i sidfoten | `#9a9a9a` på `#ffffff` | **2,81:1** | 4,5:1 |
| Ramen runt sökfälten | `#d8dde2` på `#ffffff` | **1,37:1** | 3:1 |

Resten av paletten klarar kraven, inklusive vit text på den blå (4,67:1). Mät innan ni ändrar något annat — den blå ligger nära gränsen och tål inte att göras ljusare.

**Klart när:** de tre klarar sina krav och ingen annan färg har blivit sämre. Skriv de uppmätta värdena i PR-beskrivningen.

### A11Y-8 · Störningsläget syns bara som en färgad prick — Hög

Varje linje i "Trafikläget just nu" har en prick: grön för inga störningar, orange för stora, grå för måttliga. Det finns ingen text alls. Den som inte skiljer färgerna åt får ingen information.

**Klart när:** störningsläget framgår av text bredvid symbolen, som i designskissen. Färgen får finnas kvar som förstärkning.

### A11Y-9 · Bilderna saknar `alt` — Medel

Logotypen och hero-bilden är `<img>` helt utan `alt`-attribut. De är olika fall: den ena är dekoration, den andra bär ett namn.

**Klart när:** båda har ett `alt` som stämmer med vad bilden gör på sidan.

### A11Y-10 · Fel språk i `<html>` — Låg

Sidan är på svenska men `lang="en"`.

**Klart när:** `lang="sv"`.

### RWD-1 · Desktopvyn finns inte — Hög

Det finns inte en enda media query. På en laptop ligger allt kvar i mobilbredd.

Bygg desktopvyn enligt **[designskissen](img/designskiss-desktop.png)**. Noterna längst ner i skissen säger vad som ändras: toppfältet tillkommer, menyn blir utskriven, Från och Till hamnar bredvid varandra med växlaknappen emellan, och Trafikläget blir två kolumner.

**Klart när:** desktopvyn följer skissen, **mobilvyn är oförändrad**, och ni har motiverat era brytpunkter i PR:en. Skissen visar 1280 px — mellanläget bestämmer ni själva.

### RWD-2 · Allt är satt i `px` — Hög

Den som ställer upp textstorleken i webbläsaren får ingen skillnad. WCAG kräver att text går att förstora till 200 % utan att innehåll försvinner.

**Klart när:** text och avstånd är i `rem`, och sidan fungerar vid 200 % utan att något överlappar eller klipps.

### RWD-3 · Flikraden kapas vid 320 px — Medel

Vid 320 px, som en iPhone SE, slutar fliken "Sök avgångar" vid 348 px. Den går alltså inte att läsa. WCAG 1.4.10 kräver att innehåll fungerar vid 320 px utan sidledsscroll.

**Klart när:** inget klipps eller kräver sidledsscroll vid 320 px.

### RWD-4 · För små träffytor i toppen — Medel

"Sök" och "Meny" i den blå toppen är bara **22 px höga**. WCAG 2.2 kräver minst 24×24 px (SC 2.5.8, nivå AA), och 44×44 är praxis för något man trycker på i farten med tummen.

Mät själva i DevTools innan ni ändrar — resten av sidan klarar kravet, så ändra inte på måfå.

**Klart när:** båda träffytorna är minst 24×24 px, gärna 44. Toppraden ska se likadan ut — det är ytan som växer, inte texten eller ikonerna.

## Skicka in

1. Kör igenom er egen checklista innan ni pushar: tangentbord, 320 px, 200 % textstorlek, Lighthouse, [validator.w3.org](https://validator.w3.org/).
2. Pusha branchen: `git push -u origin fix/grupp-N`
3. Öppna en **Pull Request mot `dev`** på GitHub.
4. Fyll i PR-mallen. Kryssa bara i de tickets ni faktiskt gjort — en ärlig PR är lättare att granska än en komplett.
5. Skriv in PR-länken i kanalen.

**PR:en ska inte mergas.** Den ligger kvar för granskning. En annan grupp tar över den, och hur det går till står i [REVIEW.md](REVIEW.md).
