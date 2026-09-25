# Stadstrafiken — reseplanerare (mobil)

## Läget

Vi har tagit över den här appen från en utvecklare som slutade. Mobillayouten är faktiskt **gjord och den sitter bra** — den ser ut som den ska på en telefon. Problemet är allt annat.

Hen hann aldrig göra den tillgänglig, och hann heller aldrig få den att fungera på något större än en telefon. Arbetet ligger kvar på branchen `dev`.

En tillgänglighetsgranskning har gjorts och resultatet ligger som tickets längre ner. **Er uppgift är att beta av dem.** Ni rör inte designen — mobillayouten ska se likadan ut när ni är klara.

Appen är modellerad på en riktig reseplanerare, men trafikbolaget är påhittat.

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

Sökrutan består av fyra `input` som ligger löst i en `div`. Det finns inget `<form>`, och inget fält har en `label`. Placeholder-texten är enda ledtråden om vad fältet vill ha, och den försvinner så fort man börjar skriva.

**Klart när:** fälten ligger i ett `<form>`, varje fält har en synlig `<label>` kopplad med `for`/`id`, och ingen placeholder används som enda etikett.

### A11Y-2 · Knappar och flikar är `div`-ar — Blockerande

"Sök resa", växla-knappen och de tre flikarna är alla `div`. De går inte att nå med Tab och en skärmläsare vet inte att de går att trycka på. Formuläret går alltså inte att skicka utan mus.

**Klart när:** allt som går att trycka på är `<button>` eller `<a>`, hela sidan går att använda med enbart tangentbord, och den valda fliken är utpekad i koden och inte bara med färg.

### A11Y-3 · Fokusmarkeringen är bortsläckt — Blockerande

`outline: none` ligger på `.input:focus`. Den som tabbar ser inte var hen är.

**Klart när:** alla fokuserbara element har en tydligt synlig fokusmarkering. Använd `:focus-visible`. Webbläsarens egen duger, en snyggare egen är bättre — men den ska synas mot både vit och blå bakgrund.

### A11Y-4 · Felmeddelandet är en röd remsa utan text — Hög

`.fel` är en tre pixlar hög röd list som visas när något gått fel. Den säger inte vad som är fel, och en skärmläsare märker inte att den dykt upp.

**Klart när:** felet har en text som säger vad som är fel och hur man rättar det, signaleras med mer än bara färg, och aviseras till skärmläsare med `role="alert"`.

### A11Y-5 · Fel `type` på datum och tid — Hög

Alla fyra fälten är `type="text"`. Telefonen ger då fullt tangentbord i stället för datum- respektive tidväljare.

**Klart när:** datum- och tidfälten har rätt `type`, och från/till-fälten har vettig `autocomplete`.

### A11Y-6 · Sidan saknar rubriker och landmärken — Hög

Det finns ingen `h1` på sidan, faktiskt ingen rubrik alls. "Nästa avgångar från Slussen" är en `div` som ser ut som en rubrik. Hela sidan är `div` — ingen `header`, `nav`, `main` eller `footer`.

**Klart när:** sidan har en `h1`, rubriknivåerna följer strukturen utan hopp, och de fyra landmärkena finns.

### A11Y-7 · Kontrast under AA på tre ställen — Hög

Uppmätt med WCAG-formeln:

| Var | Färger | Uppmätt | Krav |
|---|---|---|---|
| Placeholder i sökfälten | `#9a9a9a` på `#f7f9fa` | **2,66:1** | 4,5:1 |
| Länkarna i sidfoten | `#9a9a9a` på `#ffffff` | **2,81:1** | 4,5:1 |
| Ramen runt sökfälten | `#d8dde2` på `#ffffff` | **1,37:1** | 3:1 |

Resten av paletten klarar AA — mät innan ni ändrar något annat.

**Klart när:** de tre klarar sina krav och ingen annan färg har blivit sämre. Skriv de uppmätta värdena i PR-beskrivningen.

### A11Y-8 · Avvikelser markeras bara med färg — Medel

Två avgångar har en färgad prick: röd för inställd, gul för försenad. Den som inte skiljer rött från gult får ingen information alls.

**Klart när:** avvikelsen framgår av text också, inte bara av färgen.

### A11Y-9 · Fel språk i `<html>` — Låg

Sidan är på svenska men `lang="en"`. Skärmläsaren läser då svenska ord med engelskt uttal.

**Klart när:** `lang="sv"`.

### RWD-1 · Appen skalar inte upp — Hög

`.app` har `max-width: 430px` och det finns inte en enda media query. På en surfplatta eller laptop blir det en smal remsa mitt på skärmen.

**Klart när:** layouten utnyttjar ytan på större skärmar. Mobilvyn ska vara **oförändrad** — bygg vidare mobile first och lägg till uppåt. Välj brytpunkterna efter när innehållet ser illa ut, inte efter enhetsmodeller, och motivera dem i PR:en.

### RWD-2 · Allt är satt i `px` — Hög

Den som ställer upp textstorleken i webbläsaren får ingen skillnad alls. WCAG kräver att text går att förstora till 200 % utan att innehåll försvinner.

**Klart när:** text och avstånd är i `rem`, och sidan fungerar med webbläsarens teckenstorlek på 200 % utan att något överlappar eller klipps.

### RWD-3 · Flikraden kapas vid 320 px — Medel

Vid 320 px bredd, som en iPhone SE, klipps fliken "Trafikläget" av i högerkanten. WCAG 1.4.10 kräver att innehåll går att läsa vid 320 px utan sidledsscroll.

**Klart när:** inget klipps eller kräver sidledsscroll vid 320 px.

### RWD-4 · Träffytan på växla-knappen är för liten — Medel

Knappen som byter plats på Från och Till är 22×22 px. WCAG 2.2 kräver minst 24×24 px (SC 2.5.8, nivå AA). 44×44 är praxis för något man trycker på i farten med tummen.

**Klart när:** träffytan är minst 24×24 px, gärna större. Den får se likadan ut — det är ytan som ska växa, inte cirkeln.

---

## Skicka in

1. Kör igenom er egen checklista innan ni pushar: tangentbord, 320 px, 200 % textstorlek, Lighthouse, [validator.w3.org](https://validator.w3.org/).
2. Pusha branchen: `git push -u origin fix/grupp-N`
3. Öppna en **Pull Request mot `dev`** på GitHub.
4. Fyll i PR-mallen. Kryssa bara i de tickets ni faktiskt gjort — en ärlig PR är lättare att granska än en komplett.
5. Skriv in PR-länken i kanalen.

**PR:en ska inte mergas.** Den ligger kvar för granskning. En annan grupp tar över den, och hur det går till står i [REVIEW.md](REVIEW.md).
