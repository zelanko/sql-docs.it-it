---
title: Specificare che le eliminazioni non devono essere rilevate per articoli di Merge (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 25e0eb6e257098d075cca4fb4d36d586efa1841b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52772483"
---
# <a name="specify-that-deletes-should-not-be-tracked-for-merge-articles-replication-transact-sql-programming"></a>Disattivazione del rilevamento delle eliminazioni per gli articoli di merge (programmazione Transact-SQL della replica)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Per impostazione predefinita, la replica di tipo merge consente di sincronizzare i comandi DELETE tra server di pubblicazione e Sottoscrittore. Con la replica di tipo merge le righe vengono mantenute nel database di sottoscrizione anche se sono state eliminate dalla pubblicazione e viceversa. È possibile specificare a livello di programmazione che i comandi DELETE vengano ignorati durante la creazione di un nuovo articolo oppure attivare questa funzionalità in un secondo momento utilizzando le stored procedure di replica.  
  
> [!IMPORTANT]  
>  L'attivazione di questa funzionalità causa la non convergenza pertanto i dati presenti nel Sottoscrittore non rifletteranno accuratamente i dati presenti nel server di pubblicazione. È necessario implementare un meccanismo personalizzato per la rimozione manuale delle righe eliminate.  
  
### <a name="to-specify-that-deletes-be-ignored-for-a-new-merge-article"></a>Per specificare che si desidera ignorare le eliminazioni per un nuovo articolo di merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Specificare il valore `false` per **@delete_tracking**. Per altre informazioni, vedere [definire un articolo](define-an-article.md).  
  
    > [!NOTE]  
    >  Se la tabella di origine di un articolo è già pubblicata in un'altra pubblicazione, il valore di **delete_tracking** deve essere uguale per entrambi gli articoli.  
  
### <a name="to-specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>Per specificare che si desidera ignorare le eliminazioni per un articolo di merge esistente  
  
1.  Per determinare se la compensazione errori è abilitata per un articolo, eseguire [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e prendere nota del valore di **delete_tracking** nel set di risultati. Se questo valore è **0**, le eliminazioni vengono già ignorate.  
  
2.  Se il valore ottenuto al passaggio 1 è **1**, eseguire [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) nel database di pubblicazione del server di pubblicazione. Specificare il valore **delete_tracking** per **@property**e il valore `false` per **@value**.  
  
    > [!NOTE]  
    >  Se la tabella di origine di un articolo è già pubblicata in un'altra pubblicazione, il valore di **delete_tracking** deve essere uguale per entrambi gli articoli.  
  
## <a name="see-also"></a>Vedere anche  
 [Ottimizzare le prestazioni della replica di tipo merge con il rilevamento condizionale delle eliminazioni](../merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
