---
title: Convalidare le informazioni sulle partizioni per un Sottoscrittore di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication data validation [SQL Server replication], partitions
- parameterized filters [SQL Server replication], validating partition information
- validating partition information
ms.assetid: c059553e-df2c-4333-ba79-e8d6e2890c34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a95d55aa0d2722719f799af9f69f6a3b3c14689
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52805853"
---
# <a name="validate-partition-information-for-a-merge-subscriber"></a>Convalida delle informazioni sulle partizioni per un Sottoscrittore di tipo merge
  Quando si definisce un filtro di riga con parametri per una pubblicazione di tipo merge, si utilizza una funzione che fa riferimento a informazioni sul Sottoscrittore, ad esempio il nome di accesso del Sottoscrittore. Per impostazione predefinita, le informazioni sul Sottoscrittore vengono convalidate dalla replica in base a tale funzione prima di ogni sincronizzazione e ogni volta che uno snapshot viene applicato al Sottoscrittore. Il processo di convalida garantisce il partizionamento corretto dei dati per ogni Sottoscrittore. Il comportamento di convalida è controllato dalla proprietà di pubblicazione **validate_subscriber_info**, che può essere modificata mediante [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) oppure nella pagina **Opzioni sottoscrizione** della finestra di dialogo **Proprietà pubblicazione**. Per ulteriori informazioni sulla modifica delle proprietà di pubblicazione, vedere [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
## <a name="how-partition-validation-works"></a>Funzionamento della convalida delle partizioni  
 Quando una pubblicazione viene filtrata, ad esempio mediante la funzione **SUSER_SNAME()**, l'agente di merge applica lo snapshot iniziale a ogni Sottoscrittore in base ai dati validi per l'espressione **SUSER_SNAME()** .  
  
 Se la convalida è abilitata, quando il Sottoscrittore si riconnette al server di pubblicazione per la successiva sincronizzazione, l'agente di merge convalida le informazioni nel Sottoscrittore e garantisce che la partizione di ogni Sottoscrittore corrisponda a quella ricevuta nello snapshot iniziale. Per ogni successiva applicazione di snapshot o merge, l'agente di merge convalida la partizione di ogni Sottoscrittore.  
  
 Se l'agente di merge rileva che la funzione utilizzata nell'espressione di filtro restituisce un valore diverso rispetto allo snapshot iniziale, l'applicazione di snapshot o merge ha esito negativo e potrebbe essere necessaria la reinizializzazione della sottoscrizione del Sottoscrittore. La reinizializzazione può risultare necessaria per evitare i problemi che possono verificarsi in caso di modifica delle impostazioni di merge di un Sottoscrittore. Può tuttavia rivelarsi sufficiente modificare le informazioni nel Sottoscrittore, ad esempio il nome di accesso, ripristinando il valore utilizzato al momento dello snapshot originale.  
  
 Quando l'agente di merge convalida una partizione, oltre a convalidare la partizione rispetto ai valori restituiti dalle funzioni utilizzate nelle espressioni di filtro, controlla se lo snapshot è stato generato prima di modifiche che ne compromettono la validità, come operazioni di pulizia dei metadati o modifiche dello schema. Se uno snapshot partizionato è obsoleto, l'agente di merge restituirà un errore e sarà necessario rigenerare uno snapshot partizionato per il Sottoscrittore in base a uno snapshot regolare corrente.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione &#40;Replica&#41;](administration/administration-replication.md)   
 [Procedure consigliate per l'amministrazione della replica](administration/best-practices-for-replication-administration.md)   
 [Reinizializzare le sottoscrizioni](reinitialize-subscriptions.md)   
 [Convalidare i dati replicati](validate-replicated-data.md)  
  
  
