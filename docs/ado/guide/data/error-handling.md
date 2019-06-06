---
title: Gestione degli errori | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56d41b8c8fddff4d49cdb213834f45eac7fd5462
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700754"
---
# <a name="error-handling"></a>Gestione degli errori
ADO utilizza diversi metodi per notificare a un'applicazione di errori che si verificano. In questa sezione vengono descritti i tipi di errori che possono verificarsi quando si utilizza ADO e le modalità di notifica all'applicazione. Conclude l'articolo con i suggerimenti su come gestire tali errori.  
  
## <a name="how-does-ado-report-errors"></a>Come segnala errori ADO?  
 ADO si invia una notifica sugli errori in diversi modi:  
  
-   Errori ADO generano un errore di run-time. Gestire un errore ADO farebbe qualsiasi altro errore di run-time, ad esempio usando un **in caso di errore** istruzione in Visual Basic.  
  
-   Il programma può ricevere errori da OLE DB. Un errore OLE DB genera anche un errore in fase di esecuzione.  
  
-   Se l'errore è specifico per il provider di dati, uno o più **errore** gli oggetti vengono inseriti nel **errori** raccolta del **connessione** oggetto che è stato usato per accedere ai dati archivio cui si è verificato l'errore.  
  
-   Se il processo che ha generato un evento ha anche generato un errore, le informazioni sull'errore viene inseriti un **errore** dell'oggetto e passato come parametro per l'evento. Visualizzare [gestione degli eventi ADO](../../../ado/guide/data/handling-ado-events.md) per altre informazioni sugli eventi.  
  
-   I problemi che si verificano durante l'elaborazione batch di aggiornamenti o altre operazioni bulk che includono un **Recordset** possono essere indicati dal **stato** proprietà del **Recordset**. Ad esempio, le violazioni di vincolo dello schema o autorizzazioni insufficienti possono essere specificate da **RecordStatusEnum** valori.  
  
-   Problemi che si verificano che interessano un determinato **campo** presenti nel record corrente vengono inoltre indicati tramite il **stato** proprietà di ogni **campo** nel **campi**  raccolta del **Record** oppure **Recordset**. Ad esempio, gli aggiornamenti che non è stato possibile completare o tipi di dati incompatibili possono essere specificati da **FieldStatusEnum** valori.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Errori ADO](../../../ado/guide/data/ado-errors.md)  
  
-   [Errori del provider](../../../ado/guide/data/provider-errors.md)  
  
-   [Informazioni sugli errori associati ai campi](../../../ado/guide/data/field-related-error-information.md)  
  
-   [Informazioni sugli errori associati ai recordset](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [Gestione degli errori in altri linguaggi](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [Prevenzione degli errori](../../../ado/guide/data/anticipating-errors.md)
