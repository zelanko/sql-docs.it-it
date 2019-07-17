---
title: CREATE INDEX per Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 331613676b748453a56da1e41fe85f04a7715038
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081946"
---
# <a name="create-index-for-paradox"></a>CREATE INDEX per Paradox
La sintassi dell'istruzione CREATE INDEX per il driver Paradox ODBC è:  
  
 **CREARE** [**UNIQUE**] **indice** *-nome dell'indice*  
  
 **VIA** *-nome della tabella*  
  
 **(** *colonna identificatore* [**ASC**]  
  
 [ **,** *colonna identificatore* [**ASC**]...] **)**  
  
 Il driver Paradox ODBC non supporta il **DESC** parola chiave nella grammatica SQL ODBC per l'istruzione CREATE INDEX. Il *-nome della tabella* argomento può specificare il percorso completo della tabella.  
  
 Se la parola chiave **UNIQUE** viene specificato, il driver ODBC Paradox verrà creato un indice univoco. Il primo indice univoco viene creato come indice primario. Si tratta di un file chiave primario Paradox denominato *-nome della tabella*. PX. Indici primari sono soggette alle restrizioni seguenti:  
  
-   L'indice primario deve essere creato prima tutte le righe vengono aggiunte alla tabella.  
  
-   Un indice primario deve essere definito al momento le prime colonne in una tabella "n".  
  
-   Per ogni tabella è consentito un solo indice primario.  
  
-   Impossibile aggiornare una tabella dal driver Paradox se un indice primario non è definito sulla tabella. Si noti che ciò non vale per una tabella vuota, che può essere aggiornata anche se un indice univoco non è definito sulla tabella.  
  
-   Il *-nome dell'indice* argomento per un indice primario deve essere lo stesso come il nome di base della tabella, come richiesto da Paradox.  
  
 Se la parola chiave **UNIQUE** viene omesso, il driver ODBC Paradox verrà creato un indice non univoco. Questo è costituito da due file di indice secondario Paradox denominati *-nome della tabella*. X*nn* e *nome-tabella*. Y*nn*, dove *nn* è il numero della colonna nella tabella. Indici non univoci sono soggette alle restrizioni seguenti:  
  
-   Prima di poter creare un indice non univoco per una tabella, deve esistere un indice primario per la tabella.  
  
-   Per Paradox 3. *x*, il *-nome dell'indice* argomento per qualsiasi indice diverso da un indice primario (univoco o non univoco) deve essere identico al nome di colonna. Per Paradox 4. *x* e 5. *x*, può essere il nome di tale indice, ma non deve essere identico al nome di colonna.  
  
-   Per un indice non univoco, è possibile specificare una sola colonna.  
  
 Impossibile aggiungere le colonne dopo aver definito un indice su una tabella. Se la prima colonna dell'elenco di argomenti di un'istruzione CREATE TABLE consente di creare un indice, una seconda colonna non può essere incluso nell'elenco di argomenti.  
  
 Ad esempio, per usare il numero di ordine di vendita e le colonne di numeri di riga dell'indice univoco nella tabella SO_LINES, utilizzare l'istruzione:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Per usare la colonna dei numeri di parte come un indice non univoco nella tabella SO_LINES, utilizzare l'istruzione:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Si noti che quando vengono eseguite due istruzioni CREATE INDEX, la prima istruzione creerà sempre un indice primario con lo stesso nome della tabella e la seconda istruzione creerà sempre un indice non univoci con lo stesso nome di colonna. Questi indici verranno denominati in questo modo anche se vengono immessi diversi nomi nelle istruzioni CREATE INDEX e anche se l'indice viene etichettato UNIQUE nella seconda istruzione CREATE INDEX.  
  
> [!NOTE]  
>  Quando si usa il driver Paradox senza implementare Borland motore di Database di sola lettura e aggiungere le istruzioni sono consentite.
