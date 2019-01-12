---
title: Rilevamento e risoluzione dei conflitti nella replica di tipo merge avanzata| Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5aaf7031afb1b3c148bbef2bcafd5d40f4947f8d
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132881"
---
# <a name="advanced-merge-replication-conflict-detection-and-resolution"></a>Rilevamento e risoluzione avanzati dei conflitti nella replica di tipo merge
  Se un server di pubblicazione e un Sottoscrittore sono connessi e viene eseguita la sincronizzazione, l'agente di merge rileva l'eventuale presenza di conflitti. Se vengono rilevati dei conflitti, l'agente utilizza un sistema di risoluzione dei conflitti, specificato al momento dell'aggiunta di un articolo a una pubblicazione, per determinare quali dati vengono accettati e propagati agli altri siti.  
  
> [!NOTE]  
>  Sebbene un Sottoscrittore esegua la sincronizzazione con il server di pubblicazione, i conflitti in genere si verificano tra gli aggiornamenti effettuati in diversi Sottoscrittori anziché tra gli aggiornamenti effettuati in un Sottoscrittore e nel server di pubblicazione.  
  
 La procedura di rilevamento e risoluzione dei conflitti dipende dalle opzioni seguenti, descritte in questo argomento:  
  
-   Se si specifica il rilevamento a livello di colonna, a livello di riga o a livello di record logico.  
  
