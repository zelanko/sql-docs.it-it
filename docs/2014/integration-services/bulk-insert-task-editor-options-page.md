---
title: Editor attività Inserimento bulk (pagina Opzioni) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.options.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: b3702811-3eb8-4b28-9190-5ae7a1a7bb6f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5f9c37fc722613b8f30772fd825663b2dfcf9b54
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84924672"
---
# <a name="bulk-insert-task-editor-options-page"></a>Editor attività Inserimento bulk (pagina Opzioni)
  Utilizzare la pagina **Opzioni** della finestra di dialogo **Editor attività Inserimento bulk** per impostare le proprietà relative all'operazione di inserimento bulk. L'attività Inserimento bulk copia grandi quantità di dati in una [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tabella o vista.  
  
 Per altre informazioni sull'uso degli inserimenti di massa, vedere [Attività Inserimento bulk](control-flow/bulk-insert-task.md) e [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
## <a name="options"></a>Opzioni  
 **CodePage**  
 Consente di specificare la tabella codici dei dati contenuti nel file.  
  
 **DataFileType**  
 Consente di specificare il valore di tipo di dati da utilizzare nell'operazione di caricamento.  
  
 **BatchSize**  
 Consente di specificare il numero di righe di un batch. Il valore predefinito è l'intero file di dati. Se si imposta **BatchSize** su zero, i dati vengono caricati in un singolo batch.  
  
 **LastRow**  
 Consente di specificare l'ultima riga da copiare.  
  
 **FirstRow**  
 Consente di specificare la riga dalla quale iniziare la copia.  
  
 **Opzioni**  
 |Termine|Definizione|  
|----------|----------------|  
|**Vincoli CHECK**|Selezionare questa opzione per verificare i vincoli di colonna e tabella.|  
|**Mantieni valori Null**|Selezionare questa opzione per mantenere i valori Null durante l'operazione di inserimento bulk anziché inserire tutti i valori predefiniti per le colonne vuote.|  
|**Consenti IDENTITY_INSERT**|Selezionare questa opzione per inserire valori esistenti in una colonna Identity.|  
|**Blocco di tabella**|Selezionare questa opzione per bloccare la tabella durante l'inserimento bulk.|  
|**Attive trigger**|Selezionare questa opzione per attivare tutti i trigger di eliminazione, aggiornamento o inserimento nella tabella.|  
  
 **SortedData**  
 Consente di specificare la clausola ORDER BY nell'istruzione di inserimento bulk. Il nome della colonna deve corrispondere a una colonna valida della tabella di destinazione. Il valore predefinito è `false`. Questo valore implica che i dati non vengono ordinati da una clausola ORDER BY.  
  
 **MaxErrors**  
 Consente di specificare il numero massimo di errori che possono verificarsi prima dell'annullamento dell'operazione di inserimento bulk. Un valore pari a 0 indica che è consentito un numero infinito di errori.  
  
> [!NOTE]  
>  Ogni riga che non è possibile importare tramite l'operazione di caricamento bulk viene considerata un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Inserimento bulk &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor attività Inserimento bulk &#40;pagina connessione&#41;](../../2014/integration-services/bulk-insert-task-editor-connection-page.md)   
 [Pagina espressioni](expressions/expressions-page.md)   
 [Flusso di controllo](control-flow/control-flow.md)  
  
  
