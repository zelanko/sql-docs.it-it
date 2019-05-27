---
title: Controllo di identità e accesso (replica) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 8c43cd13760808822b2c0332584799383eab5e39
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64776264"
---
# <a name="identity-and-access-control-replication"></a>Controllo di identità e accesso (replica)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'autenticazione è il processo in base al quale un'entità (in genere un computer in questo contesto) verifica l'identità di un'altra entità, detta anche un *principale*, (in genere un altro computer o utente). L'autorizzazione è il processo che consente di concedere a un'entità autenticata l'accesso alle risorse, ad esempio un file nel file system o una tabella in un database.  
  
 La sicurezza della replica si basa sull'autenticazione e sull'autorizzazione per controllare l'accesso agli oggetti di database replicati e ai computer e agli agenti coinvolti nell'elaborazione della replica. Questo processo viene eseguito mediante tre meccanismi:  
  
-   Sicurezza degli agenti  
  
     Il modello di sicurezza degli agenti di replica garantisce un controllo dettagliato sugli account utilizzati per eseguire gli agenti e stabilire connessioni. Per informazioni dettagliate sul modello di sicurezza degli agenti, vedere [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). 
  
-   Ruoli di amministrazione  
  
     Verificare che vengano utilizzati i ruoli appropriati del server e del database per la configurazione, la manutenzione e l'elaborazione della replica. Per altre informazioni, vedere [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   Elenco di accesso alla pubblicazione  
  
     Concedere l'accesso alle pubblicazioni tramite l'elenco di accesso alla pubblicazione, che funziona in maniera analoga a un elenco di controllo di accesso [!INCLUDE[msCoName](../../../includes/msconame-md.md)] . Quando un Sottoscrittore si connette al server di pubblicazione o al server di distribuzione e richiede l'accesso a una pubblicazione, le informazioni di autenticazione passate dall'agente vengono controllate in base all'elenco di accesso alla pubblicazione. Per altre informazioni e procedure consigliate relative all'elenco di accesso alla pubblicazione, vedere [Proteggere il server di pubblicazione](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="filtering-published-data"></a>Applicazione di filtri ai dati pubblicati  
 Oltre a utilizzare l'autenticazione e l'autorizzazione per controllare l'accesso ai dati e agli oggetti replicati, la replica include due opzioni per controllare quali dati rendere disponibili nel Sottoscrittore: applicazione di filtri a colonne e a righe. Per altre informazioni sui filtri, vedere [Filtrare i dati pubblicati](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 Quando si definisce un articolo, è possibile pubblicare solo le colonne necessarie per la pubblicazione e omettere quelle superflue o che contengono dati riservati. Quando ad esempio si pubblica la tabella **Customer** dal database Adventure Works per gli agenti di vendita interessati, è possibile omettere la colonna **AnnualSales** che può essere rilevante solo per i dirigenti dell'azienda.  
  
 L'applicazione di filtri ai dati pubblicati consente di limitare l'accesso ai dati e di specificare i dati da rendere disponibili nel Sottoscrittore. È possibile, ad esempio, filtrare la tabella **Customer** in modo che i partner aziendali ricevano solo le informazioni relative ai clienti per cui nella colonna **ShareInfo** è impostato il valore "yes". Nella replica di tipo merge è necessario tenere in considerazione alcuni aspetti relativi alla sicurezza se si utilizza un filtro con parametri che include HOST_NAME(). Per ulteriori informazioni, vedere la sezione relativa all'utilizzo dei filtri con HOST_NAME() in [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  

## <a name="manage-logins-and-passwords-in-replication"></a>Gestione degli account di accesso e delle password nella replica
Specificare gli account di accesso e le password per gli agenti di replica durante la configurazione della replica. Dopo aver configurato la replica, è possibile modificare gli account di accesso e le password. Per altre informazioni, vedere [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md). Se si modifica la password per un account usato da un agente di replica, eseguire [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md).  

Il supporto per l'uso degli account del servizio gestito di gruppo (gMSA) è stato introdotto in SQL Server 2014. Per altre informazioni, vedere il blog [Replication and group Managed Service Accounts](https://repltalk.com/2019/03/26/replication-and-group-managed-service-accounts/) (Replica e account del servizio gestito di gruppo).
  
## <a name="see-also"></a>Vedere anche  
 [Attenuazione di minacce e vulnerabilità &#40;replica&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md) [Modello di sicurezza dell'agente di replica](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Procedure consigliate per la sicurezza della replica](../../../relational-databases/replication/security/replication-security-best-practices.md)   

  
  