-   Se si specifica il meccanismo predefinito di risoluzione basato sulla priorità o un sistema di risoluzione dei conflitti dell'articolo. Il sistema di risoluzione dei conflitti dell'articolo può essere costituito da:  
  
    -   Un *gestore della logica di business* creato con codice gestito.  
  
    -   Un *sistema di risoluzione personalizzato*basato sul modello COM.  
  
    -   Un sistema di risoluzione basato sul modello COM implementato da [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
     Se si utilizza il meccanismo di risoluzione predefinito, la procedura è determinata inoltre dal tipo di sottoscrizione selezionato: client o server.  
  
## <a name="conflict-detection"></a>Rilevamento dei conflitti  
 Una modifica dei dati viene considerata o meno un conflitto in base al tipo di rilevamento dei conflitti impostato per un articolo:  
  
-   Se si seleziona il rilevamento dei conflitti a livello di colonna, le modifiche vengono considerate in conflitto se vengono apportate alla stessa colonna e alla stessa riga in più di un nodo di replica.  
  
-   Se si seleziona il rilevamento a livello di riga, le modifiche vengono considerate in conflitto se vengono apportate a qualsiasi colonna nella stessa riga in più di un nodo di replica (le colonne interessate nelle righe corrispondenti non devono necessariamente essere le stesse).  
  
-   Se si seleziona il rilevamento a livello di record logico, le modifiche vengono considerate in conflitto se vengono apportate a qualsiasi riga nello stesso record logico in più di un nodo di replica (le colonne interessate nelle righe corrispondenti non devono necessariamente essere le stesse).  
  
 Per altre informazioni, vedere [Rilevamento e risoluzione dei conflitti nei record logici](advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 Per specificare il livello di rilevamento e risoluzione dei conflitti di un articolo, vedere [specifica del livello di risoluzione e rilevamento dei conflitti per articoli di Merge](../publish/specify-merge-replication-properties.md#interactive-conflict-resolution).  
  
## <a name="conflict-resolution"></a>Risoluzione dei conflitti  
 Dopo il rilevamento di un conflitto, l'agente di merge avvia il sistema di risoluzione dei conflitti selezionato e lo utilizza per determinare il valore in conflitto che prevale. La riga che prevale viene applicata al server di pubblicazione e al Sottoscrittore, mentre i dati della riga non confermata vengono inseriti in una tabella dei conflitti. I conflitti vengono risolti immediatamente dopo l'esecuzione del sistema di risoluzione, a meno che non si scelga di risolvere i conflitti in modo interattivo.  
  
### <a name="resolver-types"></a>Tipi di sistemi di risoluzione  
 Nella replica di tipo merge la risoluzione dei conflitti viene eseguita a livello di articolo. Per le pubblicazioni composte da numerosi articoli è possibile utilizzare diversi sistemi di risoluzione per articoli diversi oppure lo stesso sistema di risoluzione per un solo articolo, più articoli o per tutti gli articoli di una pubblicazione.  
  
 Se si desidera utilizzare il sistema di risoluzione dei conflitti predefinito basato sulle priorità, non è necessario impostare la proprietà del sistema di risoluzione di un singolo articolo. Se si desidera utilizzare un sistema di risoluzione dei conflitti di articolo anziché quello predefinito, è necessario configurare la proprietà di risoluzione per l'articolo che lo utilizzerà selezionando un sistema di risoluzione disponibile nel server di pubblicazione. Nelle proprietà delle informazioni del sistema di risoluzione è possibile specificare qualsiasi informazione specifica da trasmettere al sistema di risoluzione.  
  
 La replica di tipo merge prevede quattro tipi di sistemi di risoluzione dei conflitti:  
  
-   Il sistema di risoluzione dei conflitti predefinito basato sulla priorità  
  
     Il meccanismo di risoluzione predefinito segue una procedura diversa a seconda che la sottoscrizione sia di tipo client o server. È possibile assegnare valori di priorità ai singoli Sottoscrittori che utilizzano le sottoscrizioni server. In tal caso prevalgono le modifiche apportate al nodo con la priorità più alta. Nel caso delle sottoscrizioni client, la prima modifica scritta sul server di pubblicazione prevale nel conflitto.  
  
     Dopo la creazione di una sottoscrizione non è più possibile modificarne il tipo.  
  
-   Un gestore della logica di business  
  
     Il framework di gestione della logica di business consente di scrivere un assembly di codice gestito che viene chiamato durante il processo di sincronizzazione di tipo merge. L'assembly include la logica di business in grado di rispondere ai conflitti e altre condizioni durante la sincronizzazione. Per altre informazioni, vedere [Eseguire logiche di business durante la sincronizzazione di tipo merge](execute-business-logic-during-merge-synchronization.md).  
  
-   Un sistema di risoluzione personalizzato basato sul modello COM  
  
     La replica di tipo merge utilizza un'API per la creazione di sistemi di risoluzione come oggetti COM in linguaggi quali [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. Per altre informazioni, vedere [COM-Based Custom Resolvers](advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
-   Un sistema di risoluzione basato sul modello COM implementato da [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include un certo numero di sistemi di risoluzione basati sul modello COM. Per altre informazioni, vedere [Sistemi di risoluzione dei conflitti basati su Microsoft COM](advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 Per informazioni sulla scelta del tipo di sistema di risoluzione appropriato, vedere [Scegliere un sistema di risoluzione](advanced-merge-replication-conflict-choose-a-resolver.md).  
  
> [!NOTE]  
>  Alcuni sistemi di risoluzione dei conflitti di articolo sono progettati per gestire solo i conflitti di alcune operazioni. Ad esempio, un sistema di risoluzione può gestire gli aggiornamenti, ma non gli inserimenti o le eliminazioni. Il sistema di risoluzione dei conflitti predefinito basato sulla priorità gestisce qualsiasi conflitto non gestito dal sistema di risoluzione dei conflitti di articolo.  
  
 Per specificare una sottoscrizione di tipo merge e la priorità per la risoluzione dei conflitti, vedere  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Specificare una sottoscrizione di tipo Merge e la priorità per la risoluzione dei conflitti &#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   Replica [!INCLUDE[tsql](../../../includes/tsql-md.md)] programmazione e la programmazione oggetti RMO (Replication Management Objects): [Creare una sottoscrizione Pull](../create-a-pull-subscription.md) e [creare una sottoscrizione Push](../create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>Sistema di risoluzione interattivo  
 La replica prevede un'interfaccia utente del sistema di risoluzione interattivo che può essere utilizzata insieme al sistema di risoluzione dei conflitti predefinito basato sulla priorità o a un sistema di risoluzione dei conflitti di articolo. Quando si esegue la sincronizzazione su richiesta tramite Gestione sincronizzazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, il sistema di risoluzione interattivo visualizza i dati del conflitto in fase di esecuzione e consente di selezionare il modo in cui risolvere i conflitti. Per ulteriori informazioni sull'attivazione della risoluzione interattiva e sull'avvio del sistema di risoluzione interattivo, vedere [Interactive Conflict Resolution](advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="viewing-conflicts"></a>Visualizzazione dei conflitti  
 Il modo più diretto per visualizzare i conflitti consiste nell'utilizzare Visualizzatore conflitti di replica, disponibile in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (anche in[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono incluse stored procedure per l'esecuzione di query nelle tabelle dei conflitti). Il Visualizzatore conflitti e il sistema di risoluzione interattivo sono strumenti simili, ma il sistema di risoluzione interattivo consente di risolvere i conflitti al momento della sincronizzazione, mentre il Visualizzatore conflitti è concepito per visualizzare i conflitti dopo la risoluzione. Se i metadati del conflitto sono ancora disponibili nelle tabelle di sistema (vengono conservati per 14 giorni per impostazione predefinita), è possibile sovrascrivere i risultati della risoluzione del conflitto nel Visualizzatore conflitti. Tuttavia, se è richiesto un intervento diretto, è consigliabile utilizzare il sistema di risoluzione interattivo.  
  
> [!NOTE]  
>  I conflitti a livello di record logici non vengono visualizzati nel Visualizzatore conflitti. Per visualizzare informazioni relative a questi conflitti, utilizzare le stored procedure di replica. Per altre informazioni, vedere [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](../view-conflict-information-for-merge-publications.md).  
  
 Nel Visualizzatore conflitti sono visualizzate informazioni delle tre tabelle di sistema:  
  
-   La replica crea una tabella dei conflitti per ogni tabella dell'articolo di merge, denominata **MSmerge_conflict_\<NomePubblicazione>_\<NomeArticolo>**.  
  
     La struttura delle tabelle dei conflitti corrisponde a quella delle tabelle su cui sono basate. Una riga in una di queste tabelle rappresenta la versione non confermata di una riga in conflitto. La versione confermata della riga è inclusa nella tabella utente effettiva.  
  
-   Nella tabella **MSmerge_conflicts_info** sono contenute informazioni su ogni conflitto, incluso il tipo di conflitto.  
  
-   La tabella **sysmergearticles** identifica le tabelle utente che presentano conflitti e fornisce informazioni su tali tabelle.  
  
 Per impostazione predefinita, le informazioni sui conflitti vengono archiviate:  
  
-   Nel server di pubblicazione e nel Sottoscrittore se il livello di compatibilità della pubblicazione è pari a 90RTM o superiore.  
  
-   Nel server di pubblicazione se il livello di compatibilità della pubblicazione è inferiore a 80RTM.  
  
-   Nel server di pubblicazione se i Sottoscrittori eseguono [!INCLUDE[ssEW](../../../includes/ssew-md.md)]. I dati in conflitto non possono essere archiviati nei sottoscrittori di [!INCLUDE[ssEW](../../../includes/ssew-md.md)] .  
  
 **Per visualizzare i conflitti**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Visualizzare e risolvere i conflitti di dati per le pubblicazioni di tipo merge &#40;SQL Server Management Studio&#41;](../view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   Replica [!INCLUDE[tsql](../../../includes/tsql-md.md)] di programmazione: [Visualizzare le informazioni sui conflitti per le pubblicazioni di tipo merge &#40;programmazione Transact-SQL della replica&#41;](../view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Sincronizzare i dati](../synchronize-data.md)  
  
  
