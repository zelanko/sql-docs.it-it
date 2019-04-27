---
title: Formato di File di testo (Driver File di testo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd2bc95e6fe5468e88fc61dd8ed4adcd985ec052
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633016"
---
# <a name="text-file-format-text-file-driver"></a>Formato file di testo (driver file di testo)
Il driver ODBC testo supporta entrambi i file di testo a larghezza fissa che quelli delimitati. Un file di testo è costituito da una riga di intestazione facoltativi e zero o più righe di testo.  
  
 Anche se la riga di intestazione Usa lo stesso formato come le altre righe nel file di testo, il driver ODBC testo interpreta le voci di riga di intestazione come nomi di colonna e non dati.  
  
 Una riga di testo delimitato contiene uno o più valori di dati separati da delimitatori: virgole, tabulazioni o un delimitatore personalizzato. Lo stesso delimitatore deve essere usato in tutto il file. I valori null sono contrassegnati da due delimitatori di una riga senza dati tra di essi. Stringhe di caratteri in una riga di testo delimitato da virgole possono essere racchiuso tra virgolette doppie (""). Spazi vuoti non possono verificarsi prima o dopo i valori delimitato da virgole.  
  
 La larghezza di ogni voce di dati in una riga di testo a larghezza fissa viene specificata in uno schema. I valori null sono indicati da spazi vuoti.  
  
 Le tabelle sono limitate a un massimo di 255 campi. I nomi dei campi sono limitate a 64 caratteri e la larghezza dei campi è limitati a 32,766 caratteri. I record sono limitati a 65.000 byte.  
  
 Un file di testo può essere aperto solo per un singolo utente. Più utenti non sono supportati.  
  
 La grammatica seguente, scritta per i programmatori, definisce il formato di un file di testo che può essere letta dal driver ODBC di testo:  
  
|Formato|Rappresentazione|  
|------------|--------------------|  
|Non-corsivo|Caratteri che devono essere immesso come visualizzato|  
|*italics*|Argomenti definiti in un' posizione nella grammatica|  
|parentesi quadre ([])|Elementi facoltativi|  
|le parentesi graffe ({})|Un elenco di scelte si escludono a vicenda|  
|le barre verticali (&#124;)|Opzioni si escludono a vicenda separate|  
|ellipses (...)|Elementi che possono essere ripetuti una o più volte|  
  
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
>  La larghezza di ogni colonna in un file di testo a larghezza fissa viene specificata nel file ini.  
  
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
>  Il delimitatore in un file di testo delimitato da personalizzata è specificato nel file ini.  
  
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
>  Per i file delimitati, un valore NULL è rappresentato da dati non tra due delimitatori.  
  
```  
fixed-width-null ::= <SPACE>...  
```  
  
> [!NOTE]  
>  Per i file a larghezza fissa, un valore NULL è rappresentato da spazi.
