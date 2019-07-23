---
title: Genera filtri | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 341c6325064031b99eeb5d7b58c00dda686097db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128096"
---
# <a name="generate-filters"></a>Genera filtri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo **Genera filtri** consente di definire un filtro di riga in una tabella in una pubblicazione di tipo merge. Durante la replica, il filtro viene esteso automaticamente alle altre tabelle correlate tramite relazioni di chiave esterna. Se ad esempio si definisce un filtro in una tabella clienti in modo che contenga solo dati su clienti francesi, la replica estenderà tale filtro affinché nelle tabelle degli ordini e dei dettagli ordine correlate vengano incluse solo informazioni relative ai clienti francesi.  
  
## <a name="options"></a>Opzioni  
 Questa finestra di dialogo prevede un processo in tre passaggi per la creazione di un filtro di riga in una tabella. Il filtro viene quindi esteso alle tabelle correlate a quella su cui viene applicato il filtro tramite relazioni di chiave esterna e primaria. Si supponga ad esempio di disporre delle tre tabelle **Cliente**, **IntestazioneOrdineVendita**e **DettagliOrdineVendita**, in cui **Cliente** è correlata a **IntestazioneOrdineVendita**e **IntestazioneOrdineVendita** è correlata a **DettagliOrdineVendita**. Se si applica un filtro di riga a **Cliente**, la replica estenderà tale filtro a **IntestazioneOrdineVendita** e a **DettagliOrdineVendita**.  
  
1.  **Selezionare la tabella da filtrare.**  
  
     Selezionare una tabella dall'elenco a discesa. Le tabelle verranno visualizzate nella casella di riepilogo solo se sono state selezionate nella pagina **Articoli** .  
  
2.  **Completare l'istruzione per il filtro per identificare le righe della tabella che verranno ricevute dai Sottoscrittori.**  
  
     Consente di definire una nuova istruzione per il filtro. Nella casella di riepilogo **Colonne** vengono elencate tutte le colonne in fase di pubblicazione appartenenti alla tabella selezionata in **Selezionare la tabella da filtrare**. L'area di testo **Istruzione per il filtro** contiene il testo predefinito, nel formato seguente:  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     Questo testo non può essere modificato. Digitare la clausola di filtro dopo la parola chiave WHERE utilizzando la sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] standard.  
  
    > [!IMPORTANT]  
    >  Per motivi relativi alle prestazioni, è consigliabile evitare di applicare funzioni ai nomi di colonna nelle clausole di filtro di riga con parametri, come `LEFT([MyColumn]) = SUSER_SNAME()`. Se si usano HOST_NAME in una clausola di filtro e si sostituisce il valore HOST_NAME, può essere necessario convertire i tipi di dati tramite l'istruzione CONVERT. Per altre informazioni sulle procedure consigliate in questo caso, vedere la sezione relativa alla sostituzione del valore HOST_NAME() nell'argomento [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Specificare se i dati di questa tabella dovranno essere inviati a una o più sottoscrizioni.**  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] and later versions only. Merge replication allows you to specify the type of partitions that are best suited to your data and application. If you select **A row from this table will go to only one subscription**, merge replication sets the nonoverlapping partitions option. Nonoverlapping partitions work in conjunction with precomputed partitions to improve performance, with nonoverlapping partitions minimizing the upload cost associated with precomputed partitions. The performance benefit of nonoverlapping partitions is more noticeable when the parameterized filters and join filters used are more complex. If you select this option, you must ensure that the data is partitioned in such a way that a row cannot be replicated to more than one Subscriber. For more information, see the section "Setting 'partition options'" in the topic [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Dopo aver aggiunto un filtro, fare clic su **OK** per chiudere la finestra di dialogo. Il filtro specificato viene analizzato ed eseguito sulla tabella nella clausola SELECT. Se nell'istruzione di filtro sono presenti errori di sintassi o di altro tipo, verrà visualizzato un apposito messaggio di notifica e sarà possibile modificare l'istruzione.  
  
 Al termine dell'analisi dell'istruzione, la replica creerà i filtri join necessari. Se non è stato ancora configurato il server di distribuzione per il server di pubblicazione su cui viene eseguita la procedura guidata, verrà chiesto di eseguire tale operazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà della pubblicazione](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtrare i dati pubblicati](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Pubblicare dati e oggetti di database](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
