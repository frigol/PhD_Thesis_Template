# Manuale Comandi — Tesi Dottorato

Riferimento rapido per `thesis.sty`, `worknotes.sty` e norme editoriali PRIMPHD.

---

## 1. Citazioni bibliografiche

`biblatex` con `autocite=footnote`: le note vengono generate automaticamente. La prima occorrenza produce la citazione completa; le successive il formato abbreviato (`Cognome, Titolo abbreviato cit.`).

```latex
% Prima occorrenza → nota completa
\autocite{key}

% Con numero di pagina
\autocite[p.~nn]{key}

% Con intervallo di pagine
\autocite[pp.~nn--mm]{key}

% Con prenote + numero di pagina
\autocite[cfr.][p.~nn]{key}
\autocite[si veda][pp.~nn--mm]{key}

% Autore integrato nel corpo del testo (non in nota)
\textcite{key}
\textcite[p.~nn]{key}

% Citazione breve nel testo + nota
«testo citato»\autocite[p.~nn]{key}

% Citazione con omissione interna
«testo [...] testo»\autocite[p.~nn]{key}

% Citazione interna ad altra citazione (gerarchia: « " ' ' " »)
«testo con "citazione interna" ancora testo»\autocite[p.~nn]{key}
```

---

## 2. Citazioni lunghe (≥ 3 righe)

Corpo 11, rientro su entrambi i lati, senza virgolette, riga bianca prima e dopo. La nota bibliografica va **dopo** l'ambiente.

```latex
\begin{longcit}
    Testo della citazione lunga, in tondo, senza virgolette.
\end{longcit}
\autocite[pp.~nn--mm]{key}
```

---

## 3. Virgolette

```latex
% Caporali automatiche (csquotes — basta usare i doppi apici)
"testo"    % → «testo»

% Caporali esplicite
«testo»

% Doppie alte — istituzioni, secondo livello di citazione
"testo"    % (U+201C / U+201D)

% Singole alte — parole in evidenza, terzo livello
'testo'    % (U+2018 / U+2019)

% Gerarchia completa
«testo esterno "secondo livello 'terzo livello' fine" fine»
```

---

## 4. Parole in lingua straniera

In corsivo se non di uso comune; non declinate.

```latex
\textit{beamforming}
\textit{Higher-Order Ambisonics}

% Citazione in lingua straniera: originale nel corpo,
% traduzione in nota con indicazione della fonte
«original text»\footnote{Trad. it.: «traduzione». \autocite[p.~nn]{key}}
```

---

## 5. Risorse di rete

```latex
\webresource{https://www.conservatoriovivaldi.it}{06/10/2025}
% → <https://www.conservatoriovivaldi.it> (ultima cons. 06/10/2025)
```

---

## 6. Riferimenti incrociati interni

I `\label` dei **capitoli** vanno in `thesis.tex` subito dopo `\chapter{}`. I `\label` di sezioni e sottosezioni vanno nei file `chapter0X.tex` subito dopo `\section{}` o `\subsection{}`.

I riferimenti nel testo usano `cleveref` (`\cref` / `\Cref`), che genera automaticamente il nome del tipo di riferimento (Chapter, Section, Appendix...) senza doverlo scrivere a mano.

```latex
% Definire l'etichetta (punto di destinazione)
\chapter{Titolo}
\label{cap:chiave}

\section{Titolo}
\label{sec:chiave}

\subsection{Titolo}
\label{subsec:chiave}

% Richiamare nel testo — cref genera automaticamente "Chapter"/"Section"/ecc.
\cref{cap:chiave}      % → "chapter 3"
\Cref{cap:chiave}      % → "Chapter 3" (maiuscolo, a inizio frase)
\cref{sec:chiave}      % → "section 3.2"
p.~\pageref{sec:chiave}   % numero di pagina (resta \pageref, non cambia)

% Esempio completo
come si discuterà in \cref{cap:interprete} (p.~\pageref{cap:interprete})
```

> **Nota:** LaTeX risolve i `\cref`/`\ref` in due passate di compilazione. Se compare `??` nel PDF, ricompilare.

