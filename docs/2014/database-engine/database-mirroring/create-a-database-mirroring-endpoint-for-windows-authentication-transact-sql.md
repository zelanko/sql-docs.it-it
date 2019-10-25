---
title: Creare un endpoint del mirroring del database per l'autenticazione Windows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], database mirroring
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: baf1a4b1-6790-4275-b261-490bca33bdb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43bb7fdd5b9c8cf8a73c423ac21e8ba7f779ec79
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797933"
---
# <a name="create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql"></a>Creare un endpoint del mirroring del database per l'autenticazione Windows (Transact-SQL)
  In questo argomento si illustra come creare un endpoint del mirroring del database in cui si utilizza l'autenticazione di Windows in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per supportare il mirroring del database o [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] , per ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è necessario un endpoint del mirroring del database. In un'istanza del server può essere incluso uno solo di questo tipo di endpoint, che a sua volta dispone di una sola porta. Un endpoint del mirroring del database può utilizzare qualsiasi porta disponibile nel sistema locale al momento della creazione dell'endpoint. Tutte le sessioni di mirroring del database in un'istanza del server sono in attesa su quella porta, che viene utilizzata anche per tutte le connessioni in ingresso per il mirroring del database.  
  
> [!IMPORTANT]  
>  Se un endpoint del mirroring del database è presente e già in uso, è consigliabile utilizzare quello. L'eliminazione di un endpoint in uso determina la chiusura delle sessioni esistenti.  
  
 **Contenuto dell'articolo**  
  
