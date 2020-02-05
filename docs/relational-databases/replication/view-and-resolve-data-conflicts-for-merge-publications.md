---
title: Visualizzare e risolvere i conflitti di dati (merge)
description: Informazioni su come visualizzare e risolvere i conflitti di dati per una pubblicazioni di tipo merge per SQL Server.
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79dc4b26ee543aa99b9fc90e29f7bb6c7d571555
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321888"
---
# <a name="conflict-resolution-for-merge-replication"></a>Risoluzione dei conflitti per la replica di tipo merge
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I conflitti nella replica di tipo merge vengono risolti in base al sistema di risoluzione specificato per ogni articolo. Per impostazione predefinita, i conflitti vengono risolti senza che sia necessario l'intervento dell'utente. È tuttavia possibile visualizzare i conflitti e modificare il risultato della risoluzione nel Visualizzatore conflitti di replica [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 I dati dei conflitti sono disponibili nel Visualizzatore conflitti di replica per l'intervallo di tempo specificato per il periodo di memorizzazione dei conflitti, che per impostazione predefinita è di 14 giorni. Per impostare il periodo di memorizzazione dei conflitti, eseguire una delle operazioni seguenti:  
  
-   Specificare un valore del periodo di memorizzazione per il parametro `@conflict_retention` di [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Specificare il valore **conflict_retention** per il parametro `@property` e un valore del periodo di memorizzazione per il parametro `@value` di [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Per impostazione predefinita, le informazioni sui conflitti vengono archiviate:    
-   Nel server di pubblicazione e nel Sottoscrittore se il livello di compatibilità della pubblicazione è pari a 90RTM o superiore.   
-   Nel server di pubblicazione se il livello di compatibilità della pubblicazione è inferiore a 80RTM.   
-   Nel server di pubblicazione se i Sottoscrittori eseguono [!INCLUDE[ssEW](../../includes/ssew-md.md)]. I dati in conflitto non possono essere archiviati nei sottoscrittori di [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 L'archivio delle informazioni sui conflitti viene controllato dalla proprietà **conflict_logging** della pubblicazione. Per altre informazioni, vedere [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) e [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 I conflitti possono inoltre essere risolti in modo interattivo durante la sincronizzazione tramite il sistema di risoluzione interattivo [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Il sistema di risoluzione interattivo è disponibile tramite Gestione sincronizzazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Per altre informazioni, vedere [Sincronizzare una sottoscrizione mediante Gestione sincronizzazione Microsoft Windows &#40;Gestione sincronizzazione Microsoft Windows&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="resolve-conflicts"></a>Risolvere i conflitti  
  
1.  Connettersi al server di pubblicazione, o al Sottoscrittore se appropriato, in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione per la quale si desidera visualizzare i conflitti e quindi scegliere **Visualizza conflitti**.  
  
    > [!NOTE]  
    >  Se è stato specificato il valore **'subscriber'** per la proprietà **conflict_logging** , la voce di menu **Visualizza conflitti** non sarà disponibile. Per visualizzare i conflitti, avviare ConflictViewer.exe dal prompt dei comandi. Per impostazione predefinita, ConflictViewer.exe si trova nella directory Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Per un elenco di parametri di avvio validi, eseguire ConflictViewer.exe -?.  
  
4.  Nella finestra di dialogo **Seleziona tabella con conflitti** selezionare un database, una pubblicazione e una tabella per cui visualizzare i conflitti.  
  
5.  Nel Visualizzatore conflitti di replica è possibile:  
  
    -   Filtrare le righe con i pulsanti a destra della griglia superiore.  
  
    -   Selezionare una riga nella griglia superiore per visualizzare le informazioni su tale riga nella griglia inferiore.  
  
    -   Selezionare una o più righe nella griglia superiore e quindi fare clic su **Rimuovi**, che equivale a fare clic sul pulsante **Invia riga in conflitto confermata** , senza apportare alcuna modifica ai dati.  
  
    -   Fare clic sul pulsante delle proprietà ( **...** ) per visualizzare altre informazioni su una colonna coinvolta in un conflitto.  
  
    -   Modificare i dati nella colonna **Riga in conflitto confermata** o **Riga in conflitto ignorata** prima di inviare i dati, che sono di sola lettura se la colonna è grigia.  
  
    -   Fare clic su **Invia riga in conflitto confermata** per accettare la riga designata come riga confermata.  
  
    -   Fare clic su **Invia riga in conflitto ignorata** per non accettare la risoluzione e per propagare a tutti i nodi della topologia il valore designato come ignorato.  
  
    -   Selezionare **Registra informazioni dettagliate sul conflitto** per registrare i dati del conflitto in un file. Per specificare un percorso per il file, scegliere **Opzioni** dal menu **Visualizza**. Immettere un valore o fare clic sul pulsante Sfoglia ( **...** ) e quindi passare al file appropriato. Fare clic su **OK** per chiudere la finestra di dialogo **Opzioni** .  
  
6.  Chiudere il Visualizzatore conflitti di replica.  

## <a name="view-conflict-information"></a>Visualizzare le informazioni sui conflitti
Quando si risolve un conflitto in una replica di tipo merge, i dati della riga non confermata vengono scritti in una tabella di conflitti. I dati relativi al conflitto possono essere visualizzati a livello di programmazione tramite le stored procedure di replica. Per altre informazioni, vedere [Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Notare i valori delle colonne seguenti nel set di risultati:  
  
    -   **centralized_conflicts** : 1 indica che le righe con conflitti vengono archiviate nel server di pubblicazione, mentre 0 indica che le righe con conflitti non vengono archiviate nel server di pubblicazione.  
  
    -   **decentralized_conflicts** : 1 indica che le righe con conflitti vengono archiviate nel Sottoscrittore, mentre 0 indica che le righe con conflitti non vengono archiviate nel Sottoscrittore.  
  
        > [!NOTE]  
        >  Per definire il comportamento della registrazione dei conflitti relativi a una pubblicazione di tipo merge, viene usato il parametro `@conflict_logging` di [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Il parametro `@centralized_conflicts` è deprecato.  
  
     Nella tabella seguente sono descritti i valori di queste colonne sulla base del valore specificato per `@conflict_logging`.  
  
    |Valore della proprietà @conflict_logging|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  Nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione del Sottoscrittore eseguire [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Specificare il valore `@publication` per restituire le informazioni sui conflitti solo per articoli che appartengono a una pubblicazione specifica. In tal modo per gli articoli con conflitti verranno restituite le informazioni della tabella dei conflitti. Notare il valore di **conflict_table** per qualsiasi articolo di interesse. Se il valore di **conflict_table** per un articolo è NULL, eliminare i conflitti che si sono verificati in questo articolo.  
  
3.  (Facoltativo) Rivedere le righe con conflitti presenti negli articoli di interesse. A seconda dei valori di **centralized_conflicts** e **decentralized_conflicts** ottenuti al passaggio 1, eseguire una delle operazioni seguenti:  
  
    -   Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Specificare una tabella dei conflitti per l'articolo (ottenuta al passaggio 1) per `@conflict_table`. (Facoltativo) Specificare il valore `@publication` per limitare le informazioni restituite sui conflitti a una pubblicazione specifica. In tal modo verranno restituiti i dati della riga e altre informazioni sulla riga non confermata.  
  
    -   Nel database di sottoscrizione del Sottoscrittore eseguire [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Specificare una tabella dei conflitti per l'articolo (ottenuta al passaggio 1) per `@conflict_table`. In tal modo verranno restituiti i dati della riga e altre informazioni sulla riga non confermata.  
  
## <a name="conflict-where-delete-failed"></a>Conflitto con eliminazione non riuscita   
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Notare i valori delle colonne seguenti nel set di risultati:  
  
    -   **centralized_conflicts** : 1 indica che le righe con conflitti vengono archiviate nel server di pubblicazione, mentre 0 indica che le righe con conflitti non vengono archiviate nel server di pubblicazione.  
  
    -   **decentralized_conflicts** : 1 indica che le righe con conflitti vengono archiviate nel Sottoscrittore, mentre 0 indica che le righe con conflitti non vengono archiviate nel Sottoscrittore.  
  
        > [!NOTE]  
        >  Per definire il comportamento della registrazione dei conflitti relativi a una pubblicazione di tipo merge, viene usato il parametro `@conflict_logging` di [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Il parametro `@centralized_conflicts` è deprecato.  
  
2.  Nel database di pubblicazione del server di pubblicazione o nel database di sottoscrizione del Sottoscrittore eseguire [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Specificare un valore per `@publication` in modo da restituire le informazioni della tabella dei conflitti solo per articoli che appartengono a una pubblicazione specifica. In tal modo per gli articoli con conflitti verranno restituite le informazioni della tabella dei conflitti. Notare il valore di **source_object** per qualsiasi articolo di interesse. Se il valore di **conflict_table** per un articolo è NULL, eliminare i conflitti che si sono verificati in questo articolo.  
  
3.  (Facoltativo) Rivedere le informazioni sui conflitti per i conflitti di eliminazione. A seconda dei valori di **centralized_conflicts** e **decentralized_conflicts** ottenuti al passaggio 1, eseguire una delle operazioni seguenti:  
  
    -   Nel database di pubblicazione del server di pubblicazione eseguire [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Specificare il nome della tabella di origine (ottenuta al passaggio 1) nella quale si è verificato il conflitto per `@source_object`. (Facoltativo) Specificare il valore `@publication` per limitare le informazioni restituite sui conflitti a una pubblicazione specifica. In tal modo verranno restituite solo le informazioni sui conflitti di eliminazione archiviate nel server di pubblicazione.  
  
    -   Nel database di sottoscrizione del Sottoscrittore eseguire [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Specificare il nome della tabella di origine (ottenuta al passaggio 1) nella quale si è verificato il conflitto per `@source_object`. (Facoltativo) Specificare il valore `@publication` per limitare le informazioni restituite sui conflitti a una pubblicazione specifica. In tal modo verranno restituite solo le informazioni sui conflitti di eliminazione archiviate nel Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Specificare un sistema di risoluzione dei conflitti dell'articolo di merge](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
