---
title: Elementi usati nelle istruzioni SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], elements supported
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 85777525-1555-4731-8309-63a464c6b43a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e33beff29463172a26d53953dd5f563fe1f3f5c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512191"
---
# <a name="elements-used-in-sql-statements"></a>Elementi usati nelle istruzioni SQL
Gli elementi seguenti vengono utilizzati nelle istruzioni SQL elencate in precedenza.  
  
## <a name="element"></a>Elemento  
 *Identificatore di tabella di base* :: = *nome definito dall'utente*  
  
 *Nome-tabella di base* :: = *identificatore-tabella di base*  
  
 *valore booleano-fattore* :: = [NOT] *boolean primario*  
  
 *valore booleano-primary* :: = confronto *-predicato* &#124; ( *condizione di ricerca* )  
  
 *valore booleano-termini* :: = *fattore booleano* [AND *boolean-termine*]  
  
 *valore letterale stringa di caratteri* :: = ' {*carattere*}... " (*carattere* è qualsiasi carattere nel set di caratteri dell'origine dati/driver. Per includere un carattere letterale virgolette (") in una stringa letterale carattere, usare due virgolette letterali [' '].)  
  
 *Identificatore di colonna* :: = *nome definito dall'utente*  
  
 *nome della colonna* :: = [*nome-tabella*.] *identificatore di colonna*  
  
 *operatore di confronto* :: = < &#124; > &#124; \<= &#124; > = &#124; = &#124; <>  
  
 *predicato di confronto* :: = *espressione* espressione di operatore di confronto  
  
 *tipo di dati* :: = *tipo di stringa di caratteri* (*stringa-tipo di carattere* è qualsiasi tipo di dati per cui la colonna "" DATA_TYPE"" nel set di risultati restituiti da SQLGetTypeInfo è entrambi SQL_CHAR o SQL_VARCHAR.)  
  
 *cifra* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *il parametro dinamico* :: =?  
  
 *espressione* :: = termine &#124; espressione {+&#124;-} termine  
  
 *fattore* :: = [*+*&#124;*-*]*primario*  
  
 *valore di inserimento* :: =  
  
 *parametro dinamico*  
  
 &#124;*letterale*  
  
 &AMP;#124;NULL  
  
 &AMP;#124;UTENTE  
  
 *lettera* :: = *lower-case-lettera &#124; upper-case-letter*  
  
 *valore letterale* :: = *valore letterale stringa di caratteri*  
  
 *Lower-case-letter* :: = un &#124; b &#124; c &#124; 1!d &#124; e &#124; f &#124; g &#124; h &#124; è &#124; j &#124; k &#124; g &#124; m &#124; n &#124; o &#124; p &#124; domande e &#124; r &#124; s &#124; t &#124; u &#124; v &#124; w &#124; x &#124; y &#124; z  
  
 *clausola Order by* :: = ORDER BY *specifica di ordinamento* [, *preferenze di ordinamento*]...  
  
 *primario* :: = *nome-colonna*  
  
 &#124;*dinamico-parametro*  
  
 &#124;*letterale*  
  
 &#124;( *espressione* )  
  
 *condizione di ricerca* :: = *boolean-termine* [oppure *condizione di ricerca*]  
  
 *elenco SELECT* :: = \* &#124; *select-sottoelenco* [, *selezionare sottoelenco*]...  (*elenco select* non può contenere parametri.)  
  
 *Selezionare sottoelenco* :: = *espressione*  
  
 *Specifica di ordinamento* :: = {*unsigned integer &#124; nome della colonna*} [*Centro sicurezza di AZURE &#124; DESC*]  
  
 *Identificatore di tabella* :: = *nome definito dall'utente*  
  
 *nome della tabella* :: = *identificatore di tabella*  
  
 *riferimento alla tabella* :: = *-nome della tabella*  
  
 *elenco di riferimento nella tabella* :: = *riferimento alla tabella* [,*riferimento alla tabella*]...  
  
 *termine* :: = *factor* &#124; *termine* {\*&#124;*/*} *factor*  
  
 *intero senza segno* :: = {*cifra*}  
  
 *upper-case-letter* :: = *A &#124; B &#124; C &#124; 1!d &#124; E &#124; F &#124; G &#124; H &#124; è &#124; J &#124; K &#124; L &#124; M &#124; N &#124; O &#124; &#124;Q &#124; R &#124; S &#124; T &#124; U &#124; V &#124; W &#124; X &#124; Y &#124; Z*  
  
 *nome definito dall'utente* :: = *lettera*[*cifra* &#124; *lettera* &#124; *_*]...
