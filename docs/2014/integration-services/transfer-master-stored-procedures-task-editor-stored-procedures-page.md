---
title: Editor attività Trasferisci stored procedure master (pagina stored procedure) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferstoredprocedurestask.storedprocedures.f1
helpviewer_keywords:
- Transfer Stored Procedures Task Editor
ms.assetid: 5fcf171e-cc0b-4c24-8eb5-3a4b4775e64a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0cd0b269c0ced445017d573cfad08a767d5f2008
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439988"
---
# <a name="transfer-master-stored-procedures-task-editor-stored-procedures-page"></a>Editor attività Trasferisci stored procedure master (pagina Stored procedure)
  Usare la pagina **Stored procedure** della finestra di dialogo **Editor attività Trasferisci stored procedure master** per specificare le proprietà per la copia di una o più stored procedure definite dall'utente dal database **master** di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un database **master** di un'altra istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per altre informazioni su questa attività, vedere [Attività Trasferisci stored procedure master](control-flow/transfer-master-stored-procedures-task.md).  
  
> [!NOTE]  
>  L'attività consente solo il trasferimento di stored procedure appartenenti a **dbo** da un database **master** del server di origine a un database **master** del server di destinazione. Per poter creare stored procedure nel server di destinazione, gli utenti devono disporre dell'autorizzazione CREATE PROCEDURE nel database **master** del server di destinazione o essere membri del ruolo predefinito del server **sysadmin** nel server di destinazione.  
  
## <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di destinazione.  
  
 **IfObjectExists**  
 Selezionare la modalità con cui l'attività deve gestire le stored procedure definite dall'utente che hanno lo stesso nome di stored procedure già esistenti nel database **master** del server di destinazione.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**FailTask**|L'attività viene interrotta se nel database **master** del server di destinazione esistono già stored procedure con lo stesso nome.|  
|**Overwrite**|L'attività sovrascrive le stored procedure con lo stesso nome presenti nel database **master** del server di destinazione.|  
|**Ignora**|L'attività ignora le stored procedure con lo stesso nome presenti nel database **master** del server di destinazione.|  
  
 **TransferAllStoredProcedures**  
 Selezionare un valore per indicare se nel server di destinazione debbano essere copiate tutte le stored procedure definite dall'utente nel database **master** del server di origine.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**True**|Copia tutte le stored procedure definite dall'utente nel database **master** .|  
|**False**|Copia solo le stored procedure specificate.|  
  
 **StoredProceduresList**  
 Selezionare le stored procedure definite dall'utente nel database **master** del server di origine da copiare nel database **master** del server di destinazione. Questa opzione è disponibile solo quando la proprietà **TransferAllStoredProcedures** è impostata su **False**.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Attività Integration Services](control-flow/integration-services-tasks.md)   
 [Editor attività Trasferisci stored procedure master &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina espressioni](expressions/expressions-page.md)   
 [Gestione connessione SMO](connection-manager/smo-connection-manager.md)  
  
  
