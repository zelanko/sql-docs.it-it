---
title: Funzioni e comandi Visual FoxPro non supportati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e5b8ed06ad9f996d644df0dfb99d15adcff86bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307652"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandi e funzioni Visual FoxPro non supportati (driver ODBC Visual FoxPro)
Nella tabella seguente sono elencati i comandi e le funzioni di FoxPro che non sono supportati dal driver ODBC Visual FoxPro, ma sono supportati da Microsoft® Visual FoxPro®.  
  
 Se l'applicazione interagisce con i dati le cui regole, trigger, valori predefiniti o stored procedure chiamano questi comandi o funzioni Visual FoxPro, il driver può generare un errore.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Funzioni e comandi Visual FoxPro non supportati  
  
||||  
|-|-|-|  
|#DEFINE... #UNDEF|#IF... #ENDIF direttiva per il preprocessore|#IFDEF &#124; #IFNDEF|  
|#INCLUDE direttiva per il preprocessore|Operatore di risoluzione dell'ambito::|! Comando (vedere eseguire &#124;. Comando|  
|? &#124;? Comando|??? Comando|\ &#124; \\\ comando|  
|@ ... BOX (comando)|@ ... Comando CLASS|@ ... Cancella comando|  
|@ ... Comando EDIT-Edit boxs|@ ... Comando FILL|@ ... Ottieni|  
|@ ... Comando di MENU|@ ... PROMPT dei comandi|@ ... Comando SAY|  
|@ ... SCROLL (comando)|@ ... A Command||  
  
## <a name="a"></a>Una  
  
