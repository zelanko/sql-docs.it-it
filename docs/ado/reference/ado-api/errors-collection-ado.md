---
title: Raccolta di errori (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Errors
- Connection15::get_Errors
- Connection15::GetErrors
helpviewer_keywords:
- Errors collection [ADO]
ms.assetid: 290819e1-7b39-4e1e-a93b-801257138b00
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b595baf25a8b0f3982399c384c169c6af3f1cd81
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253187"
---
# <a name="errors-collection-ado"></a>Raccolta Errors (ADO)
Contiene tutti i [errore](../../../ado/reference/ado-api/error-object.md) gli oggetti creati in risposta a un singolo errore relativi al provider.  
  
## <a name="remarks"></a>Note  
 Qualsiasi operazione che interessa oggetti ADO è possibile generare uno o più errori del provider. Come si verifica ogni errore, una o più **errore** gli oggetti possono essere inseriti nel **errori** raccolta del [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. Quando un'altra operazione ADO genera un errore, il **errori** raccolta viene cancellata e il nuovo set di **errore** gli oggetti possono essere inseriti nel **errori** raccolta.  
  
 Ciascuna **errore** oggetto rappresenta un errore specifico del provider, non un errore ADO. Errori ADO vengono esposti al meccanismo di gestione delle eccezioni in fase di esecuzione. Ad esempio, in Microsoft Visual Basic, l'occorrenza di un errore specifico del ADO attiverà un' [onError](../../../ado/reference/rds-api/onerror-event-rds.md) eventi e vengono visualizzate nel **Err** oggetto.  
  
 Operazioni di ADO che non generano un errore non hanno alcun effetto **errori** raccolta. Usare la [cancellare](../../../ado/reference/ado-api/clear-method-ado.md) metodo cancellare manualmente le **errori** raccolta.  
  
 Il set di **errore** gli oggetti di **errori** raccolta descrive tutti gli errori che si sono verificati in risposta a una singola istruzione. L'enumerazione degli errori specifici di **errori** raccolta consente alle routine di gestione degli errori determinare la causa e l'origine di un errore in modo più preciso ed eseguire i passaggi appropriati per il ripristino.  
  
 Alcune proprietà e metodi restituiscono gli avvisi che vengono visualizzati come **errore** gli oggetti nel **errori** raccolta ma non arrestano l'esecuzione del programma. Prima di chiamare il [Risincronizza](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md), o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) metodi su un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, il [aprire](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo su un **connessione** dell'oggetto, o impostare il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà su un **Recordset** dell'oggetto, chiamare il **Clear**metodo su di **errori** raccolta. In questo modo è possibile leggere il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà delle **errori** insieme per provare gli avvisi restituiti.  
  
> [!NOTE]
>  Vedere le **errore** argomento di oggetto per una spiegazione più dettagliata del modo in cui una singola operazione di ADO può generare più errori.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Gli eventi, metodi e proprietà di raccolta errori](../../../ado/reference/ado-api/errors-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)   
 [Appendice a: Providers](../../../ado/guide/appendixes/appendix-a-providers.md)
