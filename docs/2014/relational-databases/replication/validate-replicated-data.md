---
title: Convalidare i dati replicati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- inline data validation [SQL Server replication]
- administering replication, validating data
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication]
- merge replication data validation [SQL Server replication], about data validation
- validating replicated data
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84ffe2ad4be91f8a05e4bbbd84b2ad5a67cb09a4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792493"
---
# <a name="validate-replicated-data"></a>Convalida dei dati replicati
  La replica transazionale e la replica di tipo merge consentono di verificare che i dati presenti nel Sottoscrittore corrispondano ai dati nel server di pubblicazione. La convalida può essere eseguita per sottoscrizioni specifiche o per tutte le sottoscrizioni di una pubblicazione. Specificare uno dei tipi seguenti di convalida dei dati, che verrà eseguita dall'agente di distribuzione o dall'agente di merge alla successiva sincronizzazione:  
  
-   Conteggio delle sole righe. Questo tipo di convalida verifica se la tabella nel Sottoscrittore ha lo stesso numero di righe della tabella nel server di pubblicazione, ma non verifica che il contenuto delle righe corrisponda. La convalida del conteggio delle righe è un controllo non approfondito che consente comunque di evidenziare eventuali problemi dei dati.  
  
-   Conteggio delle righe e checksum binario. Oltre al conteggio delle righe nel server di pubblicazione e nel Sottoscrittore, viene calcolato il checksum di tutti i dati tramite lo specifico algoritmo di checksum. In caso di esito negativo durante il conteggio delle righe il checksum non viene eseguito.  
  
 Oltre a verificare che i dati nel Sottoscrittore corrispondano ai dati nel server di pubblicazione, la replica di tipo merge consente di verificare che i dati vengano partizionati correttamente per ogni Sottoscrittore. Per altre informazioni, vedere [Convalidare le informazioni sulle partizioni per un Sottoscrittore di tipo merge](validate-partition-information-for-a-merge-subscriber.md).  
  
 **Per convalidare i dati**  
  
 Per convalidare tutti gli articoli di una sottoscrizione, utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], stored procedure o Replication Management Objects (RMO). Per altre informazioni, vedere [Validate Data at the Subscriber](validate-data-at-the-subscriber.md). Per convalidare singoli articoli di pubblicazioni snapshot e transazionali, è necessario utilizzare stored procedure.  
  
## <a name="data-validation-results"></a>Risultati della convalida dei dati  
 Al termine della convalida nell'agente di distribuzione o nell'agente di merge vengono registrati messaggi relativi all'esito positivo o negativo dell'operazione. Non vengono specificate le righe con esito negativo. È possibile visualizzare tali messaggi in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Monitoraggio replica e nelle tabelle di sistema di replica. Nell'argomento elencato sopra vengono illustrate le procedure di esecuzione della convalida e di visualizzazione dei risultati.  
  
 Per gestire gli errori di convalida, considerare quanto segue:  
  
-   Configurare l'avviso di replica **replica: Sottoscrittore non supera la convalida dei dati** in modo da ricevere una notifica dell'errore. Per altre informazioni, vedere [configurare gli avvisi di replica predefiniti &#40;& 41(administration/configure-predefined-replication-alerts-sql-server-management-studio.md) & SQL Server Management Studio.  
  
-   L'errore di convalida rappresenta un problema per l'applicazione utilizzata? Se sì, aggiornare manualmente i dati in modo che siano sincronizzati oppure reinizializzare la sottoscrizione:  
  
    -   È possibile aggiornare i dati tramite l' [utilità tablediff](../../tools/tablediff-utility.md). Per ulteriori informazioni sull'uso di questa utilità, vedere [Confrontare tabelle replicate al fine di individuare le differenze &#40;programmazione della replica&#41;](administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
    -   Per altre informazioni sulla reinizializzazione, vedere [Reinizializzare le sottoscrizioni](reinitialize-subscriptions.md).  
  
## <a name="considerations-for-data-validation"></a>Considerazioni sulla convalida dei dati  
 Durante la convalida dei dati è opportuno considerare gli aspetti seguenti:  
  
-   Prima di eseguire la convalida dei dati è necessario arrestare tutte le attività di aggiornamento nei Sottoscrittori. Non è necessario arrestare l'eventuale aggiornamento nel server di pubblicazione durante la convalida.  
  
-   Poiché la convalida di set di dati estesi mediante checksum e checksum binari può richiedere quantità elevate di risorse di elaborazione, è opportuno pianificare la convalida in modo che venga eseguita nei periodi di attività minore nei server utilizzati per la replica.  
  
-   La replica convalida soltanto le tabelle e non verifica che gli articoli solo schema, ad esempio le stored procedure, presenti nel server di pubblicazione e nel Sottoscrittore corrispondano.  
  
-   Il checksum binario può essere utilizzato per qualsiasi tabella pubblicata. Non è possibile convalidare mediante il calcolo del checksum tabelle con filtri colonne o strutture di tabelle logiche con offset di colonna diversi, a causa di istruzioni di tipo ALTER TABLE tramite cui vengono eliminate o aggiunte colonne.  
  
-   Convalida della replica utilizza il `checksum` e **binary_checksum** funzioni. Per informazioni sul comportamento, vedere [CHECKSUM &#40;Transact-SQL&#41;](/sql/t-sql/functions/checksum-transact-sql) e [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](/sql/t-sql/functions/binary-checksum-transact-sql).  
  
-   La convalida eseguita mediante checksum o checksum binario può segnalare erroneamente un problema se nel Sottoscrittore vi sono tipi di dati diversi rispetto al server di pubblicazione. Ciò può verificarsi se si effettua una delle operazioni indicate di seguito.  
  
    -   Impostazione esplicita delle opzioni per lo schema per l'esecuzione del mapping dei tipi di dati per versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Impostazione del livello di compatibilità della pubblicazione per una pubblicazione di tipo merge su una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], qualora le tabelle pubblicate contengano uno o più tipi di dati di cui è necessario eseguire il mapping per questa versione.  
  
    -   Inizializzazione manuale di una sottoscrizione, in caso di utilizzo di tipi di dati diversi nel Sottoscrittore.  
  
-   Le convalide mediante calcoli del checksum e checksum binario non sono supportate per la replica transazionale di sottoscrizioni trasformabili.  
  
-   La convalida non è supportata per i dati replicati in Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-data-validation-works"></a>Funzionamento della convalida dei dati  
 In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i dati vengono convalidati tramite il conteggio delle righe o il calcolo del checksum nel server di pubblicazione e nel Sottoscrittore e il successivo confronto dei risultati. Viene calcolato un solo valore per l'intera tabella di pubblicazione e un solo valore per l'intera tabella di sottoscrizione. I dati delle colonne di tipo `text`, `ntext` o `image` non vengono inclusi nei calcoli.  
  
 Durante l'esecuzione del calcolo vengono attivati temporaneamente i blocchi condivisi sulle tabelle per le quali viene eseguito il conteggio delle righe o il calcolo del checksum. Il calcolo viene comunque completato e i blocchi condivisi vengono subito rimossi.  
  
 Quando si utilizzano valori checksum binari, il controllo di ridondanza ciclico (CRC) a 32 bit viene eseguito su ogni colonna anziché sulla riga fisica di una pagina di dati. Le colonne possono essere pertanto ordinate fisicamente in qualsiasi modo nella pagina di dati e al medesimo tempo ottenere lo stesso CRC per la riga. La convalida mediante checksum binario può essere utilizzata quando alla pubblicazione sono applicati filtri di riga o di colonna.  
  
## <a name="see-also"></a>Vedere anche  
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)  
  
  
