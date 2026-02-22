# Parallax efekt, Flexbox, Scroll Snap

Tento projekt slouží jako ukázka základního **parallax efektu** vytvořeného čistě pomocí CSS a zarovnání prvků pomocí **Flexboxu**. Web prezentuje roční období formou střídání vizuálně atraktivních sekcí s fixním pozadím a informačních bloků.

## Popis webu (Zadání)

Webová stránka je koncipována jako "one-page" prezentace rozdělená do několika logických sekcí:

*   **Vizuální vzhled**:
    *   Stránka využívá moderní font *Playwrite AT* pro nadpisy i text.
    *   Střídají se celoobrazovkové sekce s obrázky na pozadí (zima, léto) a bílé sekce s textem.
    *   Obrázky na pozadí zůstávají při scrollování "přilepené" na místě, čímž vzniká dojem hloubky (parallax efekt).
    *   Nadpisy v obrázkových sekcích jsou perfektně vycentrované (vertikálně i horizontálně).
    *   Textové sekce jsou čisté, s tmavým textem na bílém podkladu pro dobrou čitelnost.

*   **Funkčnost**:
    *   Responzivní design (přizpůsobí se šířce okna díky `background-size: cover` a flexibilitě HTML).
    *   Plynulé scrollování.

## Technické řešení

Projekt je postaven na technologiích **HTML5** a **CSS3**. Nejsou využity žádné frameworky ani JavaScript, důraz je kladen na pochopení základních principů stylování.

### Použité technologie

*   **HTML5**: Sémantické značkování obsahu (`<section>`, `<article>` - v našem případě hlavně `section`).
*   **CSS3**: Stylování vzhledu, import fontů, layout.

### Vysvětlení principů

#### 1. Flexbox zarovnání
Pro zarovnání nadpisů uprostřed velkých obrázkových sekcí je využit **Flexible Box Layout (Flexbox)**.

```css
.parallax {
    display: flex;              /* Aktivuje flexbox kontejner */
    justify-content: center;    /* Zarovná obsah vodorovně na střed */
    align-items: center;        /* Zarovná obsah svisle na střed */
}
```
Díky těmto třem řádkům je obsah (`<h2>`) vždy přesně uprostřed rodičovského elementu, bez nutnosti počítat marginy nebo paddingy.

#### 2. CSS Parallax (background-attachment)
Klíčovým prvkem stránky je parallax efekt. Ten je zde realizován nejjednodušší možnou cestou – fixací pozadí vůči oknu prohlížeče.

```css
.parallax {
    background-attachment: fixed; /* Pozadí se nehýbe při scrollování stránky */
    background-position: center;  /* Pozadí je vycentrováno */
    background-repeat: no-repeat; /* Pozadí se neopakuje */
    background-size: cover;       /* Pozadí se roztáhne na celou plochu elementu */
    min-height: 100vh;            /* Sekce má výšku minimálně jako celé okno prohlížeče */
}
```
Vlastnost `background-attachment: fixed` způsobí, že se obrázek na pozadí chová jako by byl "přilepený" na pozadí okna prohlížeče, zatímco obsah stránky (textové sekce) přes něj přejíždí.

#### 3. CSS Scroll Snap (Přichytávání)
Pro moderní plynulý pocit z procházení webu je použita funkce **Scroll Snap**. Tato funkce zajistí, že při scrollování se stránka automaticky "přichytí" k začátku nejbližší sekce.

**Implementace:**
1.  **Kontejner (`html`)**: Nastavíme typ přichytávání.
    ```css
    html {
        scroll-snap-type: y mandatory; /* y = svisle, mandatory = musí se přichytit */
        scroll-behavior: smooth;      /* Plynulý posun při kliknutí na kotvy (volitelné) */
    }
    ```
2.  **Sekce (`section`)**: Určíme, kterou částí se mají přichytit.
    ```css
    section {
        scroll-snap-align: start; /* Přichytí horní hranu sekce k horní hraně okna */
    }
    ```

#### 4. SVG Přechod (Tvarový oddělovač)
Pro plynulejší přechod mezi obrázkovou sekcí a bílým obsahem je použit tvarový oddělovač ve formátu SVG.

**Implementace:**
1.  **SVG Soubor**: Tvar vlnky je uložen v samostatném souboru `img/wave.svg`.
2.  **HTML**: Uvnitř sekce `.parallax` je vložen kontejner s obrázkem `<img src="img/wave.svg">`.
3.  **CSS**:
    *   `.parallax` má `position: relative`.
    *   Kontejner/obrázek je absolutně pozicován na dno sekce, rotažen na celou šířku a otočen o 180 stupňů (pokud je potřeba).

## Cíl projektu

Tento projekt slouží k osvojení následujících dovedností pro žáky 2IT:

1.  **Základní HTML struktura**: Používání tagů `<section>` pro rozdělení obsahu.
2.  **CSS Flexbox**: Pochopení, jak jednoduše zarovnávat prvky na střed.
3.  **Práce s pozadím v CSS**: Ovládnutí vlastností `background-image`, `size`, `position` a klíčové `attachment` pro parallax.
4.  **CSS Scroll Snap**: Moderní způsob, jak zajistit přesné scrollování po sekcích bez JavaScriptu.
5.  **SVG v CSS**: Použití SVG grafiky pro pokročilé stylování přechodů.
6.  **Typografie**: Import externích fontů (Google Fonts) a jejich aplikace.
