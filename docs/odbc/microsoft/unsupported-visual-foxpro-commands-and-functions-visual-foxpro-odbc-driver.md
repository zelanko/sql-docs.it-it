---
title: Comandi e funzioni di Visual FoxPro non supportati Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307652"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandi e funzioni Visual FoxPro non supportati (driver ODBC Visual FoxPro)
Nella tabella seguente sono elencati i comandi e le funzioni FoxPro non supportati dal driver ODBC di Visual FoxPro ma supportati da Microsoft® Visual FoxPro®.  
  
 Se l'applicazione interagisce con dati le cui regole, trigger, valori predefiniti o stored procedure chiamano questi comandi o funzioni di Visual FoxPro, il driver può generare un errore.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Comandi e funzioni di Visual FoxPro non supportati  
  
||||  
|-|-|-|  
|#DEFINE ... #UNDEF|#IF ... direttiva per il preprocessore #ENDIF|#IFNDEF &#124; #IFDEF|  
|#INCLUDE direttiva per il preprocessore|:: Operatore di risoluzione dell'ambito|! Comando (vedere RUN &#124; ! Comando)|  
|? &#124; ?? Comando|??? Comando|Comando \\&#124; e|  
|@ ... Comando BOX|@ ... Comando CLASS|@ ... Comando CLEAR|  
|@ ... MODIFICA - Comando Modifica caselle|@ ... Comando FILL|@ ... Ottieni|  
|@ ... Comando MENU|@ ... Comando PROMPT|@ ... Comando SAY|  
|@ ... Comando SCROLL|@ ... Comando TO||  
  
## <a name="a"></a>Una  
  
