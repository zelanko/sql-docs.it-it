---
description: CREATE INDEX per Paradox
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0274f3f7cfdb79bf64e3616b16b7f3383063e07
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483644"
---
# <a name="create-index-for-paradox"></a>CREATE INDEX per Paradox
La sintassi dell'istruzione CREATE INDEX per il driver ODBC Paradox è la seguente:  
  
 **Create** [**Unique**] **index index** *-Name*  
  
 **Per** *nome tabella*  
  
 **(** *identificatore di colonna* [**ASC**]  
  
 [**,** *identificatore di colonna* [**ASC**]...] **)**  
  
 Il driver ODBC Paradox non supporta la parola chiave **desc** nella grammatica ODBC SQL per l'istruzione create index. L'argomento *nome tabella* può specificare il percorso completo della tabella.  
  
 Se si specifica la parola chiave **Unique** , il driver ODBC Paradox creerà un indice univoco. Il primo indice univoco viene creato come indice primario. Si tratta di un file di chiave primaria Paradox denominato *Table-Name*. PX. Gli indici primari sono soggetti alle restrizioni seguenti:  
  
-   Prima di aggiungere righe alla tabella, è necessario creare l'indice primario.  
  
-   Un indice primario deve essere definito sulle prime colonne "n" di una tabella.  
  
-   Per ogni tabella è consentito un solo indice primario.  
  
-   Una tabella non può essere aggiornata dal driver Paradox se nella tabella non è definito un indice primario. Si noti che questo non è vero per una tabella vuota, che può essere aggiornata anche se nella tabella non è definito un indice univoco.  
  
-   L'argomento *index-name* per un indice primario deve corrispondere al nome di base della tabella, come richiesto da Paradox.  
  
 Se la parola chiave **Unique** viene omessa, il driver ODBC Paradox creerà un indice non univoco. Questo è costituito da due file di indice secondario Paradox denominati *nome-tabella*. X*nn* e *nome tabella*. Y*nn*, dove *nn* è il numero della colonna nella tabella. Gli indici non univoci sono soggetti alle restrizioni seguenti:  
  
-   Prima di poter creare un indice non univoco per una tabella, è necessario che esista un indice primario per tale tabella.  
  
-   Per Paradox 3. *x*, l'argomento relativo al *nome di indice* per qualsiasi indice diverso da un indice primario (univoco o non univoco) deve corrispondere al nome della colonna. Per Paradox 4. *x* e 5. *x*, il nome di tale indice può essere, ma non deve necessariamente essere uguale al nome della colonna.  
  
-   Per un indice non univoco è possibile specificare una sola colonna.  
  
 Non è possibile aggiungere colonne dopo che è stato definito un indice in una tabella. Se la prima colonna dell'elenco di argomenti di un'istruzione CREATE TABLE crea un indice, non è possibile includere una seconda colonna nell'elenco di argomenti.  
  
 Per utilizzare ad esempio le colonne Numero ordine di vendita e numero di riga come indice univoco nella tabella SO_LINES, utilizzare l'istruzione:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Per utilizzare la colonna numero parte come indice non univoco nella tabella SO_LINES, utilizzare l'istruzione:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Si noti che quando vengono eseguite due istruzioni CREATE INDEX, la prima istruzione creerà sempre un indice primario con lo stesso nome della tabella e la seconda istruzione creerà sempre un indice non univoco con lo stesso nome della colonna. Questi indici verranno denominati in questo modo anche se nelle istruzioni CREATE INDEX vengono immessi nomi diversi, anche se l'indice è contrassegnato come UNIQUE nella seconda istruzione CREATE INDEX.  
  
> [!NOTE]  
>  Quando si usa il driver Paradox senza implementare il motore di database Borland, sono consentite solo istruzioni Read e Append.
