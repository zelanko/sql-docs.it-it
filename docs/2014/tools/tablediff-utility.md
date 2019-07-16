---
title: Utilità tablediff | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- comparing data
- tablediff utility
- tables [SQL Server replication]
- table comparisons [SQL Server]
- command prompt utilities [SQL Server], tablediff
- troubleshooting [SQL Server replication], non-convergence
- non-convergence [SQL Server]
ms.assetid: 3c3cb865-7a4d-4d66-98f2-5935e28929fc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb8b8bec38b428ca7b2eea5166867141b34a2405
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68185966"
---
# <a name="tablediff-utility"></a>utilità tablediff
  L'utilità **tablediff** viene usata per confrontare i dati in due tabelle per rilevarne l'eventuale non convergenza e risulta particolarmente utile per la risoluzione dei problemi relativi alla non convergenza in una topologia di replica. Questa utilità può essere utilizzata dal prompt dei comandi oppure in un file batch per eseguire le attività seguenti:  
  
-   Confronto riga per riga tra una tabella di origine in un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che funge da server di pubblicazione per la replica e una tabella di destinazione in una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che fungono da Sottoscrittori della replica.  
  
-   Esegue un confronto rapido mediante il confronto solo dei conteggi delle righe e degli schemi.  
  
-   Confronti a livello di colonna.  
  
-   Generazione di uno script [!INCLUDE[tsql](../includes/tsql-md.md)] per correggere le discrepanze nel server di destinazione e rendere convergenti le tabelle di origine e di destinazione.  
  
