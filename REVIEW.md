# 🔍 Kodgranskning mellan grupper

Varje grupp granskar en annan grupps PR. Ni granskar alltså inte er egen kod, och ni får er egen kod granskad av någon som inte satt med när ni skrev den. Det är hela poängen.

## 🔄 Vem granskar vem

Granskningen går i en ring: **grupp 1 granskar grupp 2, grupp 2 granskar grupp 3, och sista gruppen granskar grupp 1.**

Sandra lägger upp ringen i kanalen när alla PR:ar är öppnade.

## ⚠️ Regeln som gör granskningen värd något

**Ni får inte granska genom att bara läsa diffen.** Ni ska köra koden.

```bash
git fetch origin
git switch fix/grupp-N
```

Öppna sidan och testa själva. En granskning som inte har kört koden är en gissning.

## 🧭 Så här granskar ni

### 1. 🎯 Testa mot ticketen, inte mot tycke

Öppna [README.md](README.md) bredvid. Varje ticket har ett **Klart när**. Det är kravet — inte vad ni själva hade gjort.

### 2. 🧪 Kör de fem testerna

| Test | Hur |
|---|---|
| Tangentbord | Lägg undan musen. Tabba igenom hela sidan. Kommer ni åt allt? Syns fokus hela tiden? Går formuläret att skicka? |
| 320 px | Dra ihop fönstret. Klipps något? Finns sidledsscroll? |
| 200 % text | Firefox: Inställningar → Zooma endast text, sedan Cmd/Ctrl och plus till 200 %. Växer texten? Överlappar något? Chrome duger inte — dess zoom förstorar även `px` och döljer felet. |
| Uppåt | Dra ut fönstret brett. Ser det avslutat ut? Är mobilvyn oförändrad? |
| Lighthouse | Kör Accessibility. Notera poängen. |

### 3. 💬 Skriv kommentarerna i "Files changed"

Kommentera på **raden** det gäller, inte i ett samlat inlägg. Då ser den som ska rätta exakt var problemet sitter.

Minst **tre radkommentarer**, och minst en av dem ska hänvisa till ett specifikt **Klart när**.

Skriv så här:

> **A11Y-3:** `outline: none` ligger kvar på rad 84 för `.flik:focus`. Ticketen säger att alla fokuserbara element ska ha synlig markering — flikarna missades.

Och inte så här:

> Ser bra ut! Kanske kolla fokus?

### 4. ✅ Avsluta granskningen

I "Submit review", välj ett av två:

- **Request changes** — något *Klart när* är inte uppfyllt. Skriv vilka tickets det gäller.
- **Approve** — allt ni testat uppfyller sina krav. Skriv **vilka tickets ni verifierade och hur ni testade dem**. Ett "Approve" utan den listan räknas inte.

Hittar ni inget att anmärka på har ni antagligen inte kört de fem testerna.

## 🤝 Att få kritik

Svara på varje kommentar. Håller ni inte med, säg det och motivera — en granskare kan ha fel, och en PR är en diskussion och inte en dom.

Rätta det ni håller med om, committa på samma branch och pusha. PR:en uppdateras av sig själv.

## 🎓 Vad ni ska ha med er

Ingen PR mergas idag. Poängen är inte att få in koden, utan att ni har läst någon annans kod med ett krav i handen, och att någon har läst er.
