---
title: CREATE INDEX per Paradox Documenti Microsoft
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
ms.openlocfilehash: 2e68484efdc5194f93f2acab31973377d9c66f1c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280911"
---
# <a name="create-index-for-paradox"></a>CREATE INDEX per Paradox
La sintassi dell'istruzione CREATE INDEX per il driver ODBC Paradox è la seguente:  
  
 **CREATE** [**UNIQUE**] *INDEX-name* **INDEX**  
  
 **Nome** *tabella* ON  
  
 **(** *identificatore di colonna* [**ASC**]  
  
 [**,** *identificatore di colonna* [**ASC**]...] **)**  
  
 Il driver ODBC Paradox non supporta la parola chiave **DESC** nella grammatica SQL ODBC per l'istruzione CREATE INDEX. L'argomento *nome tabella* può specificare il percorso completo della tabella.  
  
 Se viene specificata la parola chiave **UNIQUE,** il driver ODBC Paradox creerà un indice univoco. Il primo indice univoco viene creato come indice primario. Si tratta di un file di chiave primaria di Paradox denominato *nome-tabella*. Px. Gli indici primari sono soggetti alle restrizioni seguenti:Primary indexes are subject to the following restrictions:  
  
-   L'indice primario deve essere creato prima dell'aggiunta di righe alla tabella.  
  
-   Un indice primario deve essere definito sulle prime colonne "n" di una tabella.  
  
-   È consentito un solo indice primario per tabella.  
  
-   Una tabella non può essere aggiornata dal driver Paradox se un indice primario non è definito nella tabella. (Si noti che questo non è vero per una tabella vuota, che può essere aggiornata anche se un indice univoco non è definito nella tabella.)  
  
-   *L'argomento index-name* per un indice primario deve essere uguale al nome di base della tabella, come richiesto da Paradox.  
  
 Se la parola chiave **UNIQUE** viene omessa, il driver ODBC Paradox creerà un indice non univoco. È costituito da due file di indice secondario di Paradox denominati *nome tabella*. X*nn* e *nome-tabella*. Y*nn*, dove *nn* è il numero della colonna nella tabella. Gli indici non univoci sono soggetti alle restrizioni seguenti:Non-unique indexes are subject to the following restrictions:  
  
-   Prima di poter creare un indice non univoco per una tabella, è necessario che esista un indice primario per tale tabella.  
  
-   Per Paradox 3. *x*, l'argomento *nome indice* per qualsiasi indice diverso da un indice primario (univoco o non univoco) deve essere uguale al nome della colonna. Per Paradox 4. *x* e 5. *x*, il nome di tale indice può essere, ma non deve essere uguale al nome della colonna.  
  
-   È possibile specificare una sola colonna per un indice non univoco.  
  
 Non è possibile aggiungere colonne dopo aver definito un indice in una tabella. Se la prima colonna dell'elenco di argomenti di un'istruzione CREATE TABLE crea un indice, non è possibile includere una seconda colonna nell'elenco di argomenti.  
  
 Ad esempio, per utilizzare le colonne numero ordine cliente e Numero di riga come indice univoco nella tabella SO_LINES, utilizzare il rendiconto:  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Per utilizzare la colonna del numero di parte come indice non univoco nella tabella SO_LINES, utilizzare l'istruzione:  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Si noti che quando vengono eseguite due istruzioni CREATE INDEX, la prima istruzione creerà sempre un indice primario con lo stesso nome della tabella e la seconda istruzione creerà sempre un indice non univoco con lo stesso nome della colonna. Questi indici verranno denominati in questo modo anche se vengono immessi nomi diversi nelle istruzioni CREATE INDEX e anche se l'indice è etichettato UNIQUE nella seconda istruzione CREATE INDEX.  
  
> [!NOTE]  
>  Quando si utilizza il driver Paradox senza implementare il motore di database Borland, sono consentite solo le istruzioni di lettura e aggiunta.