-   Registrazione dei risultati in un file di output oppure in una tabella nel database di destinazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      tablediff   
[ -? ] |   
{  
        -sourceserversource_server_name[\instance_name]  
        -sourcedatabasesource_database-sourcetablesource_table_name   
    [ -sourceschemasource_schema_name ]  
    [ -sourcepasswordsource_password ]  
    [ -sourceusersource_login ]  
    [ -sourcelocked ]  
        -destinationserverdestination_server_name[\instance_name]  
        -destinationdatabasesubscription_database-destinationtabledestination_table   
    [ -destinationschemadestination_schema_name ]  
    [ -destinationpassworddestination_password ]  
    [ -destinationuserdestination_login ]  
    [ -destinationlocked ]  
    [ -blarge_object_bytes ]   
    [ -bfnumber_of_statements ]   
    [ -c ]   
    [ -dt ]   
    [ -ettable_name ]   
    [ -f [ file_name ] ]   
    [ -ooutput_file_name ]   
    [ -q ]   
    [ -rcnumber_of_retries ]   
    [ -riretry_interval ]   
    [ -strict ]  
    [ -tconnection_timeouts ]   
}  
```  
  
## <a name="arguments"></a>Argomenti  
 [ **-?** ]  
 Restituisce l'elenco dei parametri supportati.  
  
 **-sourceserver** *source_server_name*[ **\\** _instance_name_]  
 Nome del server di origine. Specificare _origine\_server\_name_ per l'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Specificare _origine\_server\_name_ **\\** _istanza\_nome_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **-sourcedatabase** *source_database*  
 Nome del database di origine.  
  
 **-sourcetable** *source_table_name*  
 Nome della tabella di origine sottoposta al controllo.  
  
 **-sourceschema** *source_schema_name*  
 Proprietario dello schema della tabella di origine. Per impostazione predefinita, dbo viene considerato il proprietario della tabella.  
  
 **-sourcepassword** *source_password*  
 Password di accesso usata per connettersi al server di origine mediante l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Se possibile, specificare le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è consigliabile proteggere il file per evitare accessi non autorizzati.  
  
 **-sourceuser** *source_login*  
 Account di accesso usato per connettersi al server di origine mediante l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se non si specifica il parametro *source_login* , durante la connessione al server di origine viene usata l'autenticazione di Windows. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-sourcelocked**  
 La tabella di origine viene bloccata durante il confronto mediante gli hint di tabella TABLOCK e HOLDLOCK.  
  
 **-destinationserver** *destination_server_name*[ **\\** _istanza\_nome_]  
 Nome del server di destinazione. Specificare *destination_server_name* per l'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Specificare _destinazione\_server\_name_ **\\** _istanza\_nome_ per un'istanza denominata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **-destinationdatabase** *subscription_database*  
 Nome del database di destinazione.  
  
 **-destinationtable** *destination_table*  
 Nome della tabella di destinazione.  
  
 **-destinationschema** *destination_schema_name*  
 Proprietario dello schema della tabella di destinazione. Per impostazione predefinita, dbo viene considerato il proprietario della tabella.  
  
 **-destinationpassword** *destination_password*  
 Password di accesso usata per connettersi al server di destinazione mediante l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Se possibile, specificare le credenziali di sicurezza in fase di esecuzione. Se è necessario archiviare le credenziali in un file script, è consigliabile proteggere il file per evitare accessi non autorizzati.  
  
 **-destinationuser** *destination_login*  
 Account di accesso usato per connettersi al server di destinazione mediante l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se non si specifica il parametro *destination_login* , durante la connessione al server viene usata l'autenticazione di Windows. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-destinationlocked**  
 La tabella di destinazione viene bloccata durante il confronto mediante gli hint di tabella TABLOCK e HOLDLOCK.  
  
 **-b** *large_object_bytes*  
 Numero di byte per confrontare le colonne con tipo di dati LOB, ovvero `text`, `ntext`, `image`, `varchar(max)`, `nvarchar(max)` e `varbinary(max)`. L'impostazione predefinita di*large_object_bytes* corrisponde alle dimensioni della colonna. I dati che superano il valore di *large_object_bytes* non verranno confrontati.  
  
 **-bf**  *number_of_statements*  
 Numero di istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] da scrivere nel file script [!INCLUDE[tsql](../includes/tsql-md.md)] corrente quando si usa l'opzione **-f** . Se il numero di istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] supera il valore di *number_of_statements*, viene creato un nuovo file script [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
 **-c**  
 Esegue il confronto per individuare eventuali differenze a livello di colonna.  
  
 **-dt**  
 Elimina la tabella dei risultati specificata da *table_name*se la tabella esiste già.  
  
 **-et** *table_name*  
 Specifica il nome della tabella dei risultati da creare. Se questa tabella esiste già, è necessario usare l'opzione **-DT** . In caso contrario, l'operazione ha esito negativo.  
  
 **-f** [ *file_name* ]  
 Genera uno script [!INCLUDE[tsql](../includes/tsql-md.md)] per ripristinare la convergenza tra la tabella nel server di destinazione e quella nel server di origine. È possibile specificare facoltativamente un nome e un percorso per il file script [!INCLUDE[tsql](../includes/tsql-md.md)] generato. Se *file_name* viene omesso, il file script [!INCLUDE[tsql](../includes/tsql-md.md)] verrà generato nella directory in cui si esegue l'utilità.  
  
 **-o** *output_file_name*  
 Nome e percorso completi del file di output.  
  
 **-q**  
 Esegue un confronto rapido mediante il confronto solo dei conteggi delle righe e degli schemi.  
  
 **-rc** *number_of_retries*  
 Numero di tentativi di esecuzione di un'operazione non riuscita compiuti dall'utilità.  
  
 **-ri**  *retry_interval*  
 Intervallo espresso in secondi tra i vari tentativi.  
  
 **-strict**  
 Gli schemi di origine e di destinazione vengono confrontati rigorosamente.  
  
 **-t** *connection_timeouts*  
 Imposta il periodo di timeout della connessione, espresso in secondi, per le connessioni al server di origine e al server di destinazione.  
  
## <a name="return-value"></a>Valore restituito  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Riuscito|  
|**1**|Errore critico|  
|**2**|Differenze tra tabelle|  
  
## <a name="remarks"></a>Note  
 L'utilità **tablediff** non può essere usata con server non[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Le tabelle contenenti colonne con il tipo di dati `sql_variant` non sono supportate.  
  
 Per impostazione predefinita, l'utilità **tablediff** supporta i mapping dei tipi di dati tra colonne di origine e di destinazione elencati di seguito.  
  
|Tipo di dati di origine|Tipo di dati di destinazione|  
|----------------------|---------------------------|  
|`tinyint`|`smallint`, `int` o `bigint`|  
|`smallint`|`int` o `bigint`|  
|`int`|`bigint`|  
|`timestamp`|`varbinary`|  
|`varchar(max)`|`text`|  
|`nvarchar(max)`|`ntext`|  
|`varbinary(max)`|`image`|  
|`text`|`varchar(max)`|  
|`ntext`|`nvarchar(max)`|  
|`image`|`varbinary(max)`|  
  
 Usare l'opzione **-strict** per disabilitare questi mapping ed eseguire una convalida di tipo strict.  
  
 La tabella di origine utilizzata per il confronto deve contenere almeno una chiave primaria, un'identità o una colonna ROWGUID. Se si usa l'opzione **-strict** , anche la tabella di destinazione deve contenere una chiave primaria, un'identità o una colonna ROWGUID.  
  
 Lo script [!INCLUDE[tsql](../includes/tsql-md.md)] generato per rendere convergente la tabella di destinazione non include i tipi di dati seguenti:  
  
-   `varchar(max)`  
  
-   `nvarchar(max)`  
  
-   `varbinary(max)`  
  
-   `timestamp`  
  
-   **xml**  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
## <a name="permissions"></a>Permissions  
 Per confrontare tabelle, è necessario disporre delle autorizzazioni SELECT ALL sugli oggetti tabella da confrontare.  
  
 Per usare l'opzione **-et** , è necessario essere membro del ruolo predefinito del database db_owner oppure disporre almeno dell'autorizzazione CREATE TABLE nel database di sottoscrizione e dell'autorizzazione ALTER per lo schema del proprietario della destinazione nel server di destinazione.  
  
 Per usare l'opzione **-dt** , è necessario essere membro del ruolo predefinito del database db_owner oppure disporre almeno dell'autorizzazione ALTER per lo schema del proprietario della destinazione nel server di destinazione.  
  
 Per usare l'opzione **-o** oppure **-f** , è necessario avere autorizzazioni di scrittura per il percorso della directory di file specificato.  
  
## <a name="see-also"></a>Vedere anche  
 [Confronto di tabelle replicate al fine di individuare le differenze &#40;programmazione della replica&#41;](../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)  
  
  
