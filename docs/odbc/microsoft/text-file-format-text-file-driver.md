---
title: Formato di file di testo (Driver file di testo) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- delimited text lines
- fixed-width text files
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: f53cd4b5-0721-4562-a90f-4c55e6030cb9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5801433e0180bb07cb2d09a59db2bb74be012cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303092"
---
# <a name="text-file-format-text-file-driver"></a>Formato file di testo (driver file di testo)
Il driver di testo ODBC supporta file di testo delimitati e a larghezza fissa. Un file di testo è costituito da una riga di intestazione facoltativa e da zero o più righe di testo.  
  
 Anche se la riga di intestazione utilizza lo stesso formato delle altre righe nel file di testo, il driver di testo ODBC interpreta le voci della riga di intestazione come nomi di colonna, non dati.  
  
 Una riga di testo delimitata contiene uno o più valori di dati separati da delimitatori: virgole, tabulazioni o un delimitatore personalizzato. Lo stesso delimitatore deve essere utilizzato in tutto il file. I valori dei dati Null sono indicati da due delimitatori in una riga senza dati tra di essi. Le stringhe di caratteri in una riga di testo delimitata possono essere racchiuse tra virgolette doppie (""). Non possono verificarsi spazi vuoti prima o dopo i valori delimitati.  
  
 La larghezza di ogni immissione dati in una riga di testo a larghezza fissa viene specificata in uno schema. I valori dei dati Null sono indicati da spazi vuoti.  
  
 Le tabelle sono limitate a un massimo di 255 campi. I nomi dei campi sono limitati a 64 caratteri e la larghezza dei campi è limitata a 32.766 caratteri. I record sono limitati a 65.000 byte.  
  
 Un file di testo può essere aperto solo per un singolo utente. Non sono supportati più utenti.  
  
 La seguente grammatica, scritta per i programmatori, definisce il formato di un file di testo che può essere letto dal driver di testo ODBC:  
  
|Format|Rappresentazione|  
|------------|--------------------|  
|Non corsivo|Caratteri che devono essere immessi come mostrato|  
|*Corsivo*|Argomenti definiti in un altro punto della grammatica|  
|parentesi quadre ([])|Elementi facoltativi|  
|parentesi{}graffe ( )|Un elenco di scelte che si escludono a vicenda|  
|barre verticali (&#124;)|Scelte separate che si escludono a vicenda|  
|puntini di sospensione (...)|Elementi che possono essere ripetuti una o più volte|  
  
 Il formato di un file di testo è:  
  
```  
text-file ::=  
   [delimited-header-line] [delimited-text-line]... end-of-file |  
   [fixed-width-header-line] [fixed-width-text-line]... end-of-file  
delimited-header-line ::= delimited-text-line  
delimited-text-line ::=  
   blank-line |  
   delimited-data [delimiter delimited-data]... end-of-line  
fixed-width-header-line ::= fixed-width-text-line  
fixed-width-text-line ::=  
   blank-line |  
   fixed-width-data [fixed-width-data]... end-of-line  
end-of-file ::= <EOF>  
blank-line ::= end-of-line  
delimited-data ::= delimited-string | number | date | delimited-null  
fixed-width-data ::= fixed-width-string | number | date | fixed-width-null  
```  
  
> [!NOTE]  
>  La larghezza di ogni colonna in un file di testo a larghezza fissa è specificata nel file Schema.ini.  
  
```  
  
      end-of-line ::= <CR> | <LF> | <CR><LF>  
delimited-string ::= unquoted-string | quoted-stringunquoted-string ::= [character | digit] [character | digit | quote-character]...  
quoted-string ::=  
   quote-character  
   [character | digit | delimiter | end-of-line | embedded-quoted-string]...  
   quote-characterembedded-quoted-string ::=   quote-characterquote-character  
   [character | digit | delimiter | end-of-line]  
   quote-characterquote-characterfixed-width-string ::= [character | digit | delimiter | quote-character] ...  
character ::= any character except:  
   delimiterdigitend-of-fileend-of-linequote-characterdigit ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9  
delimiter ::= , | <TAB> |   
custom-delimitercustom-delimiter ::= any character except:  
   end-of-fileend-of-linequote-character  
```  
  
> [!NOTE]  
>  Il delimitatore in un file di testo delimitato da personalizzato viene specificato nel file Schema.ini.  
  
```  
quote-character ::= "  
number ::= exact-number | approximate-number  
exact-number ::= [+ | -] {unsigned-integer[.unsigned-integer] |  
   unsigned-integer. |  
   .unsigned-integer}  
approximate-number ::= exact-number{e | E}[+ | -]unsigned-integer  
unsigned-integer ::= {digit}...  
date ::=  
   mm date-separator dd date-separator yy |  
   mmm date-separator dd date-separator yy |  
   dd date-separator mmm date-separator yy |  
   yyyy date-separator mm date-separator dd |  
   yyyy date-separator mmm date-separator dd  
mm ::= digit [digit]  
dd ::= digit [digit]  
yy ::= digit digit  
yyyy ::= digit digit digit digit  
mmm ::= Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec  
date-separator ::= - | / | .  
delimited-null ::=  
```  
  
> [!NOTE]  
>  Per i file delimitati, un valore NULL è rappresentato da nessun dato tra due delimitatori.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  Per i file a larghezza fissa, un valore NULL è rappresentato da spazi.
