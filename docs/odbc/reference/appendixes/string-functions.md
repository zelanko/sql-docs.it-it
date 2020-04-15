---
title: Funzioni stringa Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], string functions
- string functions [ODBC]
ms.assetid: 270f669e-8aab-4db0-95a4-f2b3c69538b3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9323809028ad170a4811b1af8b6e276cdbb4293
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302842"
---
# <a name="string-functions"></a>Funzioni di stringa
Nella tabella seguente sono elencate le funzioni di modifica delle stringhe. Un'applicazione può determinare quali funzioni stringa sono supportate da un driver chiamando **SQLGetInfo** con un tipo di *informazioni* di SQL_STRING_FUNCTIONS.  
  
## <a name="remarks"></a>Osservazioni  
 Gli argomenti indicati come *string_exp* possono essere il nome di una colonna, un *carattere-stringa-valore letterale*o il risultato di un'altra funzione scalare, in cui il tipo di dati sottostante può essere rappresentato come SQL_CHAR, SQL_VARCHAR o SQL_LONGVARCHAR.  
  
 Gli argomenti indicati come *character_exp* sono una stringa di caratteri di lunghezza variabile.  
  
 Gli argomenti indicati come *start*, *length*o *count* possono essere un *valore numerico-letterale* o il risultato di un'altra funzione scalare, in cui il tipo di dati sottostante può essere rappresentato come SQL_TINYINT, SQL_SMALLINT o SQL_INTEGER.  
  
 Le funzioni stringa elencate di seguito sono in base 1; ovvero, il primo carattere della stringa è il carattere 1.  
  
 Le funzioni scalari BIT_LENGTH, CHAR_LENGTH, CHARACTER_LENGTH, OCTET_LENGTH e stringa POSITION sono state aggiunte in ODBC 3.0 per allinearsi a SQL-92.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**ASCII(** _string_exp_ **)** (ODBC 1.0)|Restituisce il valore del codice ASCII del carattere più a sinistra di *string_exp* come numero intero.|  
