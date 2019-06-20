---
title: MSSQL_ENG014114 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51b62a64ae008e0994054d40344d1e0d68bb296b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191680"
---
# <a name="mssqleng014114"></a>MSSQL_ENG014114
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|14114|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|'%s' non è configurato come server di distribuzione.|  
  
## <a name="explanation"></a>Spiegazione  
 Se nel messaggio di errore viene specificata una particolare istanza, diversa da 'null', l'istanza specificata non è stata configurata correttamente per essere riconosciuta come server di distribuzione.  
  
 Se nel messaggio viene specificato 'null' come server di distribuzione, non è presente alcuna voce del server locale nel database **master** oppure la voce non è corretta (probabilmente il computer è stato rinominato). La replica prevede che tutti i server di una topologia vengano registrati utilizzando il nome del computer con il nome di un'istanza opzionale (nel caso di un'istanza cluster il nome del server virtuale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con il nome dell'istanza opzionale). Per un corretto funzionamento della replica il valore restituito da `SELECT @@SERVERNAME` per ogni server nella topologia deve far corrispondere al nome dell'istanza opzionale il nome del computer o il nome del server virtuale.  
  
 Non sarà possibile eseguire la replica, se una qualsiasi delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene registrata utilizzando l'indirizzo IP o il nome di dominio completo (FQDN, Fully Qualified Domain Name). Se durante la configurazione della replica una delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stata registrata utilizzando l'indirizzo IP o il nome di dominio completo in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , è possibile che venga generato questo errore.  
  
## <a name="user-action"></a>Azione dell'utente  
 Se nel messaggio di errore viene specificata una particolare istanza, configurare il server come server di distribuzione. Per altre informazioni, vedere [Configurazione della distribuzione](configure-distribution.md).  
  
 Se nel messaggio non viene specificata una particolare istanza ('null'), verificare che l'istanza del server di distribuzione sia registrata correttamente. Se il nome di rete del computer e il nome dell'istanza di SQL Server sono diversi, procedere in uno dei modi seguenti:  
  
-   Aggiungere il nome dell'istanza di SQL Server come nome di rete valido. Uno dei metodi disponibili per impostare un nome di rete alternativo consiste nell'aggiungerlo al file hosts locale. Il file hosts locale è disponibile per impostazione predefinita nella cartella WINDOWS\system32\drivers\etc o WINNT\system32\drivers\etc. Per ulteriori informazioni, vedere la documentazione di Windows.  
  
     Ad esempio, se il nome del computer è comp1, l'indirizzo IP del computer è 10.193.17.129 e il nome dell'istanza è inst1/instname, aggiungere la voce seguente al file hosts:  
  
     10.193.17.129 inst1  
  
-   Disabilitare la distribuzione, registrare l'istanza e quindi riattivare la distribuzione. Se il valore di @@SERVERNAME non è corretto per un'istanza non cluster, eseguire la procedura seguente:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Dopo l'esecuzione della stored procedure [sp_addserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per rendere effettiva la modifica apportata a @@SERVERNAME.  
  
     Se il valore di @@SERVERNAME non è corretto per un'istanza cluster, è necessario modificare il nome tramite Amministrazione cluster. Per altre informazioni, vedere [Istanze del cluster di failover Always On (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
