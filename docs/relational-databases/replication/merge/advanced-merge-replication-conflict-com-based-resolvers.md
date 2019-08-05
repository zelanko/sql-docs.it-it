---
title: Sistemi di risoluzione basati su COM | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: a6637e4b-4e6b-40aa-bee6-39d98cc507c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ec508dbaf274816ecf32f8eaa0a8047baa60e2a8
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "68033391"
---
# <a name="advanced-merge-replication-conflict---com-based-resolvers"></a>Conflitti nella replica di tipo merge avanzata - Sistemi di risoluzione basati su COM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Tutti i sistemi di risoluzione basati su COM inclusi in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gestiscono i conflitti di aggiornamento e, se specificato, i conflitti di inserimento ed eliminazione. Tutti i sistemi gestiscono il rilevamento a livello di colonna e la maggior parte di essi gestisce anche il rilevamento a livello di riga. Questi e tutti gli altri sistemi di risoluzione dei conflitti basati su COM dichiarano i tipi di conflitto che possono gestire. Per tutti gli altri tipi di conflitti l'agente di merge utilizza il sistema di risoluzione dei conflitti predefinito.  
  
 I sistemi di risoluzione dei conflitti vengono installati durante il processo di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Eseguire la stored procedure **sp_enumcustomresolvers** per visualizzare tutti i sistemi di risoluzione dei conflitti registrati in un computer. Questa operazione consente di visualizzare la descrizione e l'identificatore univoco globale (GUID) per ogni sistema di risoluzione dei conflitti in un set di risultati distinto.  
  
 Per specificare un sistema di risoluzione dei conflitti, vedere [Specify a Merge Article Resolver](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md).  
  
 Nella tabella seguente vengono descritti gli attributi dei sistemi di risoluzione dei conflitti specifici.  
  
|nome|Input richiesto|Descrizione|Commenti|  
|----------|--------------------|-----------------|--------------|  
|Sistema di risoluzione dei conflitti aggiuntivi[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna da sommare. Il tipo di dati deve essere aritmetico, ad esempio **int**, **smallint**, **numeric**e così via.|La riga in conflitto confermata viene determinata in base al valore di priorità. I valori della colonna specificati sono impostati sulla somma dei valori delle colonne di origine e di destinazione. Se un valore è impostato su NULL, i valori della colonna verranno impostati sul valore dell'altra colonna.|Supporta conflitti di aggiornamento con rilevamento solo a livello di colonna.|  
|Sistema di risoluzione dei conflitti medi[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna di cui eseguire la media. Il tipo di dati deve essere aritmetico, ad esempio **int**, **smallint**, **numeric**e così via.|La riga in conflitto confermata viene determinata in base al valore di priorità. I valori della colonna risultanti sono impostati sulla media dei valori delle colonne di origine e di destinazione. Se un valore è impostato su NULL, i valori della colonna verranno impostati sul valore dell'altra colonna.|Supporta conflitti di aggiornamento con rilevamento solo a livello di colonna.|  
|Sistema di risoluzione dei conflitti DATETIME (prevale il meno recente)[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna da utilizzare per determinare la riga in conflitto confermata. Il tipo di dati deve essere **datetime** .|La colonna con il valore **datetime** meno recente determina la riga in conflitto confermata. Se il valore di una colonna è impostato su NULL, prevale la riga contenente l'altro valore.|Supporta conflitti di aggiornamento con rilevamento a livello di riga e di colonna. I valori delle colonne vengono confrontati direttamente e non vengono eseguite regolazioni in base a fusi orari diversi.|  
|Sistema di risoluzione dei conflitti DATETIME (prevale il più recente)[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna da utilizzare per determinare la riga in conflitto confermata. Il tipo di dati deve essere **datetime** .|La colonna con il valore **datetime** più recente determina la riga in conflitto confermata. Se il valore di una colonna è impostato su NULL, prevale la riga contenente l'altro valore.|Supporta conflitti di aggiornamento con rilevamento a livello di riga e di colonna.|  
|Sistema di risoluzione dei conflitti massimi[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna da utilizzare per determinare la riga in conflitto confermata. Il tipo di dati deve essere aritmetico, ad esempio **int**, **smallint**, **numeric**e così via.|La colonna con il valore numerico maggiore determina la riga in conflitto confermata. Se il valore di una colonna è impostato su NULL, prevale la riga contenente l'altro valore.|Supporta il rilevamento a livello di riga e di colonna.|  
|Sistema di risoluzione dei conflitti minimi[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna da utilizzare per determinare la riga in conflitto confermata. Il tipo di dati deve essere aritmetico, ad esempio **int**, **smallint**, **numeric**e così via.|La colonna con il valore numerico minore determina la riga in conflitto confermata. Se il valore di una colonna è impostato su NULL, prevale la riga contenente l'altro valore.|Supporta conflitti di aggiornamento con rilevamento a livello di riga e di colonna.|  
|Sistema di risoluzione dei conflitti merge colonne di testo[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome del delimitatore e della colonna di testo, ad esempio `@resolver_info = '[col1][===]'`.|La riga in conflitto confermata viene determinata in base al valore di priorità. Le colonne di testo in conflitto sono impostate su valori uniti, rappresentati da un prefisso comune seguito da una parte univoca del server di pubblicazione, quindi dal delimitatore e infine dalla parte univoca del Sottoscrittore.|Supporta conflitti di aggiornamento con rilevamento solo a livello di colonna.|  
|Sistema di risoluzione dei conflitti prevale sempre il Sottoscrittore[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Non è richiesto alcun input.|Prevale il Sottoscrittore, indipendentemente dal fatto che sia l'origine o la destinazione.|Supporta tutti i tipi di conflitto.|  
|Sistema di risoluzione colonna priorità[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Nome della colonna da utilizzare per determinare la riga in conflitto confermata. Il tipo di dati deve essere aritmetico, ad esempio **int**, **smallint**, **numeric**e così via.|La colonna con il valore numerico maggiore determina la riga in conflitto confermata. Se il valore di una colonna è impostato su NULL, prevale la riga contenente l'altro valore.|Supporta conflitti di aggiornamento con rilevamento a livello di riga e di colonna.|  
|Sistema di risoluzione dei conflitti solo caricamento[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Non è richiesto alcun input.|Le modifiche caricate nel server di pubblicazione vengono accettate. Le modifiche non vengono scaricate nel Sottoscrittore.|Supporta tutti i tipi di conflitto.|  
|Sistema di risoluzione dei conflitti solo download[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Non è richiesto alcun input.|Le modifiche caricate nel server di pubblicazione vengono rifiutate. Le modifiche vengono scaricate nel Sottoscrittore.|Supporta tutti i tipi di conflitto.|  
|Sistema di risoluzione delle stored procedure di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLServer|Nome della stored procedure che il sistema di risoluzione dei conflitti deve chiamare per gestire il conflitto.|La risoluzione del conflitto dipende dalla logica nella stored procedure specificata.|Supporta i conflitti di aggiornamento. Per altre informazioni, vedere [Implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di tipo merge](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [sp_enumcustomresolvers &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)  
  
  
