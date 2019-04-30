---
title: Tipi di descrittori di | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a042229e3149f97b72b6e86b485771966eb80c30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305622"
---
# <a name="types-of-descriptors"></a>Tipi di descrittori
Un descrittore viene usato per descrivere uno dei seguenti:  
  
-   Un set di zero o più parametri. Un descrittore del parametro può essere utilizzato per descrivere:  
  
    -   Il *buffer del parametro dell'applicazione,* che contiene degli argomenti dinamici inpui come impostato dall'applicazione o degli argomenti dinamici output dopo l'esecuzione di un **CHIAMARE** istruzione SQL.  
  
    -   Il *buffer dei parametri di implementazione*. Per argomenti di input dinamici, contiene gli stessi argomenti come il buffer del parametro dell'applicazione, dopo l'applicazione può specificare qualsiasi conversione di dati. Per argomenti dinamici di output, contiene gli argomenti restituiti, prima di qualsiasi conversione di dati che può specificare l'applicazione.  
  
     Per argomenti di input dinamici, l'applicazione deve funzionare su un descrittore di parametri dell'applicazione prima di eseguire qualsiasi istruzione SQL contenente i marcatori di parametro dinamico. Per argomenti dinamici di input e di output, l'applicazione può specificare tipi di dati diversi da quelli nel descrittore di parametri di implementazione per ottenere la conversione dei dati.  
  
-   Una singola riga di dati del database. Un descrittore riga può essere utilizzato per descrivere:  
  
    -   Il *buffer di riga di implementazione,* che contiene la riga dal database. (Questi buffer concettualmente contengono dati così come scritta o letta dal database. Tuttavia, i moduli archiviati dei dati del database non sono specificato. Un database è stato possibile eseguire la conversione aggiuntiva sui dati dal formato nel buffer di implementazione.)  
  
    -   Il *buffer di riga dell'applicazione,* che contiene la riga di dati presentato all'applicazione, qualsiasi conversione di dati che l'applicazione può specificare di seguito.  
  
     L'applicazione opera nel descrittore della riga di applicazione in tutti i casi in cui i dati della colonna dal database devono comparire in variabili di applicazione. Per ottenere la conversione dei dati di dati della colonna, l'applicazione può specificare tipi di dati diversi da quelli nel descrittore della riga di implementazione.  
  
 Nella tabella seguente sono riepilogati i tipi di descrittore.  
  
|Tipo di buffer|Righe|Parametri dinamici|  
|-----------------|----------|------------------------|  
|**Buffer dell'applicazione**|descrittore della riga di applicazione (ARD)|descrittore del parametro dell'applicazione (APD)|  
|**Buffer di implementazione**|descrittore della riga di implementazione (IRD)|Descrizione del parametro di implementazione (IPD)|  
  
 Per il parametro o il buffer di riga, se l'applicazione specifica tipi di dati diversi in record corrispondente dei descrittori di implementazione e dell'applicazione, il driver esegue la conversione dei dati quando si usa i descrittori. Ad esempio, può convertire valori numerici e data/ora in formato stringa di caratteri. (Per le conversioni valide, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Un descrittore di è possibile eseguire diversi ruoli. Istruzioni diversi possono condividere qualsiasi descrittore allocate in modo esplicito dall'applicazione. Un descrittore delle righe in un'unica istruzione può essere utilizzato come un descrittore del parametro in un'altra istruzione.  
  
 È sempre possibile sapere se un determinato descrittore è un descrittore applicazione o un descrittore di implementazione, anche se il descrittore non è ancora stato utilizzato in un'operazione di database. Per i descrittori allocati in modo implicito l'implementazione, l'implementazione registra la riga predefinita rispetto all'handle di istruzione. Qualsiasi descrittore che consente di allocare l'applicazione chiamando **SQLAllocHandle** è un descrittore applicazione.