-   **Before you begin:**  [Security](#Security)  
  
-   **Per creare un endpoint del mirroring del database usando** [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Security  
 I metodi di autenticazione e crittografia dell'istanza del server sono stabiliti dall'amministratore di sistema.  
  
> [!IMPORTANT]  
>  L'algoritmo RC4 è deprecato. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] È consigliabile utilizzare AES.  
  
####  <a name="Permissions"></a> Permissions  
 È richiesta l'autorizzazione CREATE ENDPOINT o l'appartenenza al ruolo predefinito del server sysadmin. Per altre informazioni, vedere [GRANT Endpoint Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql).  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-create-a-database-mirroring-endpoint-that-uses-windows-authentication"></a>Per creare un endpoint del mirroring del database in cui viene utilizzata l'autenticazione di Windows  
  
1.  Connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si desidera creare un endpoint del mirroring del database.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Per determinare se esiste già un endpoint del mirroring del database, utilizzare l'istruzione seguente:  
  
    ```sql
    SELECT name, role_desc, state_desc FROM sys.database_mirroring_endpoints;
    ```  
  
    > [!IMPORTANT]  
    >  Se per l'istanza del server esiste già un endpoint del mirroring, utilizzarlo per tutte le altre sessioni stabilite nell'istanza del server.  
  
4.  Per creare un endpoint utilizzabile con l'autenticazione di Windows, eseguire un'istruzione Transact-SQL CREATE ENDPOINT, Il formato generale dell'istruzione è il seguente:  
  
     CREATE ENDPOINT *\<endpointName>*  
  
     STATE=STARTED  
  
     AS TCP ( LISTENER_PORT = *\<listenerPortList>* )  
  
     FOR DATABASE_MIRRORING  
  
     (  
  
     [ AUTHENTICATION = **WINDOWS** [ *\<authorizationMethod>* ]  
  
     ]  
  
     [ [ **,** ] ENCRYPTION = **REQUIRED**  
  
     [ ALGORITHM { *\<algorithm>* } ]  
  
     ]  
  
     [ **,** ] ROLE = *\<role>*  
  
     )  
  
     dove  
  
    -   *\<endpointName>* è un nome univoco per l'endpoint del mirroring del database dell'istanza del server.  
  
    -   STARTED indica che l'endpoint deve essere avviato e deve rimanere in attesa delle connessioni. Lo stato di un endpoint del mirroring del database creato è in genere STARTED. In alternativa, è possibile avviare una sessione nello stato STOPPED (impostazione predefinita) o DISABLED.  
  
    -   *\<listenerPortList>* è un solo numero di porta (*nnnn*) su cui il server deve attendere i messaggi di mirroring del database. È consentito solo il protocollo TCP. Tutti gli altri protocolli restituiranno un errore.  
  
         È possibile utilizzare un numero di porta una sola volta per ciascun computer. Un endpoint del mirroring del database può utilizzare qualsiasi porta disponibile nel sistema locale al momento della creazione dell'endpoint. Per identificare le porte attualmente utilizzate dagli endpoint TCP nel sistema, utilizzare l'istruzione Transact-SQL seguente:  
  
        ```  
        SELECT name, port FROM sys.tcp_endpoints;  
        ```  
  
        > [!IMPORTANT]  
        >  In ogni istanza del server è necessaria un'unica porta di attesa univoca.  
  
    -   Per l'autenticazione di Windows, l'opzione AUTHENTICATION è facoltativa, a meno che non si desideri che l'endpoint utilizzi solo NTLM o Kerberos per autenticare connessioni. *\<authorizationMethod>* specifica il metodo usato per autenticare le connessioni come NTLM, KERBEROS o NEGOTIATE. Con il metodo predefinito NEGOTIATE l'endpoint utilizzerà il protocollo di negoziazione di Windows per scegliere tra NTLM e Kerberos. La negoziazione consente di utilizzare le connessioni con o senza autenticazione, a seconda del livello di autenticazione dell'endpoint opposto.  
  
    -   Per impostazione predefinita, ENCRYPTION è impostato su REQUIRED, pertanto verrà utilizzata la crittografia per tutte le connessioni a questo endpoint. È tuttavia possibile disabilitare la crittografia o renderla facoltativa in un endpoint. Sono disponibili le alternative seguenti:  
  
        |valore|Definizione|  
        |-----------|----------------|  
        |DISABLED|Specifica che i dati inviati tramite una connessione non vengano crittografati.|  
        |SUPPORTED|Specifica che i dati vengano crittografati solo se per l'endpoint opposto è stato specificato SUPPORTED o REQUIRED.|  
        |REQUIRED|Specifica che i dati inviati tramite una connessione devono essere crittografati.|  
  
         Se è necessaria la crittografia per un endpoint, ENCRYPTION deve essere impostato su SUPPORTED o REQUIRED nell'altro endpoint.  
  
    -   *\<algorithm>* consente di specificare gli standard di crittografia per l'endpoint. Il valore di *\<algorithm>* può essere uno degli algoritmi o delle combinazioni di algoritmi seguenti: RC4, AES, AES RC4 o RC4 AES.  
  
         AES RC4 indica che questo endpoint negozierà l'algoritmo di crittografia, dando la preferenza a quello AES. RC4 AES indica che questo endpoint negozierà l'algoritmo di crittografia, dando la preferenza all'algoritmo RC4. Se i due endpoint specificano entrambi gli algoritmi, ma con un ordine diverso, l'algoritmo verrà definito dall'endpoint che accetta la connessione.  
  
        > [!NOTE]  
        >  L'algoritmo RC4 è deprecato. [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] È consigliabile utilizzare AES.  
  
    -   *\<role>* definisce il ruolo o i ruoli che il server può eseguire. Il valore di ROLE deve essere specificato. Tuttavia, il ruolo dell'endpoint è rilevante solo per il mirroring del database. Per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], viene ignorato il ruolo dell'endpoint.  
  
         Per consentire a un'istanza del server di utilizzare un ruolo per una sessione di mirroring del database e un altro ruolo per un'altra sessione, specificare ROLE=ALL. Per limitare un'istanza del server in modo che funga da partner o da server di controllo del mirroring, specificare rispettivamente ROLE=PARTNER o ROLE=WITNESS.  
  
        > [!NOTE]  
        >  Per ulteriori informazioni sulle opzioni di mirroring del database per le diverse edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
     Per una descrizione completa della sintassi di CREATE ENDPOINT, vedere [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql).  
  
    > [!NOTE]  
    >  Per modificare un endpoint esistente, usare [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql).  
  
###  <a name="TsqlExample"></a> Esempio: Creazione di endpoint per supportare il mirroring del database (Transact-SQL)  
 Nell'esempio seguente si creano endpoint del mirroring del database per le istanze del server predefinite in tre sistemi di computer distinti:  
  
|Ruolo dell'istanza del server|Nome del computer host|  
|-----------------------------|---------------------------|  
|Partner (inizialmente nel ruolo principale)|`SQLHOST01\.`|  
|Partner (inizialmente nel ruolo mirror)|`SQLHOST02\.`|  
|Controllo|`SQLHOST03\.`|  
  
 Nell'esempio tutti e tre gli endpoint utilizzano la porta numero 7022, anche se qualunque numero di porta disponibile sarebbe utilizzabile. L'opzione AUTHENTICATION non è necessaria, in quanto gli endpoint utilizzano il tipo predefinito, autenticazione di Windows. L'opzione ENCRYPTION è anch'essa superflua, in quanto gli endpoint sono tutti progettati per negoziare il metodo di autenticazione per una connessione, che rappresenta il comportamento predefinito per autenticazione di Windows. Inoltre, tutti gli endpoint richiedono la crittografia, che rappresenta il comportamento predefinito.  
  
 Ogni istanza del server è limitata a fungere da partner o da server di controllo e l'endpoint di ogni server specifica espressamente il ruolo (ROLE=PARTNER o ROLE=WITNESS).  
  
> [!IMPORTANT]  
>  Ogni istanza del server può includere un solo endpoint. Pertanto, se si desidera che un'istanza del server sia partner in alcune sessioni e server di controllo in altre, specificare ROLE=ALL.  
  
```sql
--Endpoint for initial principal server instance, which  
--is the only server instance running on SQLHOST01.  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (ROLE=PARTNER);  
GO  
--Endpoint for initial mirror server instance, which  
--is the only server instance running on SQLHOST02.  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (ROLE=PARTNER);  
GO  
--Endpoint for witness server instance, which  
--is the only server instance running on SQLHOST03.  
CREATE ENDPOINT endpoint_mirroring  
    STATE = STARTED  
    AS TCP ( LISTENER_PORT = 7022 )  
    FOR DATABASE_MIRRORING (ROLE=WITNESS);  
GO  
```  
  
##  <a name="RelatedTasks"></a> Attività correlate  

### <a name="to-configure-a-database-mirroring-endpoint"></a>Per configurare un endpoint del mirroring del database
  
-   [Creazione di un endpoint del mirroring del &#40;Database per gruppi di disponibilità AlwaysOn SQL Server PowerShell&#41;](../availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [Impostare l'endpoint del mirroring del database per l'uso di certificati per le connessioni in uscita &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [Impostazione dell'endpoint del mirroring del database per l'utilizzo di certificati per le connessioni in ingresso &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Specificare un indirizzo di rete del server &#40;mirroring del database&#41;](specify-a-server-network-address-database-mirroring.md)  
  
-   [Specifica dell'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](../availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Per visualizzare informazioni sull'endpoint del mirroring del database**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-endpoint-transact-sql)   
 [Scelta di un algoritmo di crittografia](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [Specificare un indirizzo di rete del server &#40;Mirroring del database&#41;](specify-a-server-network-address-database-mirroring.md)   
 [Esempio: Impostazione del mirroring del database tramite l'autenticazione di Windows &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-windows-authentication-transact-sql.md)   
 [Endpoint del mirroring del database &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)  