||||  
|-|-|-|  
|Comando ACCEPT|Funzione ACLASS( )|Comando ACTIVATE MENU|  
|COMANDO ACTIVATE POPUP|Comando ACTIVATE SCREEN|Comando ACTIVATE WINDOW|  
|Metodo ActivateCell|Comando AGGIUNGI CLASS|Funzione ADIR( )|  
|Funzione AFONT( )|Funzione AINSTANCE( )|_ALIGNMENT variabile di memoria di sistema|  
|Funzione AMEMBERS( )|Funzione ANSITOOEM( )|Funzione APRINTERS( )|  
|Funzione ASELOBJ( )|Comando ASSIST||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|Funzione BAR( )|Funzione BARCOUNT( )|Funzione BARPROMPT( )|  
|_BEAUTIFY variabile di memoria di sistema|_BOX variabile di memoria di sistema|Comando BROWSE|  
|Variabile di memoria di sistema _BROWSER|Comando BUILD APP|Comando EXE BUILD|  
|Comando BUILD PROJECT|_BUILDER variabile di memoria di sistema||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|_CALCVALUE variabile di memoria di sistema|_CLIPTEXT variabile di memoria di sistema|_CONVERTER variabile di memoria di sistema|  
|_CUROBJ variabile di memoria di sistema|Comando CALL|Comando CANCEL|  
|Funzione CAPSLOCK( )|Comando CD|Comando CHANGE|  
|Comando CHDIR|Funzione CHRSAW( )|Comando CLOSE MEMO|  
|Funzione CNTBAR( )|Funzione CNTPAD( )|Funzione COL( )|  
|Comando COMPILE|Comando COMPILE DATABASE|Comando COMPILE FORM|  
|Funzione COMPOBJ( )|Oggetto Container|Oggetto Control|  
|Comando COPY FILE|Comando COPY MEMO|Comando CREATE CLASS|  
|Comando CREATE CLASSLIB|Comando CREATE COLOR SET|Comando CREATE|  
|Comando CREATE CONNECTION|Comando CREATE DATABASE|Comando CREATE FORM|  
|Comando CREATE FROM|Comando CREATE LABEL|Comando CREATE MENU|  
|Comando CREATE PROJECT|Comando CREATE QUERY|Comando CREATE REPORT|  
|Comando CREATE SCREEN|Comando CREATE SQL VIEW|Comando CREATE TRIGGER|  
|Comando CREATE VIEW|Funzione CREATEOBJECT( )|Funzione CURDIR( )|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|_DBLCLICK variabile di memoria di sistema|_DIARYDATE variabile di memoria di sistema|DbSETPROP( ) (funzione)|  
|Funzioni DDE|Comando DEACTIVATE MENU|Comando DEACTIVATE POPUP|  
|Deactivate WINDOW (comando)|DECLARE - Comando DLL|Comando DECLARE|  
|Comando DEFINE BAR|Comando DEFINE BOX|Comando DEFINE CLASS|  
|Comando DEFINE MENU|Comando DEFINE PAD|Comando DEFINE POPUP|  
|Comando DEFINE WINDOW|Comando DELETE CONNECTION|Comando DELETE DATABASE|  
|Comando DELETE FILE|Comando DELETE TRIGGER|Comando DELETE VIEW|  
|Comando DIR|Comando DIRECTORY|Comando DISPLAY|  
|COMANDO DISPLAY CONNECTIONS|Comando DISPLAY DATABASE|Comando DLLS DISPLAY|  
|Comando FILE DISPLAY|COMANDO DISPLAY MEMORY|COMANDO OGGETTI DISPLAY|  
|Comando DISPLAY PROCEDURES|COMANDO DISPLAY STATUS|Comando DISPLAY STRUCTURE|  
|Comando DISPLAY TABLES|Comando DISPLAY VIEWS|Comando DO FORM|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Comando MODIFICA|Comando ERROR||  
|Comando ERASE|Comando EXTERNAL|Comando EXPORT|  
|Comando EJECT|Comando EJECT PAGE||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _FOXDOC|_FOXGRAPH variabile di memoria di sistema|Funzione FEOF( )|  
|FCLOSE( ) Funzione|Funzione FCREATE( )|Funzione FGETS( )|  
|Funzione FERROR( )|FFLUSH( ) (funzione)|Funzione FKLABEL( )|  
|Comando FILER|Comando TROVA|Funzione FOPEN( )|  
|Funzione FKMAX( )|Funzione FONTMETRIC( )|Funzione FSEEK( )|  
|FPUT( ) Funzione|Funzione FREAD( )||  
|Funzione FWRITE( )|Funzione FCHSI-E( )||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH variabile di memoria di sistema|Variabile di memoria di sistema _GENMENU|_GENPD variabile di memoria di sistema|  
|_GENSCRN variabile di memoria di sistema|_GENXTAB variabile di memoria di sistema|Funzione GETBAR( )|  
|Funzione GETCOLOR( )|Funzione GETDIR( )|Comando GETEXPR|  
|Funzione GETFILE( )|Funzione GETFONT( )|Funzione GETOBJECT( )|  
|Funzione GETPAD( )|Funzione GETPICT( )|Funzione GETPRINTER( )|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando HELP|Comando HIDE MENU|Comando HIDE POPUP|  
|Comando HIDE WINDOW|Funzione HOME( )||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Funzione IMESTATUS( )|Comando IMPORTA|Comando INPUT|  
|Comando INDEX ON|Funzione INKEY( )|Funzione ISCOLOR( )|  
|Comando INSERT|Funzione INSMODE( )||  
|Funzione ISMOUSE( )|Variabile di memoria di sistema _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando JOIN|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando TASTIERA|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN variabile di memoria di sistema|Comando LABEL|Funzione LASTKEY( )|  
|Funzione LINENO( )|Comandi LIST|Comando LIST CONNECTIONS|  
|Comando LOAD|Funzione LOCFILE( )||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Funzione MCOL( )|Comando MD|Comando MENU TO|  
|Funzione MEMORY( )|Comando MENU|Comando MKDIR|  
|Funzione MENU( )|Funzione MESSAGEBOX( )|Comando MODIFY CONNECTION|  
|Comando MODIFY CLASS|MODIFY COMMAND Command|Comando MODIFY FORM|  
|Comando MODIFY DATABASE|Comando MODIFY FILE|Comando MODIFY MEMO|  
|Comando MODIFY GENERAL|Comando MODIFY LABEL|Comando MODIFY PROJECT|  
|Comando MENU MODIFY|Comando MODIFY PROCEDURE|Comando MODIFY SCREEN|  
|Comando MODIFY QUERY|Comando MODIFY REPORT|Comando MODIFY WINDOW|  
|Comando MODIFY STRUCTURE|Comando MODIFY VIEW|Comando MOVE WINDOW|  
|Comando MOUSE|Comando MOVE POPUP|Funzione MROW( )|  
|Funzione MRKBAR( )|Funzione MRKPAD( )||  
|Funzione MWINDOW( )|Funzione MDOWN( )||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Funzione NUMLOCK( )|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Funzione OBJNUM( )|OBJTOCLIENT( ) Funzione|Comando ON BAR|  
|Funzione OEMTOANSI( )|Comando ON APLABOUT|Comando ON EXIT MENU|  
|Comando ON ESCAPE|ON EXIT BAR Comando|ON KEY - Comando|  
|Comando ON EXIT PAD|Comando ON EXIT POPUP|Comando ON PAD|  
|Comando ON KEY LABEL|Comando MACHELP SU|Comando ON SELECTION BAR|  
|Comando ON PAGE|On READERROR Comando|Comando ON SELECTION POPUP|  
|Comando ON SELECTION MENU|Comando ON SELECTION PAD||  
|Comando ON SHUTDOWN|Funzione OBJVAR( )||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE variabile di memoria di sistema|_PAGENO variabile di memoria di sistema|_PBPAGE variabile di memoria di sistema|  
|_PCOLNO variabile di memoria di sistema|_PCOPIES variabile di memoria di sistema|_PDRIVER variabile di memoria di sistema|  
|_PDSETUP variabile di memoria di sistema|_PECODE variabile di memoria di sistema|_PEJECT variabile di memoria di sistema|  
|_PEPAGE variabile di memoria di sistema|Variabile di memoria di sistema _PLENGTH|_PLINENO variabile di memoria di sistema|  
|_PLOFFSET variabile di memoria di sistema|_PPITCH variabile di memoria di sistema|_PQUALITY variabile di memoria di sistema|  
|_PRETEXT variabile di memoria di sistema|_PSCODE variabile di memoria di sistema|_PSPACING variabile di memoria di sistema|  
|_PWAIT variabile di memoria di sistema|Comando PACK DATABASE|Funzione PAD( )|  
|Funzione PCOL( )|Funzione PEMSTATUS( )|Comando RIPRODUCI MACRO|  
|Comando CHIAVE POP|Comando POP MENU|Comando POP POPUP|  
|Funzione POPUP( )|Printjob... Comando ENDPRINTJOB|Funzione PRINTSTATUS( )|  
|Funzione PRMBAR( )|Funzione PRMPAD( )|Funzione PROMPT( )|  
|Funzione PROW( )|Funzione PRTINFO( )|Comando PUSH KEY|  
|Comando MENU PUSH|Comando PUSH POPUP|Funzione PUTFILE( )|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando QUIT|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN variabile di memoria di sistema|Comando Desktop remoto|Funzione READKEY( )|  
|Comando READ|Comando READ MENU|Release COMANDO BAR|  
|Funzione REFRESH()|Comando REINDEX|Comando RELEASE LIBRARY|  
|Comando CLASSLIB RELEASE|Comando RELEASE|Comando RELEASE PAD|  
|Comando RELEASE MENUS|Release MODULO Comando|Release COMANDO WINDOWS|  
|Comando RELEASE POPUPS|Comando RELEASE PROCEDURE|Comando RENAME|  
|Comando REMOVE CLASS|Comando RENAME CLASS|Comando RENAME VIEW|  
|Comando RENAME CONNECTION|Comando RENAME TABLE|Comando RESTORE FROM|  
|Comando REPORT|Funzione REQUERY( )|Comando RESTORE WINDOW|  
|Comando MACRO RESTORE|Comando RESTORE SCREEN|Funzione RGBSCHEME( )|  
|Comando RESUME|Funzione RGB( )|&#124; RUN ! Comando|  
|Comando RMDIR|Funzione ROW( )||  
|Comando RUNSCRIPT|Funzione RDLEVEL( )||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Comando SALVA MACROS|Comando SAVE SCREEN|Comando SALVA TO|  
|Comando SAVE WINDOWS|Funzione SCHEME( )|SCOLS( ) (funzione)|  
|Comando SCROLL|_SCREEN variabile di memoria di sistema|Comando SET|  
|Comando SET ALTERNATE|SET ANSI (comando)|Comando SET APLABOUT|  
|Comando SET AUTOSAVE|Comando SET BELL|Comando SET BLINK|  
|Comando SET BORDER|Comando SET BRSTATUS|Comando SET CLASSLIB|  
|Comando SET CLEAR|Comando SET CLOCK|COMANDO SET COLOR OF|  
|Comando SET COLOR OF SCHEME|Comando SET COLOR SET|Comando SET COLOR TO|  
|Comando SET COMPATIBLE|Comando SET CONFIRM|Comando SET CONSOLE|  
|IMPOSTA CPCOMPILE|IMPOSTA CPDIALOG|Comando SET CURRENCY|  
|Comando SET CURSOR|Comando SET DATASESSION|Comando SET DEBUG|  
|Comando SET DECIMALS|Comando SET DELIMITERS|Comando SET DEVELOPMENT|  
|Comando SET DEVICE|Comando SET DISPLAY|Comando SET DOHISTORY|  
|Comando SET ECHO|Comando SET ESCAPE|Comando SET FORMAT|  
|Comando SET FUNCTION|Comando SET HEADINGS|Comando SET HELP|  
|Comando SET HELPFILTER|Comando SET INTENSITY|Comando SET KEY|  
|Comando SET KEYCOMP|Comando SET LOGERRORS|Comando SET MACDESKTOP|  
|Comando SET MACHELP|Comando SET MACKEY|Comando SET MARGIN|  
|Comando SET MARK OF|Comando SET MARK TO|Comando SET MEMOWIDTH|  
|Comando SET MESSAGE|Comando SET MOUSE|Comando SET ODOMETER|  
|Comando SET OLEOBJECT|COMANDO SET PALETTE|Comando SET PDSETUP|  
|Comando SET POINT|Comando SET PRINTER|Comando SET READBORDER|  
|Comando SET REFRESH|Comando SET RESOURCE|Comando SET SAFETY|  
|Comando SET SCOREBOARD|Comando SET SECONDS|Comando SET SEPARATOR|  
|Comando SET SHADOWS|COMANDO SET SKIP OF|Comando SET SPACE|  
|Comando SET STATUS|Comando SET STATUS BAR|Comando SET STEP|  
|Comando SET STICKY|Comando SET SYSFORMATS|Comando SET SYSMENU|  
|Comando SET TALK|Comando SET TEXTMERGE|Comando SET TEXTMERGE DELIMITERS|  
|Comando SET TOPIC|Comando ID SET TOPIC|Comando SET TRBETWEEN|  
|Comando SET TYPEAHEAD|Comando SET VIEW|COMANDO SET WINDOW OF MEMO|  
|Comando SET XCMDFILE|_SHELL variabile di memoria di sistema|Comando SHOW GET|  
|Comando SHOW GETS|Comando MENU SHOW|Comando SHOW OBJECT|  
|Comando SHOW POPUP|Comando SHOW WINDOW|Comando POP DIMENSIONE|  
|Comando FINESTRA DIMENSIONE|Funzione SKPBAR( )|Funzione SKPPAD( )|  
|Funzione SOUNDEX( )|_SPELLCHK variabile di memoria di sistema|Funzioni SQL|  
|SROWS( ) Funzione|_STARTUP variabile di memoria di sistema|Comando SUSPEND|  
|Funzioni SYS() ad eccezione di SYS(2011)|SysMETRIC( ) Funzione||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS variabile di memoria di sistema|Testo... Comando ENDTEXT|Funzione TXTWIDTH( )|  
|Funzione TRANSFORM( )|Variabile di memoria di sistema _TRANSPORT||  
|Comando TYPE|_THROTTLE variabile di memoria di sistema||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Funzione UPDATED( )|Comando USO||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Comando VALIDATE DATABASE|Funzione VARREAD( )|Funzione VERSION( )|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|_WINDOWS variabile di memoria di sistema|_WIZARD variabile di memoria di sistema|Funzione WCHILD( )|  
|Comando WAIT|Funzione WBORDER( )|Funzione WFONT( )|  
|Funzione WCOLS( )|Funzione WEXIST( )|Funzione WLROW( )|  
|Con... Comando ENDWITH|Funzione WLAST( )|Funzione DI SUPERIORE( )|  
|Funzione WMAXIMUM( )|Funzione WLCOL( )|Funzione WREAD( )|  
|Funzione WOUTPUT( )|Funzione WMINIMUM( )|Funzione WVISIBLE( )|  
|Funzione WPARENT( )|Funzione WTITLE( )||  
|Funzione WROWS( )|_WRAP variabile di memoria di sistema||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando FINESTRA di zoom|||
