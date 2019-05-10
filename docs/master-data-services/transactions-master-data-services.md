---
title: Transazioni (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 887380136c96cb9cb1dbcd8d9d04b486daaf6659
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65486100"
---
# <a name="transactions-master-data-services"></a>Transazioni (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]



--------------------------------------------------
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], viene registrata una transazione ogni volta che viene eseguita un'azione su un membro. Le transazioni possono essere visualizzate da tutti gli utenti e possono essere invertite dagli amministratori. Nelle transazioni vengono indicati, tra gli altri dettagli, anche la data, l'ora e l'utente che ha eseguito l'azione. Gli utenti possono aggiungere un'annotazione a una transazione, per indicare il motivo per il quale si è verificata.  
  
## <a name="when-transaction-are-recorded"></a>Quando vengono registrate le transazioni  
 Le transazioni vengono registrate quando i membri:  
  
-   Vengono creati, eliminati o riattivati.  
  
-   Vengono modificati i valori dei relativi attributi.  
  
-   Vengono spostati in una gerarchia.  
  
 Le transazioni non vengono registrate quando i valori di attributo vengono modificati dalle regole business.  
  
## <a name="view-and-manage-transactions"></a>Visualizzare e gestire transazioni  
 Nell'area funzionale **Visualizzatore** è possibile visualizzare e annotare le transazioni create, ovvero aggiungervi commenti. 
  
 Nell'area funzionale **Gestione versioni** gli amministratori possono visualizzare tutte le transazioni per tutti gli utenti per i modelli a cui possono accedere e invertire una di queste transazioni.
 
> [!NOTE]  
>  Gli amministratori possono visualizzare tutte le transazioni per tutti gli utenti a condizione che non dispongano dell'autorizzazione di sola lettura applicata nell'area funzionale **Gestione versioni**. Ad esempio, se è impostato il livello di autorizzazione di sola lettura e aggiornamento per l'amministratore, l'amministratore non può visualizzare altre transazioni utente perché l'autorizzazione di sola lettura ha la precedenza sull'autorizzazione di aggiornamento.
  
 È possibile configurare il periodo di conservazione dei dati del log delle transazioni impostando la proprietà **Conservazione log in giorni** nelle impostazioni di sistema per il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] e impostando **Giorni di conservazione log** quando si crea o si modifica un modello. Per altre informazioni, vedere [Impostazioni di sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) e [Creare un modello &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md).  
  
 Il processo di SQL Server Agent, MDS_MDM_Sample_Log_Maintenace, attiva la pulizia dei log delle transazioni e viene eseguito ogni notte. È possibile usare SQL Server Agent per modificare la pianificazione del processo.  
  
 È anche possibile chiamare le stored procedure seguenti per pulire i log delle transazioni.  
  
|Stored procedure|Descrizione|  
|----------------------|-----------------|  
|mdm.udpTransactionsCleanup|Pulisce la cronologia delle transazioni|  
|mdm.udpValidationsCleanup|Pulisce la cronologia di convalida|  
|mdm.udpEntityStagingBatchTableCleanup|Pulisce la tabella di staging|  
  
 **Esempio**  
  
```  
DECLARE @CleanupOlderThanDate date = '2014-11-11',  
@ModelID INT = 7  
--Clean up Transaction Logs  
EXEC mdm.udpTransactionsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up Validation History  
EXEC mdm.udpValidationsCleanup @ModelID, @CleanupOlderThanDate;  
  
--Clean up EBS tables  
EXEC mdm.udpEntityStagingBatchTableCleanup @ModelID, @CleanupOlderThanDate;  
  
```  
  
## <a name="system-settings"></a>Impostazioni sistema  
 In [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] è disponibile un'impostazione che determina se le transazioni vengono registrate quando i record vengono gestiti in modo temporaneo. È possibile regolare questa impostazione in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] o direttamente nella tabella Impostazioni sistema del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per altre informazioni, vedere [Impostazioni di sistema &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
 In caso di importazione di dati in questa versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è possibile specificare se registrare transazioni all'avvio della stored procedure. Per altre informazioni, vedere [Stored procedure di gestione temporanea &#40;Master Data Services&#41;](../master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="concurrency"></a>Concorrenza  
 Se un particolare valore dell'entità viene mostrato contemporaneamente in più di una sessione dello strumento di esplorazione, sono possibili modifiche simultanee allo stesso valore. Le modifiche simultanee non verranno rilevate automaticamente da MDS. Questa situazione si può verificare quando più utenti utilizzano Esplora di MDS nel Web browser da più sessioni, ad esempio da più computer, più schede o finestre del browser o più account utente.  
  
 Più utenti possono aggiornare gli stessi valori dell'entità senza errore, nonostante transazioni abilitate. In genere, l'ultima modifica al valore in una sequenza di tempo avrà la precedenza. Il conflitto duplicato delle modifiche può essere osservato manualmente nella cronologia delle transazioni e invertito manualmente dall'amministratore. La cronologia delle transazioni mostra le singole transazioni in base a **Valore precedente** e **Nuovo valore** per l'attributo in questione di ogni sessione, ma non risolve automaticamente il conflitto se esistono più valori **Nuovi valori** per lo stesso valore precedente.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Annullare un'azione invertendo una transazione (solo amministratori).|[Invertire una transazione &#40;Master Data Services&#41;](../master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="external-resources"></a>Risorse esterne  
 Post di blog su [transazioni, problemi di convalida e pulizia della tabella di gestione temporanea](https://go.microsoft.com/fwlink/p/?LinkId=615374) nel sito msdn.com.  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Amministratori &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   [Annotazioni &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)  
  
  
