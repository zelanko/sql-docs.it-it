---
title: Visualizzare e leggere il log di diagnostica dell'istanza del cluster di failover| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 68074bd5-be9d-4487-a320-5b51ef8e2b2d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 774dc4ec4a02c72420d004909cb7e6ee1b31f3a7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046073"
---
# <a name="view-and-read-failover-cluster-instance-diagnostics-log"></a>Visualizzazione e lettura del log di diagnostica dell'istanza del cluster di failover
  Tutti gli errori critici e gli eventi di avviso relativi alla DLL risorse SQL Server vengono scritti nel registro eventi di Windows. Un log in esecuzione relativo a informazioni di diagnostica specifiche di SQL Server viene acquisito dalla stored procedure di sistema [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) e viene scritto nei file di log di diagnostica del cluster di failover di SQL Server, noti anche come log *SQLDIAG*.  
  
-   **Prima di iniziare:**  [Indicazioni](#Recommendations), [Sicurezza](#Security)  
  
-   **Per visualizzare il log di diagnostica usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Per configurare le impostazioni del log di diagnostica usando:** [Transact-SQL](#TsqlConfigure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
 Per impostazione predefinita, l'utilità SQLdiag è archiviata in una cartella LOG locale della directory dell'istanza di SQL Server, ad esempio,' C\programmi\microsoft Files\Microsoft SQL Server\MSSQL12. \<InstanceName> \MSSQL\LOG ' del nodo proprietario dell'istanza del cluster di failover (FCI) AlwaysOn. La dimensione di ogni file di log SQLDIAG è pari a 100 MB. Successivamente, tali file di log vengono archiviati nel computer prima di essere riciclati per i nuovi log.  
  
 Nei log viene utilizzato il formato di file degli eventi estesi. La funzione di sistema **sys.fn_xe_file_target_read_file** può essere usata per leggere i file creati dagli eventi estesi. Viene restituito un evento per riga in formato XML. Eseguire una query sulla vista di sistema per analizzare i dati XML come set di risultati. Per altre informazioni, vedere [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 L'autorizzazione VIEW SERVER STATE è necessaria per eseguire **fn_xe_file_target_read_file**.  
  
 Aprire SQL Server Management Studio come amministratore.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per visualizzare i file di log di diagnostica:**  
  
1.  Scegliere **Apri** dal menu **File**, selezionare **File**, quindi scegliere il file di log di diagnostica che si desidera visualizzare.  
  
2.  Gli eventi vengono visualizzati come righe nel riquadro destro e per impostazione predefinita **name**e **timestamp** sono le uniche due colonne visualizzate.  
  
     Viene inoltre attivato il menu **ExtendedEvents** .  
  
3.  Per visualizzare più colonne, passare al menu **ExtendedEvents** e selezionare **Scegli colonne**.  
  
     Verrà visualizzata una finestra di dialogo con le colonne disponibili in cui è possibile selezionare le colonne da visualizzare.  
  
4.  È possibile filtrare e ordinare i dati degli eventi utilizzando il menu **ExtendedEvents** e selezionando l'opzione **Filtro** .  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per visualizzare i file di log di diagnostica:**  
  
 Per visualizzare tutte le voci di log nel file di log SQLDIAG, utilizzare la query seguente:  
  
```  
SELECT  
xml_data.value('(event/@name)[1]','varchar(max)') AS 'Name'  
,xml_data.value('(event/@package)[1]','varchar(max)') AS 'Package'  
,xml_data.value('(event/@timestamp)[1]','datetime') AS 'Time'  
,xml_data.value('(event/data[@name=''state'']/value)[1]','int') AS 'State'  
,xml_data.value('(event/data[@name=''state_desc'']/text)[1]','varchar(max)') AS 'State Description'  
,xml_data.value('(event/data[@name=''failure_condition_level'']/value)[1]','int') AS 'Failure Conditions'  
,xml_data.value('(event/data[@name=''node_name'']/value)[1]','varchar(max)') AS 'Node_Name'  
,xml_data.value('(event/data[@name=''instancename'']/value)[1]','varchar(max)') AS 'Instance Name'  
,xml_data.value('(event/data[@name=''creation time'']/value)[1]','datetime') AS 'Creation Time'  
,xml_data.value('(event/data[@name=''component'']/value)[1]','varchar(max)') AS 'Component'  
,xml_data.value('(event/data[@name=''data'']/value)[1]','varchar(max)') AS 'Data'  
,xml_data.value('(event/data[@name=''info'']/value)[1]','varchar(max)') AS 'Info'  
FROM  
 ( SELECT object_name AS 'event'  
  ,CONVERT(xml,event_data) AS 'xml_data'  
  FROM sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SQLNODE1_MSSQLSERVER_SQLDIAG_0_129936003752530000.xel',NULL,NULL,NULL)   
)   
AS XEventData  
ORDER BY Time;  
  
```  
  
> [!NOTE]  
>  È possibile filtrare i risultati in base a stati o componenti specifici utilizzando la clausola WHERE.  
  
##  <a name="using-transact-sql"></a><a name="TsqlConfigure"></a> Uso di Transact-SQL  
 **Per configurare le proprietà del log di diagnostica**  
  
> [!NOTE]  
>  Per un esempio di questa procedura, vedere [Esempio (Transact-SQL)](#TsqlExample)più avanti in questa sezione.  
  
 Utilizzando l'istruzione DDL (Data Definition Language), `ALTER SERVER CONFIGURATION` è possibile avviare o arrestare la registrazione dei dati di diagnostica acquisiti dalla [sp_server_diagnostics &#40;procedura&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) e impostare i parametri di configurazione dei log SQLDIAG, ad esempio il numero di rollover dei file di log, le dimensioni del file di log e il percorso del file. Per dettagli sulla sintassi, vedere [Setting diagnostic log options](/sql/t-sql/statements/alter-server-configuration-transact-sql#Diagnostic).  
  
###  <a name="examples-transact-sql"></a><a name="ConfigTsqlExample"></a> Esempi (Transact-SQL)  
  
####  <a name="setting-diagnostic-log-options"></a><a name="TsqlExample"></a>Impostazione delle opzioni del log di diagnostica  
 Negli esempi inclusi in questa sezione viene illustrato come impostare i valori per l'opzione del log di diagnostica.  
  
##### <a name="a-starting-diagnostic-logging"></a>R. Avvio della registrazione dei dati di diagnostica  
 Nell'esempio seguente viene avviata la registrazione dei dati di diagnostica.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
##### <a name="b-stopping-diagnostic-logging"></a>B. Arresto della registrazione dei dati di diagnostica  
 Nell'esempio seguente viene arrestata la registrazione dei dati di diagnostica.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
##### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. Definizione della posizione dei log di diagnostica  
 Nell'esempio seguente viene impostata la posizione dei log di diagnostica sul percorso di file specificato.  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
##### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. Definizione della dimensione massima di ogni log di diagnostica  
 Nell'esempio seguente viene impostata su 10 megabyte la dimensione massima di ogni log di diagnostica.  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Criteri di failover per le istanze del cluster di failover](failover-policy-for-failover-cluster-instances.md)  
  
  