||||  
|-|-|-|  
|Comando ACCEPT|Funzione ACLASS ()|Comando di MENU attiva|  
|ATTIVA comando POPUP|Comando attiva schermata|Comando attiva finestra|  
|Metodo ActivateCell|Aggiungi classe (comando)|Funzione ADIR ()|  
|Funzione AFONT ()|Funzione AINSTANCE ()|Variabile di memoria di sistema _ALIGNMENT|  
|Funzione AMEMBERS ()|Funzione ANSITOOEM ()|Funzione APRINTERS ()|  
|Funzione ASELOBJ ()|Comando ASSIST||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|Funzione barra ()|Funzione BARCOUNT ()|Funzione BARPROMPT ()|  
|Variabile di memoria di sistema _BEAUTIFY|Variabile di memoria di sistema _BOX|Comando Sfoglia|  
|Variabile di memoria di sistema _BROWSER|Comando Compila APP|Comando BUILD EXE|  
|Comando Compila progetto|Variabile di memoria di sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _CALCVALUE|Variabile di memoria di sistema _CLIPTEXT|Variabile di memoria di sistema _CONVERTER|  
|Variabile di memoria di sistema _CUROBJ|CHIAMA comando|Annulla comando|  
|Funzione CAPSLOCK ()|Comando CD|Comando CHANGE|  
|Comando CHDIR|Funzione CHRSAW ()|Comando Chiudi MEMO|  
|Funzione CNTBAR ()|Funzione CNTPAD ()|Funzione COL ()|  
|Compila comando|Comando Compila DATABASE|Comando Compila modulo|  
|Funzione COMPOBJ ()|Oggetto contenitore|Oggetto Control|  
|Comando copia FILE|COPY MEMO (comando)|Comando CREATE CLASS|  
|Comando CREATE CLASSLIB|Comando crea SET di colori|Crea comando|  
|Comando Crea connessione|Comando CREATE DATABASE|Comando Crea modulo|  
|Crea da comando|Comando Crea etichetta|Comando di MENU crea|  
|Comando Crea progetto|Comando crea QUERY|Comando crea REPORT|  
|Comando Crea schermata|Comando Crea vista SQL|Comando CREATE TRIGGER|  
|Comando Crea visualizzazione|Funzione CREATEOBJECT ()|Funzione CURDIR ()|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _DBLCLICK|Variabile di memoria di sistema _DIARYDATE|Funzione DBSETPROP ()|  
|Funzioni DDE|DISATTIVA comando di MENU|DISATTIVA comando POPUP|  
|DISATTIVA comando finestra|Comando DECLARE-DLL|DECLARE (comando)|  
|Comando Definisci barra|Comando Definisci casella|Comando Definisci classe|  
|Comando di MENU Definisci|Definisci comando di riempimento|Definisci comando POPUP|  
|Comando Definisci finestra|Comando Elimina connessione|Comando DELETE DATABASE|  
|Comando DELETE FILE|Comando DELETE TRIGGER|Comando Elimina visualizzazione|  
|DIR (comando)|Comando DIRECTORY|Visualizza comando|  
|Comando Visualizza connessioni|Comando Visualizza DATABASE|Comando Visualizza dll|  
|Comando Visualizza file|Comando Visualizza memoria|Comando Visualizza oggetti|  
|Comando Visualizza routine|Comando Visualizza stato|Comando Visualizza struttura|  
|Comando Visualizza tabelle|Comando Visualizza visualizzazioni|Comando DO FORM|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Modifica comando|Comando ERROR||  
|Comando ERASE|Comando esterno|Esporta comando|  
|Comando EJECT|Comando Rimuovi pagina||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _FOXDOC|Variabile di memoria di sistema _FOXGRAPH|Funzione FEOF ()|  
|Funzione FCLOSE ()|Funzione FCREATE ()|Funzione FGETS ()|  
|Funzione FERRItor ()|Funzione FFLUSH ()|Funzione FKLABEL ()|  
|FILEr (comando)|Comando trova|Funzione FOPEn ()|  
|Funzione FKMAX ()|Funzione FONTMETRIC ()|Funzione FSEEK ()|  
|Funzione FPUTS ()|FREAD () (funzione)||  
|Funzione FWRITE ()|Funzione FCHSIZE ()||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _GENGRAPH|Variabile di memoria di sistema _GENMENU|Variabile di memoria di sistema _GENPD|  
|Variabile di memoria di sistema _GENSCRN|Variabile di memoria di sistema _GENXTAB|Funzione GETBAR ()|  
|Funzione GetColor ()|Funzione GETDIR ()|Comando getexpr|  
|Funzione GETFILE ()|Funzione GETFONT ()|Funzione GetObject ()|  
|Funzione GETPAD ()|Funzione GETPICT ()|Funzione GetPrinter ()|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando della Guida|Comando Nascondi MENU|Nascondi comando POPUP|  
|Comando Nascondi finestra|HOME () (funzione)||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Funzione IMESTATUS ()|Comando IMPORT|INPUT (comando)|  
|Indice sul comando|Funzione INKEY ()|Funzione COLOR ()|  
|Inserisci comando|Funzione INSMODE ()||  
|Funzione tomouse ()|Variabile di memoria di sistema _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando JOIN|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando tastiera|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _LMARGIN|LABEL (comando)|Funzione LASTKEY ()|  
|Funzione lino ()|Elenca comandi|Comando LIST CONNECTIONs|  
|Comando LOAD|Funzione LOCFILE ()||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Funzione MCOL ()|Comando MD|Comando da MENU a|  
|Funzione MEMORY ()|Comando di MENU|Comando MKDIR|  
|Funzione MENU ()|MESSAGEBOX () (funzione)|Comando modifica connessione|  
|Comando modifica classe|Comando Modifica comando|Comando modifica modulo|  
|Comando modifica DATABASE|Comando modifica FILE|Comando modifica MEMO|  
|Modifica comando generale|Comando modifica etichetta|Comando modifica progetto|  
|Comando di MENU modifica|Comando MODIFY PROCEDURE|Comando modifica schermata|  
|Comando modifica QUERY|Comando modifica REPORT|Comando modifica finestra|  
|Comando modifica struttura|Comando modifica visualizzazione|Comando Sposta finestra|  
|Comando del MOUSE|Sposta comando POPUP|Funzione MROW ()|  
|Funzione MRKBAR ()|Funzione MRKPAD ()||  
|Funzione MWINDOW ()|Funzione MDOWN ()||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Funzione NUMLOCK ()|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Funzione OBJNUM ()|Funzione OBJTOCLIENT ()|Comando su barra|  
|Funzione OEMTOANSI ()|Comando ON APLABOUT|Comando di MENU Esci|  
|Comando di ESCAPE|Comando barra di uscita|ON KEY = comando|  
|Comando di riempimento in uscita|Comando POPUP di uscita|Comando ON PAD|  
|Comando per l'etichetta chiave|Comando ON MACHELP|Comando barra di selezione|  
|Comando della pagina|Comando ON READERROR|Comando POPUP di selezione|  
|Comando di MENU selezione|Comando per il riquadro di selezione||  
|AL comando SHUTDOWN|Funzione OBJVAR ()||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _PADVANCE|Variabile di memoria di sistema _PAGENO|Variabile di memoria di sistema _PBPAGE|  
|Variabile di memoria di sistema _PCOLNO|Variabile di memoria di sistema _PCOPIES|Variabile di memoria di sistema _PDRIVER|  
|Variabile di memoria di sistema _PDSETUP|Variabile di memoria di sistema _PECODE|Variabile di memoria di sistema _PEJECT|  
|Variabile di memoria di sistema _PEPAGE|Variabile di memoria di sistema _PLENGTH|Variabile di memoria di sistema _PLINENO|  
|Variabile di memoria di sistema _PLOFFSET|Variabile di memoria di sistema _PPITCH|Variabile di memoria di sistema _PQUALITY|  
|Variabile di memoria di sistema _PRETEXT|Variabile di memoria di sistema _PSCODE|Variabile di memoria di sistema _PSPACING|  
|Variabile di memoria di sistema _PWAIT|Comando PACK DATABASE|Funzione PAD ()|  
|Funzione PCOL ()|Funzione PEMSTATUS ()|Comando Riproduci MACRO|  
|Comando POP KEY|Comando MENU POP|Comando POP POPUP|  
|Funzione POPUP ()|PRINTJOB... Comando ENDPRINTJOB|Funzione PRINTSTATUS ()|  
|Funzione PRMBAR ()|Funzione PRMPAD ()|Funzione PROMPT ()|  
|Funzione prora ()|Funzione PRTINFO ()|Comando PUSH KEY|  
|Comando di MENU PUSH|Comando POPUP PUSH|Funzione PUTFILE ()|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|QUIT-comando|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _RMARGIN|Comando RD|Funzione READKEY ()|  
|Comando READ|Comando di MENU READ|Comando della barra della versione|  
|Funzione REFRESH ()|Comando REINDEX|RELEASE LIBRARY (comando)|  
|Comando RELEASE CLASSLIB|Comando RELEASE|Comando RELEASE PAD|  
|Comando menu versione|Comando RELEASE MODULE|Comando rilascia WINDOWS|  
|Comando rilascia POPUP|Comando RELEASE PROCEDURE|Rinomina comando|  
|Comando Rimuovi classe|Comando Rinomina classe|Comando Rinomina visualizzazione|  
|Comando Rinomina connessione|Comando Rinomina tabella|Comando RESTOre FROM|  
|Comando REPORT|Funzione Requery ()|Comando Ripristina finestra|  
|Comando RESTOre MACROs|Comando Ripristina schermata|Funzione RGBSCHEME ()|  
|RESUME (comando)|Funzione RGB ()|ESEGUIRE &#124;. Comando|  
|Comando RMDIR|ROW () (funzione)||  
|Comando RUNSCRIPT|Funzione RDLEVEL ()||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Comando SAVE MACROs|Comando Salva schermata|Salva in comando|  
|Salva comando WINDOWS|Funzione SCHEME ()|Funzione SCOLS ()|  
|SCROLL (comando)|Variabile di memoria di sistema _SCREEN|IMPOSTA comando|  
|IMPOSTA comando alternativo|SET ANSI (comando)|Comando SET APLABOUT|  
|IMPOSTA comando salvataggio automatico|SET BELL (comando)|IMPOSTA comando BLINK|  
|SET BORDER (comando)|Comando SET BRSTATUS|Comando SET CLASSLIB|  
|SET CLEAR (comando)|Comando SET CLOCK|IMPOSTA il colore del comando|  
|Imposta colore del comando Schema|IMPOSTA il comando set colori|Imposta colore su comando|  
|IMPOSTA il comando compatibile|IMPOSTA comando conferma|IMPOSTA comando CONSOLE|  
|IMPOSTA CPCOMPILE|IMPOSTA CPDIALOG|Comando Imposta valuta|  
|Comando imposta cursore|IMPOSTA comando DataSession|SET DEBUG-comando|  
|IMPOSTA comando decimali|IMPOSTA comando delimitatori|IMPOSTA comando di sviluppo|  
|Comando Imposta dispositivo|IMPOSTA comando Visualizza|Comando SET DOHISTORY|  
|IMPOSTA comando ECHO|IMPOSTA comando ESCAPE|Comando SET FORMAT|  
|Comando SET FUNCTION|Comando imposta intestazioni|IMPOSTA comando della Guida|  
|Comando SET HELPFILTER|Comando Imposta intensità|Comando Imposta chiave|  
|Imposta comando per la configurazione|Comando SET LOGERRORS|Comando SET MACDESKTOP|  
|Comando SET MACHELP|IMPOSTA comando MACKEY|Comando SET MARGIN|  
|SET MARK OF Command|Imposta contrassegno su comando|Comando SET MEMOWIDTH|  
|Comando imposta messaggio|IMPOSTA comando MOUSE|SET odometro (comando)|  
|IMPOSTA il comando OLEOBJECT|Comando imposta TAVOLOzza|Comando SET PDSETUP|  
|Comando SET POINT|Comando Imposta stampante|Comando SET READBORDER|  
|SET REFRESH (comando)|Comando SET RESOURCE|Comando Imposta sicurezza|  
|IMPOSTA comando SEGNAPUNTi|Comando imposta secondi|IMPOSTA SEPARATOre (comando)|  
|Comando SET SHADOWs|SET SKIP OF Command|Comando imposta spazio|  
|Comando imposta stato|Comando imposta barra di stato|Comando SET STEP|  
|IMPOSTA comando STICKY|Comando SET SYSFORMATS|Comando SET SYSMENU|  
|IMPOSTA comando TALK|Comando SET TEXTMERGE|IMPOSTA comando delimitatori TEXTMERGE|  
|Comando imposta argomento|Comando imposta ID argomento|Comando SET TRBETWEEN|  
|Comando SET TYPEAHEAD|Comando imposta visualizzazione|IMPOSTARE la finestra del comando MEMO|  
|Comando SET XCMDFILE|Variabile di memoria di sistema _SHELL|Mostra comando GET|  
|Mostra comando ottiene|Mostra comando di MENU|Mostra comando oggetto|  
|Mostra comando POPUP|Mostra comando finestra|Comando POPUP dimensioni|  
|Comando finestra dimensioni|Funzione SKPBAR ()|Funzione SKPPAD ()|  
|Funzione SOUNDEX ()|Variabile di memoria di sistema _SPELLCHK|Funzioni SQL|  
|Funzione SROWS ()|Variabile di memoria di sistema _STARTUP|SOSPENDi comando|  
|Funzioni SYS () ad eccezione di SYS (2011)|Funzione SYSMETRIC ()||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _TABS|TESTO... Comando ENDTEXT|Funzione TXTWIDTH ()|  
|Funzione TRANSFORM ()|Variabile di memoria di sistema _TRANSPORT||  
|Comando di tipo|Variabile di memoria di sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Funzione UPDATED ()|Comando USE||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Comando VALIDATE DATABASE|Funzione VARREAD ()|Funzione VERSION ()|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _WINDOWS|Variabile di memoria di sistema _WIZARD|Funzione WCHILD ()|  
|Comando WAIT|Funzione WBORDER ()|Funzione WFONT ()|  
|Funzione WCOLS ()|Funzione WEXIST ()|Funzione WLROW ()|  
|CON... Comando ENDWITH|Funzione WLAST ()|Funzione WONTOP ()|  
|Funzione WMAXIMUM ()|Funzione WLCOL ()|Funzione WREAD ()|  
|Funzione WOUTPUT ()|Funzione WMINIMUM ()|Funzione WVISIBLE ()|  
|Funzione WPARENT ()|Funzione WTITLE ()||  
|Funzione WROWS ()|Variabile di memoria di sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando della finestra ZOOM|||