> **Nota:** `\Cref{}` (C maiuscola) va usato a inizio frase; `\cref{}` (minuscolo) all'interno della frase.

---

## 6bis. Riferimenti alle appendici

Le appendici usano un contatore dedicato (`appsec`) associato al comando `\appendixsection{}`, definito in `thesis.sty`. `\cref` riconosce questo contatore e genera automaticamente "Appendix X".

```latex
% In thesis.tex, dentro \chapter*{Appendici}
\appendixsection{Titolo dell'appendice}
\label{sec:app_chiave}
\input{chapters/appendixNN}

% Nel testo
si veda \cref{sec:app_chiave}      % → "appendix C"
\Cref{sec:app_chiave} descrive...   % → "Appendix C descrive..."
```

---

## 7. Note a piè di pagina

Il richiamo va in esponente **dopo** l'eventuale punteggiatura.

```latex
testo,\footnote{Nota.}
testo.\footnote{Nota.}
«citazione»\autocite[p.~nn]{key}
```

---

## 8. Titoli di opere

```latex
% Titolo descrittivo → corsivo
\textit{Les Forges de l'Invisible}
\textit{Canto a Concordu}

% Designazione di genere → tondo, senza virgolette
Sonata per violino e pianoforte in fa maggiore

% Sezione di composizione o aria → virgolette caporali
«Kyrie eleison»
«E lucevan le stelle»

% Nome di rivista → virgolette caporali
«Journal of the Audio Engineering Society»
«Rivista Italiana di Musicologia»
```

---

## 9. Elementi musicali

```latex
% Note e tonalità → minuscolo
sol, fa\#, la\textflat{} maggiore

% Indicazioni dinamiche ed espressive → minuscolo corsivo
\textit{piano}, \textit{fortissimo}, \textit{crescendo}

% Movimenti → tondo, iniziale maiuscola
l'Adagio della Sonata op.~7
```

---

## 10. Nomi autori in maiuscoletto

Per riferimenti scritti a mano, fuori da `biblatex`.

```latex
\authorname{Alvise Vidolin}
\authorname{Denis Smalley}
```

---

## 11. Figure e tabelle

Didascalie senza punto finale, allineamento centrale (già impostato in `thesis.sty`).

```latex
\begin{figure}[h]
    \centering
    \includegraphics[width=0.8\textwidth]{graphics/nomefile}
    \caption{Descrizione sintetica senza punto finale}
    \label{fig:chiave}
\end{figure}

% Riferimento nel testo
\cref{fig:chiave}      % → "figure 3"
\cref{tab:chiave}      % → "table 2"
```

---

## 12. Elenchi

```latex
\begin{itemize}
    \item[-] primo elemento
    \item[-] secondo elemento
\end{itemize}
```

---

## 13. Abbreviazioni principali

| Abbreviazione | Significato |
|---|---|
| `cfr.` | confronta |
| `cit.` | citato/a |
| `p.` / `pp.` | pagina/e |
| `vol.` / `voll.` | volume/i |
| `cap.` / `capp.` | capitolo/i |
| `a cura di` | per i curatori |
| `trad. it.` | traduzione italiana |

---

## 14. Note di lavoro (worknotes.sty)

Visibili solo in bozza. Per disattivarle tutte: impostare `\worknotesfalse` in `worknotes.sty` prima della consegna. I file dei capitoli rimangono invariati.

```latex
\notecontent{Contenuto pianificato per questa sezione.}
\noteopen{Questione aperta da risolvere prima della consegna.}
\noterefs{Riferimenti bibliografici da integrare: chiave1, chiave2.}
\notestatus{Bozza / In sviluppo / Completo.}
```

---

## 15. Appendice

Sezioni nell'indice senza numerazione:

```latex
% In thesis.tex, prima di \input{chapters/appendix01}
\chapter{Appendix}
\markboth{Appendix}{Appendix}
\setcounter{secnumdepth}{0}   % non numera le sezioni
\setcounter{tocdepth}{2}      % mostra nell'indice fino a \subsection
\input{chapters/appendix01}
```

