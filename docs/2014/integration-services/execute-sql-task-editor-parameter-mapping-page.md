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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cfbb4468cb69947dfa54fb519b7698286393d578
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437368"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>Editor attività Esegui SQL (pagina Mapping parametri)
  Usare la pagina **Mapping parametri** della finestra di dialogo **Editor attività Esegui SQL** per eseguire il mapping tra variabili e parametri nell'istruzione SQL.  
  
 Per informazioni su questa attività, vedere [Attività Esegui SQL](control-flow/execute-sql-task.md) e [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md).  
  
## <a name="options"></a>Opzioni  
 **Nome variabile**  
 Dopo avere aggiunto un mapping dei parametri facendo clic su **Aggiungi**, selezionare una variabile di sistema o definita dall'utente nell'elenco oppure fare clic su \<**New variable...**> per aggiungere una nuova variabile utilizzando la finestra di dialogo **Aggiungi variabile** .  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md)  
  
 **Direzione**  
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
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Esegui SQL &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor attività Esegui SQL &#40;pagina del set di risultati&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference)  
  
  
