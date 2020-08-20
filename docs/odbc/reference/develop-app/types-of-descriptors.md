---
description: Tipi di descrittori
title: Tipi di descrittori | Microsoft Docs
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
ms.openlocfilehash: 4ef6bcaa737e26a4a3125e980f6f6bf3c3cff070
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491346"
---
# <a name="types-of-descriptors"></a>Tipi di descrittori
Un descrittore viene usato per descrivere uno dei seguenti elementi:  
  
-   Set di zero o più parametri. Un descrittore di parametro può essere usato per descrivere:  
  
    -   Il *buffer del parametro dell'applicazione,* che contiene gli argomenti dinamici di input impostati dall'applicazione o gli argomenti dinamici di output dopo l'esecuzione di un'istruzione **Call** di SQL.  
  
    -   *Buffer del parametro di implementazione*. Per gli argomenti dinamici di input, contiene gli stessi argomenti del buffer del parametro dell'applicazione, dopo la conversione dei dati che l'applicazione può specificare. Per gli argomenti dinamici di output, contiene gli argomenti restituiti, prima di qualsiasi conversione dei dati che l'applicazione può specificare.  
  
     Per gli argomenti dinamici di input, l'applicazione deve agire su un descrittore di parametri dell'applicazione prima di eseguire qualsiasi istruzione SQL contenente marcatori di parametro dinamici. Per gli argomenti dinamici di input e di output, l'applicazione può specificare tipi di dati diversi da quelli nel descrittore del parametro di implementazione per ottenere la conversione dei dati.  
  
-   Una singola riga di dati del database. Un descrittore di riga può essere utilizzato per descrivere:  
  
    -   *Buffer della riga di implementazione,* che contiene la riga del database. Questi buffer contengono concettualmente i dati scritti o letti dal database. Tuttavia, il formato archiviato dei dati del database non è specificato. Un database può eseguire una conversione aggiuntiva sui dati dal relativo form nel buffer di implementazione.  
  
    -   Il *buffer della riga dell'applicazione,* che contiene la riga di dati presentata all'applicazione, in seguito a qualsiasi conversione dei dati che l'applicazione può specificare.  
  
     L'applicazione opera sul descrittore di riga dell'applicazione in ogni caso in cui i dati delle colonne del database devono essere visualizzati nelle variabili dell'applicazione. Per ottenere la conversione dei dati della colonna, l'applicazione può specificare tipi di dati diversi da quelli nel descrittore della riga di implementazione.  
  
 I tipi di descrittore sono riepilogati nella tabella seguente.  
  
|Tipo di buffer|Righe|Parametri dinamici|  
|-----------------|----------|------------------------|  
|**Buffer applicazione**|Descrittore di riga dell'applicazione (ARD)|Descrittore del parametro dell'applicazione (APD)|  
|**Buffer di implementazione**|Descrittore della riga di implementazione (IRD)|Descrittore parametri di implementazione (dpi)|  
  
 Per il parametro o i buffer di riga, se l'applicazione specifica tipi di dati diversi nei record corrispondenti dei descrittori di implementazione e dell'applicazione, il driver esegue la conversione dei dati quando usa i descrittori. È ad esempio possibile convertire i valori numerici e DateTime in formato stringa di caratteri. Per le conversioni valide, vedere [Appendice D: tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 Un descrittore può eseguire ruoli diversi. Diverse istruzioni possono condividere qualsiasi descrittore allocato in modo esplicito dall'applicazione. Un descrittore di riga in un'istruzione può fungere da descrittore di parametro in un'altra istruzione.  
  
 È sempre noto se un determinato descrittore è un descrittore dell'applicazione o un descrittore di implementazione, anche se il descrittore non è ancora stato utilizzato in un'operazione di database. Per i descrittori allocati dall'implementazione in modo implicito, l'implementazione registra la riga predefinita relativa all'handle di istruzione. Qualsiasi descrittore allocato dall'applicazione chiamando **SQLAllocHandle** è un descrittore dell'applicazione.