> **Nota:** questa sezione descrive un'implementazione precedente. L'appendice attuale usa `\chapter*{Appendix}` + il comando `\appendixsection{}` (contatore dedicato `appsec`, lettere A/B/C..., voce di indice tramite `\l@appendixsec` personalizzato) descritto nella sezione 6bis. Se vuoi, posso riscrivere questa sezione 15 per allinearla all'implementazione reale in `thesis.sty`.

---

## 16. Glossario

Le voci del glossario si trovano in `frontbackmatter/glossary.tex`, gestite dal pacchetto `glossaries` (caricato in `thesis.sty` con `sort=standard, toc, nonumberlist`). Ogni voce si definisce con `\newglossaryentry`:

```latex
\newglossaryentry{beamforming}{
    name={Beamforming},
    description={Definizione del termine...}
}

\newglossaryentry{spatial}{
    name={Spatial},
    description={Definizione del termine...}
}
```

**✅ Ordinamento alfabetico automatico:** le voci possono essere scritte in QUALSIASI ordine nel file sorgente — `glossaries` le ordina da solo in fase di compilazione (opzione `sort=standard`). Non serve inserirle manualmente nella posizione corretta.

**Per termini con formattazione o simboli nel nome** (es. `HOA (\textit{Higher-Order Ambisonics})`, `QDI (\textit{...})`), aggiungi il campo `sort={...}` con il testo puro da usare come chiave di ordinamento, altrimenti il markup LaTeX interno può confondere l'algoritmo di sort:

```latex
\newglossaryentry{hoa}{
    name={HOA (\textit{Higher-Order Ambisonics})},
    sort={HOA},
    description={...}
}
```

**Nel `thesis.tex`**, il glossario si stampa così — non serve scrivere `\chapter*{Glossary}` a mano, `\printglossary` lo genera da solo (grazie all'opzione `toc`):

```latex
\input{frontbackmatter/glossary}
\printglossary[title={Glossary}]
```

**Per richiamare una voce dal corpo del testo:**

```latex
come mostra \gls{spatial}, ...
\Gls{quintina} emerge come...   % maiuscola a inizio frase, come \Cref
```

`\gls{chiave}` stampa il termine **e** crea un link cliccabile alla sua definizione nel glossario — sostituisce sia il testo che il riferimento in un unico comando.

**⚠️ Passaggio di compilazione aggiuntivo richiesto:** `makeglossaries` deve girare tra un passaggio LaTeX e l'altro, come `biber` per la bibliografia:

```
pdflatex thesis
makeglossaries thesis
pdflatex thesis
pdflatex thesis
```

Con **latexmk**, aggiungi al tuo `latexmkrc`:

```perl
add_cus_dep('glo', 'gls', 0, 'makeglossaries');
$clean_ext .= " glo gls glg";
```

---

## 17. Commenti di lavoro con data/ora (comments.sty)

Diverso da `worknotes.sty` (note strutturate per sezione): `comments.sty` serve per appunti puntuali agganciati a un momento preciso di scrittura, tipo "post-it" cronologici sparsi nel testo mentre lavori.

**⚠️ Limite tecnico:** LaTeX non può rilevare automaticamente *quando* hai scritto una riga di testo — può solo stampare la data della compilazione corrente (`\today`), che cambia ogni volta che ricompili. Per questo la data/ora va scritta a mano, come primo argomento, esattamente come un messaggio di commit.

```latex
% Commento con data/ora scritta a mano (consigliato)
\tcomment{17/03/2026, 15:40}{Verificare se questa citazione va
spostata nel Cap. 5 una volta scritto il §5.4.4.}

% Variante rapida: usa la data di compilazione corrente
% (riflette solo l'ultima ricompilazione, non quando è stato scritto davvero)
\tcommentnow{Controllare questa frase, suona strana}
```

Produce un box giallo con "Commento — [data]" come titolo e il testo del commento sotto.

**Per disattivare tutti i commenti in blocco** prima della consegna, in `comments.sty`:

```latex
\showcommentstrue   →   \showcommentsfalse
```

I file dei capitoli restano invariati — stesso principio di `\worknotesfalse` per `worknotes.sty`.