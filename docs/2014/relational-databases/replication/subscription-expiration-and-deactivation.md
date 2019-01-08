---
title: Scadenza e disattivazione delle sottoscrizioni | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Distributors [SQL Server replication], distribution retention period
- subscriptions [SQL Server replication], expiration
- publications [SQL Server replication], publication retention periods
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- publication retention periods
- distribution retention period
- subscriptions [SQL Server replication], deactivation
- deactivating subscriptions
ms.assetid: 4d03f5ab-e721-4f56-aebc-60f6a56c1e07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89818f172ee9af09a44654dffc800bf6adc35de4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804333"
---
# <a name="subscription-expiration-and-deactivation"></a>Scadenza e disattivazione delle sottoscrizioni
  Le sottoscrizioni possono essere disattivate o scadere se non vengono sincronizzate entro il *periodo di memorizzazione*specificato. Vengono eseguite azioni diverse a seconda del tipo di replica e del periodo di memorizzazione scaduto.  
  
 Per impostare i periodi di memorizzazione, vedere [Impostare il periodo di scadenza per le sottoscrizioni](publish/set-the-expiration-period-for-subscriptions.md), [Impostare il periodo di memorizzazione per la distribuzione per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](set-distribution-retention-period-for-transactional-publications.md), e [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md).  
  
## <a name="transactional-replication"></a>Replica transazionale  
 La replica transazionale usa il periodo massimo di memorizzazione per la distribuzione (il parametro **@max_distretention** di [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)) e il periodo di memorizzazione per la pubblicazione (il parametro **@retention** di [sp_addpublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)):  
  
-   Se una sottoscrizione non è stata sincronizzata entro il periodo massimo di memorizzazione per la distribuzione (72 ore per impostazione predefinita) e nel database di distribuzione sono presenti modifiche che non sono state recapitate al Sottoscrittore, la sottoscrizione viene contrassegnata come disattivata dal processo **Eliminazione del contenuto della distribuzione** in esecuzione nel server di distribuzione. La sottoscrizione deve essere reinizializzata.  
  
-   Se una sottoscrizione non è stata sincronizzata entro il periodo di memorizzazione per la pubblicazione (336 ore per impostazione predefinita), la sottoscrizione scade e viene eliminata dal processo **Pulizia dei riferimenti alla sottoscrizione scaduta** in esecuzione nel server di pubblicazione. La sottoscrizione deve essere ricreata e sincronizzata.  
  
     Se una sottoscrizione push scade, viene completamente rimossa, a differenza delle sottoscrizioni pull, che devono essere eliminate nel Sottoscrittore. Per altre informazioni, vedere [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
## <a name="merge-replication"></a>Replica di tipo merge  
 La replica di tipo merge usa il periodo di memorizzazione per la pubblicazione (i parametri **@retention** e **@retention_period_unit** di [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)). Se una sottoscrizione è scaduta, è necessario reinizializzarla, poiché i relativi metadati vengono rimossi. Le sottoscrizioni che non vengono reinizializzate vengono rimosse mediante il processo **Pulizia dei riferimenti alla sottoscrizione scaduta** eseguito sul server di pubblicazione. Per impostazione predefinita, questo processo viene eseguito ogni giorno e rimuove tutte le sottoscrizioni push che non sono state sincronizzate per il doppio della durata del periodo di memorizzazione per la pubblicazione. Ad esempio:  
  
-   Se una pubblicazione ha un periodo di memorizzazione di 14 giorni, una sottoscrizione può scadere se non è stata sincronizzata entro 14 giorni.  
  
     Se il server di pubblicazione esegue [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versione successiva e l'agente per la sottoscrizione appartiene a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o a una versione successiva, una sottoscrizione scade solo se sono state apportate modifiche ai dati nella relativa partizione. Ad esempio, si supponga che un Sottoscrittore riceva dati relativi solo ai clienti residenti in Germania. Se il periodo di memorizzazione impostato è pari 14 giorni, la sottoscrizione scade il 14° giorno solo se sono state apportate modifiche ai dati dei clienti tedeschi negli ultimi 14 giorni.  
  
-   È possibile reinizializzare la sottoscrizione da 14 a 27 giorni dopo l'ultima sincronizzazione.  
  
-   Dopo 28 giorni dall'ultima sincronizzazione, la sottoscrizione viene rimossa mediante il processo **Pulizia dei riferimenti alla sottoscrizione scaduta** . Se una sottoscrizione push scade, viene completamente rimossa, a differenza delle sottoscrizioni pull, che devono essere eliminate nel Sottoscrittore. Per altre informazioni, vedere [Delete a Pull Subscription](delete-a-pull-subscription.md).  
  
### <a name="considerations-for-setting-the-publication-retention-period-for-merge-publications"></a>Considerazioni sull'impostazione del periodo di memorizzazione per la pubblicazione per le pubblicazioni di tipo merge  
 Tenere sempre presenti le considerazioni seguenti nell'impostazione del periodo di memorizzazione per le pubblicazioni di tipo merge:  
  
-   Il periodo di memorizzazione per le pubblicazioni di tipo merge ha un periodo di prova di 24 ore per adattarsi ai Sottoscrittori dei diversi fusi orari. Se, ad esempio, si imposta un periodo di memorizzazione di un giorno, il periodo di memorizzazione effettivo sarà di 48 ore.  
  
-   La pulizia dei metadati di replica di tipo merge dipende dal periodo di memorizzazione per la pubblicazione:  
  
    -   La replica non è in grado di eliminare i metadati dei database di pubblicazione e sottoscrizione prima della scadenza del periodo di memorizzazione. Quando si imposta un valore elevato per il periodo di memorizzazione, verificare che non sia tale da avere effetti negativi sulle prestazioni della replica. Se si prevede che la sincronizzazione di tutti i Sottoscrittori verrà eseguita regolarmente entro tale periodo di tempo, è consigliabile specificare un valore inferiore.  
  
    -   È possibile specificare che le sottoscrizioni non devono scadere (impostando il valore 0 per **@retention**), ma è consigliabile non utilizzare questo valore, poiché impedisce l'eliminazione dei metadati.  
  
-   Il periodo di memorizzazione per i server di ripubblicazione deve essere impostato su un valore uguale o minore del periodo di memorizzazione impostato nel server di pubblicazione originale. Impostare lo stesso periodo di memorizzazione delle pubblicazioni per tutti i server di pubblicazione e i relativi partner di sincronizzazione alternativi. L'impostazione di periodi di memorizzazione diversi potrebbe causare la non convergenza dei dati. Se è necessario modificare il periodo di memorizzazione della pubblicazione, reinizializzare manualmente il Sottoscrittore per evitare la non convergenza dei dati.  
  
-   Se, dopo la pulizia dei metadati, si incrementa il periodo di memorizzazione della pubblicazione e una sottoscrizione tenta di eseguire il merge con il server di pubblicazione (in cui i metadati sono già stati eliminati), a causa dell'incremento del periodo di memorizzazione la sottoscrizione non scadrà. Tuttavia, il server di pubblicazione non dispone di metadati sufficienti per scaricare le modifiche al Sottoscrittore e si avrà pertanto una situazione di non convergenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Reinizializzare le sottoscrizioni](reinitialize-subscriptions.md)   
 [Amministrazione dell'agente di replica](agents/replication-agent-administration.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
