---
title: Rilevamento e risoluzione dei conflitti per l'aggiornamento in coda | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 413fc991d9f908d4390de109dededa07056e5b63
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54125532"
---
# <a name="updatable-subscriptions---queued-updating-conflict-resolution"></a>Sottoscrizioni aggiornabili - Risoluzione dei conflitti per l'aggiornamento in coda
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Dato che le sottoscrizioni ad aggiornamento in coda consentono la modifica degli stessi dati in più posizioni, è possibile che durante la sincronizzazione dei dati nel server di pubblicazione si verifichino conflitti. I conflitti vengono rilevati quando le modifiche vengono sincronizzate con il server di pubblicazione e vengono risolti in base ai criteri di risoluzione selezionati durante la creazione della pubblicazione. È possibile che si verifichino i conflitti seguenti:  
  
-   Conflitti di aggiornamento e inserimento. Questo tipo di conflitti si verifica quando gli stessi dati vengono modificati in due posizioni diverse. In questo caso, vengono confermate solo le modifiche apportate in una posizione.  
  
-   Conflitti di eliminazione. Si verificano se la stessa riga viene eliminata in una posizione e modificata in un'altra.  
  
 Il rilevamento e la risoluzione dei conflitti può richiedere tempi lunghi e un numero elevato di risorse. È pertanto consigliabile ridurre al minimo i conflitti nelle applicazioni tramite la creazione di partizioni di dati in modo da consentire la modifica di subset di dati diversi in Sottoscrittori diversi.  
  
## <a name="detecting-conflicts"></a>Rilevamento dei conflitti  
 Quando si crea una pubblicazione e si abilita l'aggiornamento in coda, viene aggiunta alla tabella sottostante una colonna di tipo **uniqueidentifier** (**msrepl_tran_version**) con il valore predefinito **newid()** . Quando si modificano i dati pubblicati nel server di pubblicazione o nel Sottoscrittore, le righe ricevono un nuovo identificatore univoco globale (GUID) a indicare che esiste una nuova versione della riga. L'agente di lettura coda utilizza questa colonna durante la sincronizzazione per determinare se esiste un conflitto.  
  
 Le transazioni inserite in una coda mantengono i valori di versione nuovi e vecchi delle righe. Quando la transazione viene applicata al server di pubblicazione, vengono confrontati i GUID della transazione e il GUID della pubblicazione. Se il vecchio GUID archiviato nella transazione corrisponde al GUID della pubblicazione, la pubblicazione viene aggiornata e il nuovo GUID viene assegnato alla riga generata dal Sottoscrittore. In seguito all'aggiornamento della pubblicazione con il GUID della transazione, le versioni delle righe nella pubblicazione corrispondono alle versioni della transazione.  
  
 Se il vecchio GUID archiviato nella transazione non corrisponde al GUID della pubblicazione, viene rilevato un conflitto. Il nuovo GUID della pubblicazione indica che esistono due diverse versioni della riga: una versione nella transazione inviata dal Sottoscrittore e una versione più recente nel server di pubblicazione. Ciò significa che un altro Sottoscrittore o il server di pubblicazione hanno aggiornato la stessa riga della pubblicazione prima della sincronizzazione della transazione da parte del server di sottoscrizione.  
  
 A differenza della replica di tipo merge, le colonne GUID non vengono utilizzate per identificare la riga stessa, ma per verificare se è stata modificata.  
  
## <a name="resolving-conflicts"></a>Risoluzione dei conflitti  
 Quando si crea una pubblicazione configurata per l'aggiornamento in coda, si seleziona un sistema di risoluzione dei conflitti da utilizzare qualora venissero rilevati dei conflitti. L'agente di lettura coda gestisce le versioni diverse della stessa riga rilevate durante la sincronizzazione in base al sistema di risoluzione dei conflitti. Dopo la creazione della pubblicazione è tuttavia possibile modificare i criteri di risoluzione dei conflitti a condizione che non esistano sottoscrizioni della pubblicazione. Le opzioni del sistema di risoluzione dei conflitti sono le seguenti:  
  
-   Prevale il server di pubblicazione (impostazione predefinita)  
  
-   Prevale il server di pubblicazione e la sottoscrizione viene reinizializzata  
  
-   Prevale il Sottoscrittore  
  
 I conflitti vengono registrati e possono essere visualizzati tramite il Visualizzatore conflitti.  
  
 **Per impostare i criteri di risoluzione dei conflitti per l'aggiornamento in coda**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Impostare le opzioni di risoluzione dei conflitti per l'aggiornamento in coda &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
-   Programmazione Transact-SQL della replica: [Abilitare le sottoscrizioni aggiornabili per le pubblicazioni transazionali](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **Per visualizzare i conflitti di dati**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Visualizzare i conflitti di dati per le pubblicazioni transazionali &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>Prevale il server di pubblicazione  
 Quando il criterio di risoluzione dei conflitti è impostato su Prevale il server di pubblicazione, la consistenza transazionale viene mantenuta in base ai dati del server di pubblicazione. Viene eseguito il rollback della transazione in conflitto nel Sottoscrittore in cui è stata inizializzata.  
  
 Quando l'agente di lettura coda rileva un conflitto, vengono generati i comandi di compensazione, i quali vengono distribuiti al Sottoscrittore inserendoli nel database di distribuzione. L'agente di distribuzione applica quindi i comandi di compensazione al Sottoscrittore che ha originato la transazione in conflitto. Le azioni di compensazione aggiornano le righe nel Sottoscrittore in modo che corrispondano alla riga nel server di pubblicazione.  
  
 Fino a quando non vengono applicati i comandi di compensazione, è possibile leggere i risultati di una transazione di cui verrà eseguito il rollback nel Sottoscrittore. Ciò equivale a una lettura dirty, ovvero al livello di isolamento Read Uncommitted. Per le successive transazioni dipendenti che possono verificarsi, non è prevista alcuna compensazione. Vengono comunque rispettati i limiti delle transazioni e viene eseguito il commit, oppure in caso di conflitto, il rollback di tutte le azioni all'interno di una transazione.  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>Prevale il server di pubblicazione e la sottoscrizione viene reinizializzata  
 La reinizializzazione del Sottoscrittore per la risoluzione dei conflitti consente di mantenere un grado elevato di consistenza transazionale nel Sottoscrittore, ma può richiedere molto tempo se la pubblicazione contiene una quantità di dati elevata.  
  
 Quando l'agente di lettura coda rileva un conflitto, le altre transazioni della coda, compresa la transazione in conflitto, vengono rifiutate e il Sottoscrittore viene contrassegnato per la reinizializzazione. Il successivo snapshot generato per la pubblicazione viene applicato dall'agente di distribuzione al Sottoscrittore.  
  
### <a name="subscriber-wins"></a>Prevale il Sottoscrittore  
 Il rilevamento dei conflitti in base ai criteri Prevale il Sottoscrittore implica che l'ultima transazione del Sottoscrittore che aggiorna il server di pubblicazione risulta prioritaria. In questo caso, quando viene rilevato un conflitto, viene comunque utilizzata la transazione inviata dal Sottoscrittore e il server di pubblicazione viene aggiornato. Questi criteri sono adatti alle applicazioni in cui tali modifiche non compromettono l'integrità dei dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
