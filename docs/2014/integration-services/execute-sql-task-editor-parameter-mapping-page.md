---
title: Editor attività Esegui SQL (pagina Mapping parametri) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7508324be0bef23ba0590bb181135512d75701e7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059035"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>Editor attività Esegui SQL (pagina Mapping parametri)
  Usare la pagina **Mapping parametri** della finestra di dialogo **Editor attività Esegui SQL** per eseguire il mapping tra variabili e parametri nell'istruzione SQL.  
  
 Per informazioni su questa attività, vedere [Attività Esegui SQL](control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opzioni  
 **Nome variabile**  
 Dopo aver aggiunto un mapping dei parametri facendo clic su **Aggiungi**, selezionare una variabile di sistema o una variabile definita dall'utente nell'elenco oppure fare clic su \<**Nuova variabile**> per aggiungere una nuova variabile usando la finestra di dialogo **Aggiungi variabile**.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
 **Direction**  
 Consente di selezionare la direzione del parametro. Eseguire il mapping di ogni variabile a un parametro di input, a un parametro di output o a un codice restituito.  
  
 **Tipo di dati**  
 Selezionare il tipo di dati del parametro. L'elenco dei tipi di dati disponibili è specifico del provider selezionato per la gestione connessione utilizzata dall'attività.  
  
 **Nome parametro**  
 Consente di specificare un nome per il parametro.  
  
 A seconda del tipo di gestione connessione utilizzata dall'attività, è necessario specificare numeri o nomi di parametri. Alcuni tipi di gestioni delle connessioni prevedono che il primo carattere del nome del parametro sia il segno \@, nomi specifici come \@Param1 oppure nomi di colonna come nomi di parametri.  
  
 **Argomenti correlati:** [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **Dimensioni parametro**  
 Fornisce le dimensioni dei parametri a lunghezza variabile, ad esempio stringhe e campi binario.  
  
 Tale impostazione assicura che il provider allochi spazio sufficiente per i valori dei parametri a lunghezza variabile.  
  
 **Aggiungere**  
 Fare clic su questo pulsante per aggiungere un mapping dei parametri.  
  
 **Rimuovi**  
 Selezionare un mapping dei parametri nell'elenco e quindi fare clic su **Rimuovi**.  
  
## <a name="see-also"></a>Vedi anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Esegui SQL &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor attività Esegui SQL &#40;pagina del set di risultati&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference)  
  
  
