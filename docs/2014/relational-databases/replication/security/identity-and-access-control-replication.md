---
title: Controllo di identità e accesso (replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd51a3e4c139c52d6510140324ae042c653377b5
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289519"
---
# <a name="identity-and-access-control-replication"></a>Controllo di identità e accesso (replica)
  L'autenticazione è il processo in base al quale un'entità (in genere un computer in questo contesto) verifica l'identità di un'altra entità, detta anche un *principale*, (in genere un altro computer o utente). L'autorizzazione è il processo che consente di concedere a un'entità autenticata l'accesso alle risorse, ad esempio un file nel file system o una tabella in un database.  
  
 La sicurezza della replica si basa sull'autenticazione e sull'autorizzazione per controllare l'accesso agli oggetti di database replicati e ai computer e agli agenti coinvolti nell'elaborazione della replica. Questo processo viene eseguito mediante tre meccanismi:  
  
-   Sicurezza agente: il modello di sicurezza dell'agente di replica consente un controllo con granularità fine sugli account con cui gli agenti di replica eseguono ed eseguono le connessioni. Per informazioni dettagliate sul modello di sicurezza degli agenti, vedere [Replication Agent Security Model](replication-agent-security-model.md). Per informazioni sull'impostazione di account di accesso e password per gli agenti, vedere [Gestire gli account di accesso e le password nella replica](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication).  
  
-   Ruoli di amministrazione: assicurarsi che i ruoli del server e del database corretti vengano utilizzati per la configurazione, la manutenzione e l'elaborazione della replica. Per altre informazioni, vedere [Security Role Requirements for Replication](security-role-requirements-for-replication.md).  
  
-   Elenco di accesso alla pubblicazione: concedere l'accesso alle pubblicazioni tramite l'elenco di accesso alla pubblicazione. che funziona in maniera analoga a un elenco di controllo di accesso [!INCLUDE[msCoName](../../../includes/msconame-md.md)] . Quando un Sottoscrittore si connette al server di pubblicazione o al server di distribuzione e richiede l'accesso a una pubblicazione, le informazioni di autenticazione passate dall'agente vengono controllate in base all'elenco di accesso alla pubblicazione. Per altre informazioni e procedure consigliate relative all'elenco di accesso alla pubblicazione, vedere [Proteggere il server di pubblicazione](secure-the-publisher.md).  
  
## <a name="filtering-published-data"></a>Applicazione di filtri ai dati pubblicati  
 Oltre a utilizzare l'autenticazione e l'autorizzazione per controllare l'accesso ai dati e agli oggetti replicati, la replica include due opzioni per controllare quali dati rendere disponibili nel Sottoscrittore: applicazione di filtri a colonne e a righe. Per altre informazioni sui filtri, vedere [Filtrare i dati pubblicati](../publish/filter-published-data.md).  
  
 Quando si definisce un articolo, è possibile pubblicare solo le colonne necessarie per la pubblicazione e omettere quelle superflue o che contengono dati riservati. Quando ad esempio si pubblica la tabella **Customer** dal database Adventure Works per gli agenti di vendita interessati, è possibile omettere la colonna **AnnualSales** che può essere rilevante solo per i dirigenti dell'azienda.  
  
 L'applicazione di filtri ai dati pubblicati consente di limitare l'accesso ai dati e di specificare i dati da rendere disponibili nel Sottoscrittore. È possibile, ad esempio, filtrare la tabella **Customer** in modo che i partner aziendali ricevano solo le informazioni relative ai clienti per cui nella colonna **ShareInfo** è impostato il valore "yes". Nella replica di tipo merge è necessario tenere in considerazione alcuni aspetti relativi alla sicurezza se si utilizza un filtro con parametri che include HOST_NAME(). Per ulteriori informazioni, vedere la sezione relativa all'utilizzo dei filtri con HOST_NAME() in [Parameterized Row Filters](../merge/parameterized-filters-parameterized-row-filters.md).  

## <a name="manage-logins-and-passwords-in-replication"></a>Gestione degli account di accesso e delle password nella replica
  Specificare gli account di accesso e le password per gli agenti di replica durante la configurazione della replica. Dopo aver configurato la replica, è possibile modificare gli account di accesso e le password. Per altre informazioni, vedere [View and Modify Replication Security Settings](view-and-modify-replication-security-settings.md). Se si modifica la password per un account usato da un agente di replica, eseguire [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Modello di sicurezza dell'agente di replica](replication-agent-security-model.md)   
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Sicurezza replica di SQL Server](view-and-modify-replication-security-settings.md)   
 [Attenuazione di minacce e vulnerabilità della replica](threat-and-vulnerability-mitigation-replication.md)   

  
  
