---
title: Elementi utilizzati nelle istruzioni SQL Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49a1cd54957426d4d14d84d43df670c8c3d96189
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307022"
---
# <a name="elements-used-in-sql-statements"></a>Elementi usati nelle istruzioni SQL
Gli elementi seguenti vengono utilizzati nelle istruzioni SQL elencate in precedenza.  
  
## <a name="element"></a>Elemento  
 *identificatore di tabella di base* :: : nome definito *dall'utente*  
  
 *nome-tabella di base* :: *identificatore della tabella di base*  
  
 *booleano-fattore* :: : [NOT] *booleano-primario*  
  
 *booleano-primario* :: : confronto *-predicato* &#124; ( *condizione-ricerca* )  
  
 *termine-booleano* :: : *boolean-factor* [AND *boolean-term*]  
  
 *carattere-stringa-valore letterale* :: ''''carattere '...''*character* (*carattere* è qualsiasi carattere nel set di caratteri del driver/origine dati. Per includere un singolo carattere di citazione letterale ('') in un carattere-stringa-valore letterale, utilizzare due caratteri di virgolette letterali ['''''].)  
  
 *identificatore-colonna* :: : *nome definito dall'utente*  
  
 *nome-colonna* :: : [*nome-tabella*.] *identificatore di colonna*  
  
 *operatore di confronto* \<:: < &#124; > &#124;  &#124; > &#124; >&#124; &#124; <>  
  
 espressione *di confronto-predicate* :: : *espressione comparison-operator*  
  
 *tipo di dati* :: *, carattere-stringa-tipo* *(carattere-stringa-tipo* è qualsiasi tipo di dati per il quale la colonna ""DATA_TYPE"" nel set di risultati restituito da SQLGetTypeInfo è SQL_CHAR o SQL_VARCHAR.)  
  
 *cifra* :: 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9  
  
 *parametro dinamico* :: ?  
  
 *espressione* :: : termine &#124; espressione :&#124; -)  
  
 *fattore* ::*+* *-*: [&#124;]*primario*  
  
 *insert-valore* ::  
  
 *parametro dinamico*  
  
 &#124; *letterale*  
  
 &#124; NULL  
  
 &#124; UTENTE  
  
 *Lettera* :: lettera *minuscola &#124; lettera maiuscola*  
  
 *valore letterale* :: : *carattere-stringa-valore letterale*  
  
 *minuscola-lettera* :: a &#124; b &#124; &#124; &#124; s &#124; &#124; e &#124; &#124; g &#124; &#124; g &#124; &#124; &#124; &#124; &#124; &#124; &#124; &#124; &#124; &#124; n &#124; &#124; &#124; &#124; &#124; &#124; &#124; &#124; &#124; s &#124; s &#124; t &#124; u &#124; v &#124; &#124; &#124; &#124; &#124; &#124; &#124; &#124; z  
  
 *order-by-clause* :: : ORDER BY *specifica di ordinamento* [, *specifica di ordinamento*]...  
  
 *nome-colonna* *primaria* ::  
  
 &#124; *parametro dinamico*  
  
 &#124; *letterale*  
  
 &#124; ( *espressione* )  
  
 *condizione-ricerca* :: : *termine booleano* [OR *condizione di ricerca*]  
  
 *select-list* :: \* &#124; *select-sublist* [, *select-sublist*]...  *(l'elenco di selezione* non può contenere parametri.)  
  
 *Select-sublist* :: *espressione*  
  
 *specifica di ordinamento* :: :*unsigned-integer &#124; nome-colonna*[*ASC &#124; DESC*]  
  
 *identificatore di tabella* :: : *nome definito dall'utente*  
  
 *nome-tabella* :: *identificatore di tabella*  
  
 *Table-reference* :: *nome-tabella*  
  
 *elenco di riferimenti a tabella* :: : riferimento alla *tabella* [, riferimento*di tabella*]...  
  
 *termine* :: : *fattore* *factor* &#124;\*&#124;*/* *termine*  
  
 *Unsigned-integer* :: :*cifra*  
  
 *lettera maiuscola ::* *: A &#124; B &#124; C &#124; D &#124; E &#124; F &#124; &#124; G &#124; H &#124; &#124; &#124; &#124; k &#124; L &#124; N &#124; &#124; N.&#124; &#124; O &#124; o &#124; P &#124; &#124; R &#124; &#124; R &#124; &#124; R &#124; S.U &#124;.S.R &#124; &#124; &#124;.L. &#124;*  
  
 *nome-definito dall'utente* :: *lettera*[*cifra* &#124; *lettera* &#124; *_*]...
