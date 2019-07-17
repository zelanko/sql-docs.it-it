---
title: Indice personalizzato (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c57bf8b8-55a6-4b6c-9adb-91b5f4f1ee3c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 546e04385490e725adfa0bb2f256109da7a0d55d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094427"
---
# <a name="custom-index-master-data-services"></a>Indice personalizzato (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Gli indici personalizzati consentono di creare un indice non cluster in un attributo (indice singolo) o in un elenco di attributi (indice composto) e in un'entità. In genere gli indici migliorano le prestazioni del processo di esecuzione delle query. Per altre informazioni sugli indici di SQL Server, vedere [Indici](../relational-databases/indexes/indexes.md).  
  
## <a name="type-of-indexes"></a>Tipi di indici  
 È possibile creare i seguenti tipi di indici personalizzati per ogni entità.  
  
-   Indice univoco  
  
-   Indice non univoco  
  
 Un indice univoco garantisce che la colonna indicizzata non contenga valori duplicati. Per gli indici univoci composti, l'indice garantisce che ogni combinazione di valori nell'elenco di attributi selezionati sia univoca. Non è possibile creare un indice univoco se sono presenti valori duplicati per gli attributi selezionati.  
  
## <a name="rules"></a>Regole  
 Le regole seguenti si applicano agli indici personalizzati, sia univoci che non univoci.  
  
-   Per creare un indice personalizzato, assicurarsi di selezionare almeno un attributo.  
  
-   Se si tenta di salvare un indice con lo stesso elenco di attributi e flag di univocità di un altro indice, l'indice non può essere salvato. Verrà visualizzato un errore.  
  
    > [!NOTE]  
    >  MDS crea automaticamente gli indici per determinati attributi (ad esempio di DBA e codice). Ciò significa che non è possibile creare un altro indice che contenga uno di questi attributi e non ne contenga altri.  
  
-   Gli attributi possono essere inclusi in più di un indice personalizzato, purché vi sia almeno un attributo diverso negli altri indici. In caso contrario, gli indici sono gli stessi.  
  
-   Se si crea un indice che contiene numerosi attributi o attributi di grandi dimensioni e le dimensioni totali degli attributi selezionati superano la dimensione massima della chiave indice (900 byte), l'indice non può essere salvato.  
  
-   Un indice personalizzato può essere creato in attributi membro foglia, esclusi gli attributi di file.  
  
-   Se si vuole eliminare un attributo incluso in un indice personalizzato, si applica quanto segue.  
  
    -   Se l'indice viene creato in un solo attributo (indice singolo), verranno eliminati sia l'attributo sia l'indice.  
  
    -   Se l'indice viene creato in più di un attributo (indice composto), l'attributo può essere eliminato finché non si modifica l'indice.  
  
-   Non è possibile modificare il tipo di attributo incluso in un indice personalizzato.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Creare un indice|[Creare un indice &#40;Master Data Services&#41;](../master-data-services/create-an-index-master-data-services.md)|  
|Modificare ed eliminare un indice|[Modificare ed eliminare un indice &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)|  
  
  
