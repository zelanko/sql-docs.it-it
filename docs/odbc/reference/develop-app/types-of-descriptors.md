---
title: Tipi di descrittori . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a6c7b55194eb61c1a909ced2296e4ad2050b674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304892"
---
# <a name="types-of-descriptors"></a>Tipi di descrittori
Un descrittore viene utilizzato per descrivere uno dei seguenti elementi:  
  
-   Un set di zero o più parametri. Un descrittore di parametro può essere utilizzato per descrivere:A parameter descriptor can be used to describe:  
  
    -   Buffer dei *parametri dell'applicazione,* che contiene gli argomenti dinamici di input impostati dall'applicazione o gli argomenti dinamici di output dopo l'esecuzione di un'istruzione **CALL** di SQL.  
  
    -   Il *parametro di implementazione buffer*. Per gli argomenti dinamici di input, contiene gli stessi argomenti del buffer dei parametri dell'applicazione, dopo qualsiasi conversione dei dati che l'applicazione può specificare. Per gli argomenti dinamici di output, contiene gli argomenti restituiti, prima di qualsiasi conversione di dati che l'applicazione può specificare.  
  
     Per gli argomenti dinamici di input, l'applicazione deve operare su un descrittore di parametri dell'applicazione prima di eseguire qualsiasi istruzione SQL che contiene indicatori di parametro dinamico. Per gli argomenti dinamici di input e output, l'applicazione può specificare tipi di dati diversi da quelli nel descrittore del parametro di implementazione per ottenere la conversione dei dati.  
  
-   Una singola riga di dati di database. Un descrittore di riga può essere utilizzato per descrivere:A row descriptor can be used to describe:  
  
    -   Buffer *di riga di implementazione,* che contiene la riga del database. (Questi buffer concettualmente contengono dati come scritti o letti dal database. Tuttavia, la forma memorizzata dei dati del database non è specificata. Un database potrebbe eseguire una conversione aggiuntiva sui dati dal relativo formato nel buffer di implementazione.)  
  
    -   Buffer *di riga dell'applicazione,* che contiene la riga di dati presentata all'applicazione, in seguito a qualsiasi conversione di dati che l'applicazione può specificare.  
  
     L'applicazione opera sul descrittore di riga dell'applicazione in qualsiasi caso in cui i dati di colonna del database devono essere visualizzati nelle variabili dell'applicazione. Per ottenere la conversione dei dati di colonna, l'applicazione può specificare tipi di dati diversi da quelli nel descrittore di riga di implementazione.  
  
 I tipi di descrittore sono riepilogati nella tabella seguente.  
  
|Tipo di buffer|Righe|Parametri dinamici|  
|-----------------|----------|------------------------|  
|**Buffer dell'applicazione**|Descrittore di riga dell'applicazione (ARD)Application row descriptor (ARD)|Descrittore di parametro dell'applicazione (APD)|  
|**Buffer di implementazione**|Descrittore di riga di implementazione (IRD)Implementation row descriptor (IRD)|Descrittore del parametro di implementazione (IPD)Implementation parameter descriptor (IPD)|  
  
 Per il parametro o i buffer di riga, se l'applicazione specifica tipi di dati diversi nei record corrispondenti dei descrittori di implementazione e dell'applicazione, il driver esegue la conversione dei dati quando utilizza i descrittori. Ad esempio, può convertire valori numerici e datetime in formato stringa di caratteri. Per le conversioni valide, vedere [appendice D: tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 Un descrittore può eseguire ruoli diversi. Istruzioni diverse possono condividere qualsiasi descrittore allocato in modo esplicito dall'applicazione. Un descrittore di riga in un'istruzione può fungere da descrittore di parametro in un'altra istruzione.  
  
 È sempre noto se un determinato descrittore è un descrittore dell'applicazione o un descrittore di implementazione, anche se il descrittore non è ancora stato utilizzato in un'operazione di database. Per i descrittori che l'implementazione alloca in modo implicito, l'implementazione registra la riga predefinita relativa all'handle dell'istruzione. Qualsiasi descrittore che l'applicazione alloca chiamando **SQLAllocHandle** è un descrittore dell'applicazione.
