---
title: I comandi di Visual FoxPro e funzioni non supportate | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db6aff35944b8811e79627c6076ab61e838edf3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912326"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandi e funzioni Visual FoxPro non supportati (driver ODBC Visual FoxPro)
Nella tabella seguente elenca i comandi di FoxPro e funzioni che non sono supportate dal Driver ODBC Visual FoxPro ma supportate da Microsoft® Visual FoxPro.  
  
 Se l'applicazione interagisce con i dati cui le regole, trigger, valori predefiniti o le stored procedure chiamano questi comandi di Visual FoxPro o funzioni, il driver può generare un errore.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Funzioni e i comandi di Visual FoxPro non supportati  
  
||||  
|-|-|-|  
|#DEFINE #UNDEF|... #IF #ENDIF direttiva del preprocessore|#IFDEF &#124; #IFNDEF|  
|#INCLUDE (direttiva del preprocessore)|:: Operatore di risoluzione dell'ambito|! Comando (vedere eseguire &#124; . Comando)|  
|? &#124; ?? Comando|??? Comando|\ &#124; \\\ Comando|  
|@ ... FINESTRA comando|@ ... Comando di classe|@ ... Comando CLEAR|  
|@ ... Modifica - comando caselle di modifica|@ ... COMPILARE comandi|@ ... GET|  
|@ ... Comando di MENU|@ ... Prompt dei comandi|@ ... Ad esempio di comando|  
|@ ... Comando di scorrimento|@ ... AL comando||  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ACCETTARE i comandi|Funzione ACLASS)|Attiva comando di MENU|  
|Attiva comando POPUP|ATTIVARE il comando dello schermo|ATTIVARE la finestra di comando|  
|Metodo ActivateCell|Comando Aggiungi classe|ADIR () (funzione)|  
|Funzione AFONT)|Funzione AINSTANCE)|Variabile di memoria di sistema _ALIGNMENT|  
|Funzione AMEMBERS)|Funzione ANSITOOEM)|Funzione APRINTERS)|  
|Funzione ASELOBJ)|Comando ASSIST||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|BARRA () (funzione)|Funzione BARCOUNT)|Funzione BARPROMPT)|  
|Variabile di memoria di sistema _BEAUTIFY|Variabile di memoria di sistema _BOX|Sfoglia comando|  
|Variabile di memoria di sistema browser|COMPILARE APP comando|Comando EXE di compilazione|  
|Comando di progetto di compilazione|Variabile di memoria di sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _CALCVALUE|Variabile di memoria di sistema _CLIPTEXT|Variabile di memoria di sistema _CONVERTER|  
|Variabile di memoria di sistema _CUROBJ|Comando di chiamata|Comando CANCEL|  
|CAPSLOCK () (funzione)|Comando CD|Comando di modifica|  
|Comando CHDIR|Funzione CHRSAW)|Comando Chiudi promemoria|  
|Funzione CNTBAR)|Funzione CNTPAD)|Funzione di COL)|  
|Comando di compilazione|COMPILARE comandi DATABASE|FORM comando di compilazione|  
|Funzione COMPOBJ)|Oggetto contenitore|Oggetto di controllo|  
|COPIARE i FILE (comando)|Comando COPY di credito|CLASSE comando CREATE|  
|Comando CLASSLIB CREATE|CREARE SET di colori (comando)|Comando CREATE|  
|CREARE il comando di connessione|CREARE il comando DATABASE|FORM comando CREATE|  
|Il nome di comando|Crea comando etichetta|CREARE il comando MENU|  
|CREARE il comando di progetto|CREARE il comando QUERY|CREARE REPORT comando|  
|CREARE il comando dello schermo|CREARE il comando di visualizzazione SQL|CREARE TRIGGER comando|  
|CREARE il comando di visualizzazione|Funzione CREATEOBJECT)|Funzione CURDIR)|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _DBLCLICK|Variabile di memoria di sistema _DIARYDATE|Funzione DBSETPROP)|  
|Funzioni DDE|DISATTIVARE il comando MENU|DISATTIVARE comando POPUP|  
|DISATTIVARE la finestra di comando|DICHIARARE - comando DLL|DICHIARARE comando|  
|DEFINIRE della barra di comando|DEFINIRE finestra comando|DEFINIRE comandi di classe|  
|DEFINIRE comandi MENU|DEFINIRE comandi di riempimento|DEFINIRE comandi POPUP|  
|DEFINIRE una finestra di comando|CONNESSIONE comando DELETE|Elimina i comandi DATABASE|  
|Elimina FILE (comando)|Comando TRIGGER DELETE|Comando di visualizzazione DELETE|  
|Comando DIR|Comando della DIRECTORY|Comando di visualizzazione|  
|Comando di visualizzazione connessioni|Comando di visualizzazione del DATABASE|Comando DLL di visualizzazione|  
|VISUALIZZAZIONE file (comando)|Comando memoria visualizzazione|VISUALIZZARE gli oggetti comando|  
|Comando procedure visualizzazione|Comando dello stato di visualizzazione|Comando struttura di visualizzazione|  
|Comando di visualizzazione tabelle|Comando di visualizzazione viste|FORM comando|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Comando di modifica|Errore del comando||  
|Comando Cancella|Comando esterno|Comando di esportazione|  
|Rimuovi comando|Rimuovi comando pagina||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _FOXDOC|Variabile di memoria di sistema _FOXGRAPH|FEOF (funzione))|  
|FCLOSE (funzione))|Funzione FCREATE)|FGETS (funzione))|  
|FERROR (funzione))|FFLUSH (funzione))|Funzione FKLABEL)|  
|Comando di filtro|Comando Trova|Funzione FOPEN)|  
|Funzione FKMAX)|Funzione FONTMETRIC)|FSEEK (funzione))|  
|FPUTS () (funzione)|FREAD (funzione))||  
|FWRITE (funzione))|Funzione FCHSIZE)||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _GENGRAPH|Variabile di memoria di sistema _GENMENU|Variabile di memoria di sistema _GENPD|  
|Variabile di memoria di sistema _GENSCRN|Variabile di memoria di sistema _GENXTAB|Funzione GETBAR)|  
|GETCOLOR () (funzione)|Funzione GETDIR)|Comando GETEXPR|  
|Funzione GETFILE)|GETFONT () (funzione)|Funzione GETOBJECT)|  
|Funzione GETPAD)|Funzione GETPICT)|Funzione GETPRINTER)|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando?|NASCONDERE i comandi MENU|Nascondi comando POPUP|  
|Nascondi finestra di comando|HOME () (funzione)||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Funzione IMESTATUS)|Comando IMPORT|Comandi di INPUT|  
|Indice in comando|Funzione INKEY)|Funzione ISCOLOR)|  
|Comando di inserimento|Funzione INSMODE)||  
|Funzione ISMOUSE)|Variabile di memoria di sistema rientro||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|AGGIUNTA di comandi|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando di tasti|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _LMARGIN|Comando etichetta|Funzione LASTKEY)|  
|Funzione LINENO)|ELENCO comandi|Comando ELENCA le connessioni|  
|Comando di caricamento|Funzione LOCFILE)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Funzione MCOL)|Comando MD|MENU al comando|  
|Funzione () di memoria|Comando di MENU|Comando MKDIR|  
|Funzione () dal MENU|Funzione MESSAGEBOX)|MODIFICARE il comando di connessione|  
|MODIFICARE il comando di classe|MODIFICARE il comando di comando|MODIFICARE il comando di FORM|  
|MODIFICARE il comando di DATABASE|MODIFICARE i FILE (comando)|MODIFICARE il comando di credito|  
|MODIFICARE il comando generale|MODIFICARE il comando etichetta|MODIFICARE il comando di progetto|  
|MODIFICARE il comando di MENU|MODIFICARE il comando di PROCEDURE|Comando SCHERMATA di modifica|  
|MODIFICARE il comando di QUERY|MODIFICARE il comando di REPORT|Modifica finestra di comando|  
|MODIFICARE il comando di struttura|Comando di visualizzazione di modifica|Spostamento finestra (comando)|  
|Comandi del MOUSE|Comando POPUP di spostamento|Funzione MROW)|  
|Funzione MRKBAR)|Funzione MRKPAD)||  
|Funzione MWINDOW)|Funzione MDOWN)||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Funzione di BLOCNUM)|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Funzione OBJNUM)|Funzione OBJTOCLIENT)|VIA della barra di comando|  
|Funzione () non vengono|NEL comando APLABOUT|Comando MENU EXIT ON|  
|NEL comando di ESCAPE|IN uscita della barra dei comandi|CHIAVE = comando|  
|Comando PAD uscita ON|Comando POPUP uscita ON|Comando PAD ON|  
|NEL comando di tasti etichetta|NEL comando MACHELP|NELLA selezione della barra dei comandi|  
|Nella pagina di comando|NEL comando READERROR|NEL comando POPUP di selezione|  
|NEL comando di MENU di selezione|NEL comando riquadro selezione||  
|NEL comando di arresto|Funzione OBJVAR)||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _PADVANCE|Variabile di memoria di sistema _PAGENO|Variabile di memoria di sistema _PBPAGE|  
|Variabile di memoria di sistema _PCOLNO|Variabile di memoria di sistema _PCOPIES|Variabile di memoria di sistema _PDRIVER|  
|Variabile di memoria di sistema _PDSETUP|Variabile di memoria di sistema _PECODE|Variabile di memoria di sistema _PEJECT|  
|Variabile di memoria di sistema _PEPAGE|Variabile di memoria di sistema _PLENGTH|Variabile di memoria di sistema _PLINENO|  
|Variabile di memoria di sistema _PLOFFSET|Variabile di memoria di sistema _PPITCH|Variabile di memoria di sistema _PQUALITY|  
|Variabile di memoria di sistema _PRETEXT|Variabile di memoria di sistema _PSCODE|Variabile di memoria di sistema _PSPACING|  
|Variabile di memoria di sistema _PWAIT|Comando DATABASE di Service PACK|Funzione di riempimento)|  
|Funzione PCOL)|Funzione PEMSTATUS)|Comando di riproduzione (macro)|  
|Comando POP chiave|Comando di MENU POP|Comando POPUP POP|  
|POPUP () (funzione)|PRINTJOB... Comando ENDPRINTJOB|Funzione PRINTSTATUS)|  
|Funzione PRMBAR)|Funzione PRMPAD)|Messaggio di richiesta () (funzione)|  
|Funzione PROW)|Funzione PRTINFO)|Comando di tasti PUSH|  
|Comando di MENU PUSH|Comando POPUP PUSH|Funzione PUTFILE)|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando QUIT|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _RMARGIN|Comando di desktop remoto|Funzione READKEY)|  
|LEGGERE il comando|LETTURA di comando di MENU|VERSIONE della barra dei comandi|  
|Refresh() (funzione)|REINDICIZZARE comando|Comando LIBRARY versione|  
|Comando CLASSLIB versione|Comando versione|Comando blocco note di rilascio|  
|Comando menu di rilascio|VERSIONE modulo comando|Comando di WINDOWS versione|  
|Comando popup di rilascio|PROCEDURE di rilascio (comando)|Il comando di RIDENOMINAZIONE|  
|CLASSE comando Rimuovi|CLASSE comando RENAME|Il comando di visualizzazione di RIDENOMINAZIONE|  
|Il comando di connessione di RIDENOMINAZIONE|RINOMINARE tabella comandi|RIPRISTINO dal comando|  
|Comando REPORT|Rieseguire una query () (funzione)|FINESTRA di comando di ripristino|  
|MACRO comando RESTORE|SCHERMATA comando RESTORE|Funzione RGBSCHEME)|  
|Comando Riprendi|Funzione RGB)|RUN &#124; ! Comando|  
|Comando RMDIR|Funzione di riga)||  
|Comando RUNSCRIPT|Funzione RDLEVEL)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|SALVARE le macro di comandi|SALVARE i comandi dello schermo|SALVARE in comando|  
|SALVARE i comandi di WINDOWS|Funzione di combinazione)|Funzione SCOLS)|  
|Comando di scorrimento|Variabile di memoria di sistema schermo|SET (comando)|  
|SET ALTERNATIVO (comando)|SET ANSI (comando)|Comando APLABOUT SET|  
|SET di comandi di salvataggio automatico|SET (comando) a forma di CAMPANA|SET (comando) per il LAMPEGGIAMENTO|  
|Comando SET del bordo|Comando BRSTATUS SET|Comando CLASSLIB SET|  
|Comando CLEAR SET|SET di comandi di orologio|IMPOSTARE il colore del comando|  
|IMPOSTARE il colore del comando di schema|SET di colori SET (comando)|IMPOSTARE il colore al comando|  
|SET di comandi compatibile|Comando conferma SET|Comando della CONSOLE insieme|  
|SET CPCOMPILE|SET CPDIALOG|Comando valuta SET|  
|Comando SET del cursore|Comando DATASESSION SET|SET di comandi DEBUG|  
|SET di numeri DECIMALI comando|SET di DELIMITATORI comando|SET di comandi di sviluppo|  
|Comando SET di dati del dispositivo|VISUALIZZAZIONE di SET (comando)|Comando DOHISTORY SET|  
|Comando ECHO SET|SET di comandi ESCAPE|FORMATO di SET (comando)|  
|Comando SET (funzione)|SET di intestazioni comando|SET (comando) della Guida|  
|Comando HELPFILTER SET|Comando intensità SET|Comando chiave SET|  
|Comando KEYCOMP SET|Comando LOGERRORS SET|Comando MACDESKTOP SET|  
|Comando MACHELP SET|Comando MACKEY SET|Comando margine SET|  
|CONTRASSEGNARE i SET di comandi|MARK di SET di comandi|Comando MEMOWIDTH SET|  
|SET (comando) messaggio|Comando SET del MOUSE|Comando CONTACHILOMETRI SET|  
|Classi OLEOBJECT SET (comando)|TAVOLOZZA di SET (comando)|Comando PDSETUP SET|  
|Comando Imposta punto|SET (comando) della stampante|Comando READBORDER SET|  
|Comando REFRESH SET|Comando RESOURCE SET|Comando SAFETY SET|  
|Comando TABELLONE SET|SET (comando) secondi|Comando separatore SET|  
|Comando SHADOWS SET|Ignora SET di comandi|SET (comando) dello spazio|  
|Comando STATUS SET|IMPOSTARE lo stato della barra dei comandi|PASSAGGIO di SET (comando)|  
|SET permanenti (comando)|Comando SYSFORMATS SET|Comando SYSMENU SET|  
|Comando TALK SET|Comando TEXTMERGE SET|Comando DELIMITATORI TEXTMERGE SET|  
|ARGOMENTO di SET (comando)|Comando ID argomento di SET|Comando TRBETWEEN SET|  
|Comando TYPEAHEAD SET|Comando di visualizzazione di SET|FINESTRA di comando di credito|  
|Comando XCMDFILE SET|Variabile di memoria di sistema _SHELL|Comando GET SHOW|  
|Comando Ottiene SHOW|Comando di MENU SHOW|Comando dell'oggetto SHOW|  
|Comando POPUP SHOW|Mostra finestra di comando|Comando POPUP delle dimensioni|  
|FINESTRA di dimensioni comando|Funzione SKPBAR)|Funzione SKPPAD)|  
|Funzione SOUNDEX)|Variabile di memoria di sistema _SPELLCHK|Funzioni SQL|  
|Funzione SROWS)|Variabile di memoria di sistema Startup|Comando di sospensione|  
|Funzioni sys() eccetto SYS(2011)|Funzione SYSMETRIC)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _TABS|TESTO... Comando ENDTEXT|Funzione TXTWIDTH)|  
|TRANSFORM () (funzione)|Variabile di memoria di sistema _TRANSPORT||  
|Comando TYPE|Variabile di memoria di sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|(Funzione) (aggiornate)|USARE il comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Comando DATABASE di convalida|Funzione VARREAD)|Funzione di versione)|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema Windows|Variabile di memoria di sistema _WIZARD|Funzione WCHILD)|  
|Comando di attesa|Funzione WBORDER)|Funzione WFONT)|  
|Funzione WCOLS)|Funzione WEXIST)|Funzione WLROW)|  
|CON... Comando ENDWITH|Funzione WLAST)|Funzione WONTOP)|  
|Funzione WMAXIMUM)|Funzione WLCOL)|Funzione WREAD)|  
|Funzione WOUTPUT)|Funzione WMINIMUM)|Funzione WVISIBLE)|  
|Funzione WPARENT)|Funzione WTITLE)||  
|Funzione WROWS)|Variabile di memoria di sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZOOM finestra di comando|||