|**BIT_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Restituisce la lunghezza in bit dell'espressione stringa.<br /><br /> Non funziona solo per i tipi di dati stringa, pertanto non convertirà in modo implicito *string_exp* in stringa, ma restituirà la dimensione (interna) di qualsiasi tipo di dati fornito.|  
|**CHAR(** _codice_ **)** (ODBC 1.0)|Restituisce il carattere con il valore del codice ASCII specificato dal *codice*. Il valore del *codice* deve essere compreso tra 0 e 255; in caso contrario, il valore restituito dipende dall'origine dati.|  
|**CHAR_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Restituisce la lunghezza in caratteri dell'espressione stringa, se l'espressione stringa è di un tipo di dati carattere; in caso contrario, restituisce la lunghezza in byte dell'espressione stringa (il numero intero più piccolo non inferiore al numero di bit diviso per 8). Questa funzione è la stessa della funzione CHARACTER_LENGTH.|  
|**CHARACTER_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Restituisce la lunghezza in caratteri dell'espressione stringa, se l'espressione stringa è di un tipo di dati carattere; in caso contrario, restituisce la lunghezza in byte dell'espressione stringa (il numero intero più piccolo non inferiore al numero di bit diviso per 8). (Questa funzione è la stessa della funzione CHAR_LENGTH.)|  
|**CONCAT(** _string_exp1__, string_exp2_**)** (ODBC 1.0)|Restituisce una stringa di caratteri che è il risultato della concatenazione di *string_exp2* a *string_exp1.* La stringa risultante dipende da DBMS. Ad esempio, se la colonna rappresentata da *string_exp1* conteneva un valore NULL, DB2 restituirebbe NULL ma SQL Server restituirebbe la stringa non NULL.|  
|**DIFFERENCE(** _string_exp1_,_string_exp2_**)** (ODBC 2.0)|Restituisce un valore intero che indica la differenza tra i valori restituiti dalla funzione SOUNDEX per *string_exp1* e *string_exp2*.|  
|**INSERT(** _string_exp1_, *start*, *length* _string_exp2_**)** (ODBC 1.0)|Restituisce una stringa di caratteri in cui i caratteri *di lunghezza* sono stati eliminati da *string_exp1*, a partire *dall'inizio*e in cui *string_exp2* è stato inserito in *string_exp,* a partire *dall'inizio.*|  
|**LCASE(** _string_exp_ **)** (ODBC 1.0)|Restituisce una stringa uguale a quella in *string_exp*, con tutti i caratteri maiuscoli convertiti in caratteri minuscoli.|  
|**SINISTRA(** _string_exp_, _count_**)** (ODBC 1.0)|Restituisce i caratteri di *conteggio* più a sinistra di *string_exp.*|  
|**LENGTH(** _string_exp_ **)** (ODBC 1.0)|Restituisce il numero di caratteri in *string_exp,* esclusi gli spazi vuoti finali.<br /><br /> **LENGTH** accetta solo stringhe. Pertanto convertirà in modo implicito *string_exp* in una stringa e restituirà la lunghezza di questa stringa (non la dimensione interna del tipo di dati).|  
|**LOCATE(** _string_exp1_, *string_exp2*[, *inizio*]**)** (ODBC 1.0)|Restituisce la posizione iniziale della prima occorrenza di *string_exp1* all'interno *di string_exp2.* La ricerca della prima occorrenza di *string_exp1* inizia con la prima posizione del carattere in *string_exp2,* a meno che non venga specificato l'argomento facoltativo *start*. Se *si specifica start,* la ricerca inizia con la posizione del carattere indicata dal valore di *start*. La posizione del primo carattere in *string_exp2* è indicata dal valore 1. Se *string_exp1* non viene trovato all'interno *di string_exp2*, viene restituito il valore 0.<br /><br /> Se un'applicazione può chiamare la funzione scalare LOCATE con gli argomenti *string_exp1* *, string_exp2*e *start,* il driver restituisce SQL_FN_STR_LOCATE quando **SQLGetInfo** viene chiamato con un'opzione di SQL_STRING_FUNCTIONS. *Option* Se l'applicazione può chiamare la funzione scalare LOCATE con solo il *string_exp1* e *string_exp2* argomenti, il driver restituisce SQL_FN_STR_LOCATE_2 quando **SQLGetInfo** viene chiamato con un *Opzione* di SQL_STRING_FUNCTIONS. I driver che supportano la chiamata della funzione LOCATE con due o tre argomenti restituiscono sia SQL_FN_STR_LOCATE che SQL_FN_STR_LOCATE_2.|  
|**LTRIM(** _string_exp_ **)** (ODBC 1.0)|Restituisce i caratteri di *string_exp*, con gli spazi vuoti iniziali rimossi.|  
|**OCTET_LENGTH(** _string_exp_ **)** (ODBC 3.0)|Restituisce la lunghezza in byte dell'espressione stringa. Il risultato è il più piccolo numero integer non inferiore al numero di bit diviso per 8.<br /><br /> Non funziona solo per i tipi di dati stringa, pertanto non convertirà in modo implicito *string_exp* in stringa, ma restituirà la dimensione (interna) di qualsiasi tipo di dati fornito.|  
|**POSITION(** _character_exp_ **IN** _character_exp_**)** (ODBC 3.0)|Restituisce la posizione della prima espressione di caratteri nella seconda espressione di caratteri. Il risultato è un numero esatto con una precisione definita dall'implementazione e una scala pari a 0.The result is an exact numeric with an implementation-defined precision and a scale of 0.|  
|**REPEAT(** _string_exp,_ _count_**)** (ODBC 1.0)|Restituisce una stringa di caratteri composta da *string_exp* *conteggio* ripetuto volte.|  
|**REPLACE(** _string_exp1_, *string_exp2* _, string_exp3_**)** (ODBC 1.0)|Cercare *string_exp1* di *string_exp2*e sostituirlo con *string_exp3*.|  
|**DESTRA(** _string_exp_, _count_**)** (ODBC 1.0)|Restituisce i caratteri di *conteggio* più a destra di *string_exp.*|  
|**RTRIM(** _string_exp_ **)** (ODBC 1.0)|Restituisce i caratteri di *string_exp* con gli spazi vuoti finali rimossi.|  
|**SOUNDEX(** _string_exp_ **)** (ODBC 2.0)|Restituisce una stringa di caratteri dipendente dall'origine dati che rappresenta il suono delle parole in *string_exp*. Ad esempio, SQL Server restituisce un codice SOUNDEX a 4 cifre; Oracle restituisce una rappresentazione fonetica di ogni parola.|  
|**BARRA(** _conteggio)_ **)** (ODBC 2.0)|Restituisce una stringa di caratteri costituita da spazi di *conteggio.*|  
|**SUBSTRING(** _string_exp_, *inizio*, length **)** (ODBC 1.0)|Restituisce una stringa di caratteri derivata da *string_exp*, a partire dalla posizione del carattere specificata da *start* *for* length characters.|  
|**UCASE(** _string_exp_ **)** (ODBC 1.0)|Restituisce una stringa uguale a quella di *string_exp*, con tutti i caratteri minuscoli convertiti in maiuscolo.|
