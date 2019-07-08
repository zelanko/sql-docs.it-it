---
title: Avviare o arrestare un set di raccolta | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection sets [SQL Server], stopping
- collection sets [SQL Server], starting
ms.assetid: 48a7b2fe-6bc3-4278-a7ec-1babc1290345
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 12e425f889826a5fc9464ee8c85c88ab05043f4b
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580294"
---
# <a name="start-or-stop-a-collection-set"></a>Avviare o arrestare un set di raccolta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come avviare o arrestare un set di raccolte in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Prerequisiti](#Prerequisites)  
  
     [Indicazioni](#Recommendations)  
  
     [Security](#Security)  
  
-   **Per avviare o arrestare un set di raccolta utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le stored procedure dell'agente di raccolta dati e le viste del catalogo vengono archiviate nel database **msdb** .  
  
-   A differenza delle normali stored procedure, i parametri per le stored procedure dell'agente di raccolta dati utilizzano parametri fortemente tipizzati e non supportano la conversione automatica del tipo di dati. Se tali parametri non vengono chiamati con i tipi di dati corretti per i parametri di input, come indicato nella descrizione dell'argomento, la stored procedure restituisce un errore.  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario che il servizio SQL Server Agent sia avviato.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Per ottenere informazioni sui set di raccolta, eseguire una query sulla vista del catalogo [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) .  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo predefinito del database **dc_operator** . Se al set di raccolta non è associato un account proxy, è richiesta l'appartenenza al ruolo predefinito del server **sysadmin** . Esempi  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-start-a-collection-set"></a>Per avviare un set di raccolta  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , **Raccolta dati**, quindi **Set di raccolta dati di sistema**.  
  
2.  Fare clic con il pulsante destro del mouse sul set di raccolta che si vuole avviare, quindi scegliere **Avviare il set di raccolta dati**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     A message box displays the results of this action, and a green arrow on the icon for the collection set indicates that the collection set has started.  
  
#### <a name="to-stop-a-collection-set"></a>Per arrestare un set di raccolta  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , **Raccolta dati**, quindi **Set di raccolta dati di sistema**.  
  
2.  Fare clic con il pulsante destro del mouse sul set di raccolta che si vuole arrestare, quindi scegliere **Arrestare il set di raccolta dati**.  
  
     In una finestra di messaggio verranno visualizzati i risultati di questa azione, mentre un cerchio rosso sull'icona del set di raccolta indica che il set di raccolta è stato arrestato.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-start-a-collection-set"></a>Per avviare un set di raccolta  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si usa [sp_syscollector_start_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md) per avviare il set di raccolta con l'ID `1`.  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
#### <a name="to-stop-a-collection-set"></a>Per arrestare un set di raccolta  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si usa [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md) per arrestare il set di raccolta con l'ID `1`.  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
