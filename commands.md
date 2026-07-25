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

```latex
% Definire l'etichetta (punto di destinazione)
\chapter{Titolo}
\label{cap:chiave}

\section{Titolo}
\label{sec:chiave}

\subsection{Titolo}
\label{subsec:chiave}

% Richiamare nel testo (~ = spazio non separabile)
Capitolo~\ref{cap:chiave}
la sezione~\ref{sec:chiave}
cfr.~§~\ref{subsec:chiave}
p.~\pageref{sec:chiave}

% Esempio completo
come si discuterà nel Capitolo~\ref{cap:interprete} (p.~\pageref{cap:interprete})
```

> **Nota:** LaTeX risolve i `\ref` in due passate di compilazione. Se compare `??` nel PDF, ricompilare.

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
la Figura~\ref{fig:chiave}
la Tabella~\ref{tab:chiave}
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