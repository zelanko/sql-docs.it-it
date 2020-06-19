---
title: Editor origine OData (pagina connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- Sql12.dts.designer.odatasource.connection.f1
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 64d40dd2a6f0f2568e7e7817a3a9366be8f83cc4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965081"
---
# <a name="odata-source-editor-connection-page"></a>Editor origine OData (pagina Connessione)
  Usare la pagina **Connessione** della finestra di dialogo **Editor origine OData** per selezionare la gestione connessione OData per l'origine OData. In questa pagina è inoltre possibile specificare una raccolta o un percorso della risorsa, nonché tutte le opzioni query per scegliere i dati che devono essere recuperati dall'origine OData. Per altre informazioni sull'origine OData, vedere [Origine OData](data-flow/odata-source.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione OData**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuovo**  
 Creare una nuova gestione connessione usando la finestra di dialogo **Editor gestione connessione OData** .  
  
 **Usa percorso risorsa o raccolta**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Description|  
|------------|-----------------|  
|Raccolta|Recuperare i dati dall'origine OData utilizzando il nome di una raccolta.|  
|Percorso risorsa|Recuperare i dati dall'origine OData utilizzando un percorso della risorsa.|  
  
 **Opzioni query**  
 Specificare le opzioni per la query.  Ad esempio: $top=5  
  
 **URL feed**  
 Viene visualizzato l'URL del feed di dati di sola lettura in base alle opzioni selezionate nella finestra di dialogo.  
  
 **Anteprima**  
 Vengono visualizzati in anteprima i risultati tramite la finestra di dialogo **Anteprima** . L'**anteprima** supporta la visualizzazione di un massimo di 20 righe.  
  
## <a name="dynamic-options"></a>Opzioni dinamiche  
  
### <a name="use-collection-or-resource-path--collection"></a>Usa percorso risorsa o raccolta = Raccolta  
 **Raccolta**  
 Selezionare una raccolta dall'elenco a discesa.  
  
### <a name="use-collection-or-resource-path--resource-path"></a>Usa percorso risorsa o raccolta = Percorso risorsa  
 **Resource path**  
 Digitare un percorso della risorsa. Ad esempio: Dipendenti  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine OData &#40;pagina colonne&#41;](../../2014/integration-services/odata-source-editor-columns-page.md)   
 [Editor origine OData &#40;pagina output degli errori&#41;](../../2014/integration-services/odata-source-editor-error-output-page.md)   
 [Gestione connessione OData](connection-manager/odata-connection-manager.md)  
  
  
