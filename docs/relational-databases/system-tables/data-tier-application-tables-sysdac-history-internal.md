---
title: sysdac_history_internal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdac_history_internal
- sysdac_history_internal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysdac_history_internal
ms.assetid: 774a1678-0b27-42be-8adc-a6d7a4a56510
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40696085bc8eb9980d1150feade91a9edd627be0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471140"
---
# <a name="data-tier-application-tables---sysdachistoryinternal"></a>Tabelle applicazioni livello dati - sysdac_history_internal
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene informazioni sulle azioni eseguite per gestire le applicazioni livello dati. Questa tabella è archiviata nel **dbo** dello schema delle **msdb** database.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**action_id**|**int**|Identificatore dell'azione|  
|**sequence_id**|**int**|Consente di identificare un passaggio all'interno di un'azione.|  
|**instance_id**|**uniqueidentifier**|Identificatore dell'istanza di applicazione livello dati. Questa colonna può essere unita la **instance_id** colonna nelle [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md).|  
|**action_type**|**tinyint**|Identificatore del tipo di azione:<br /><br /> **0** = distribuzione<br /><br /> **1** = creazione<br /><br /> **2** = ridenominazione<br /><br /> **3** = detach<br /><br /> **4** = delete|  
|**action_type_name**|**varchar(19)**|Nome del tipo di azione:<br /><br /> **deploy**<br /><br /> **create**<br /><br /> **rename**<br /><br /> **detach**<br /><br /> **delete**|  
|**dac_object_type**|**tinyint**|Identificatore del tipo di oggetto interessato dall'azione:<br /><br /> **0** = dacpac<br /><br /> **1** = login<br /><br /> **2** = database|  
|**dac_object_type_name**|**varchar(8)**|Nome del tipo di oggetto interessato dall'azione:<br /><br /> **file dacpac** = istanza di applicazione livello dati<br /><br /> **login**<br /><br /> **database**|  
|**action_status**|**tinyint**|Codice di identificazione dello stato corrente dell'azione:<br /><br /> **0** = in sospeso<br /><br /> **1** = success<br /><br /> **2** = fail|  
|**action_status_name**|**varchar(11)**|Stato corrente dell'azione:<br /><br /> **pending**<br /><br /> **success**<br /><br /> **fail**|  
|**Obbligatorio**|**bit**|Utilizzato dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] per il rollback di un'operazione dell'applicazione livello dati.|  
|**dac_object_name_pretran**|**sysname**|Nome dell'oggetto prima dell'esecuzione del commit della transazione contenente l'azione. Utilizzato solo per database e account di accesso.|  
|**dac_object_name_posttran**|**sysname**|Nome dell'oggetto dopo l'esecuzione del commit della transazione contenente l'azione. Utilizzato solo per database e account di accesso.|  
|**sqlscript**|**nvarchar(max)**|Script [!INCLUDE[tsql](../../includes/tsql-md.md)] che implementa un'azione in un database o account di accesso.|  
|**payload**|**varbinary(max)**|Definizione del pacchetto di applicazione livello dati salvata in una stringa codificata binaria.|  
|**Commenti**|**ntext**|Consente di registrare l'accesso di un utente che ha accettato la possibile perdita dei dati in un aggiornamento dell'applicazione livello dati.|  
|**error_string**|**nvarchar(max)**|Messaggio di errore generato se l'azione rileva un errore.|  
|**created_by**|**sysname**|Account di accesso che ha avviato l'azione di creazione questa voce.|  
|**date_created**|**datetime**|Data e ora di creazione della voce.|  
|**date_modified**|**datetime**|Data e ora dell'ultima modifica della voce.|  
  
## <a name="remarks"></a>Note  
 Le azioni di gestione di applicazione livello dati, quali ad esempio la distribuzione o l'eliminazione di un'applicazione livello dati, generano più passaggi. A ogni azione viene assegnato un identificatore dell'azione. Ogni passaggio viene assegnato un numero di sequenza e una riga in **sysdac_history_internal**, in cui viene registrato lo stato del passaggio. Ogni riga viene creata all'avvio del passaggio dell'azione e aggiornata in base alle necessità per riflettere lo stato dell'operazione. Ad esempio, un'operazione di distribuzione dell'applicazione livello dati è stato possibile assegnare **action_id** 12 e quattro righe nel **sysdac_history_internal**:  
  
|||||  
|-|-|-|-|  
|**action_id**|**sequence_id**|**action_type_name**|**dac_object_type_name**|  
|12|0|create|dacpac|  
|12|1|create|login|  
|12|2|create|Database|  
|12|3|ridenominazione|Database|  
  
 Operazioni di applicazione livello dati, ad esempio delete, non rimuovono righe dalla **sysdac_history_internal**. È possibile utilizzare la query seguente per eliminare manualmente le righe per le applicazioni livello dati non più distribuite su un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
```sql  
DELETE FROM msdb.dbo.sysdac_history_internal  
WHERE instance_id NOT IN  
   (SELECT instance_id  
    FROM msdb.dbo.sysdac_instances_internal);  
```  
  
 L'eliminazione delle righe per le applicazioni livello dati attive non influisce sulle operazioni di applicazione livello dati; l'unico effetto è che non sarà possibile registrare la cronologia completa dell'applicazione livello dati.  
  
> [!NOTE]  
>  Attualmente non è disponibile alcun meccanismo per l'eliminazione **sysdac_history_internal** righe su [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'appartenenza al ruolo predefinito del server sysadmin. Accesso in lettura a questa vista è disponibile per tutti gli utenti con autorizzazioni sufficienti per connettersi al database master.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazioni livello dati](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [dbo.sysdac_instances &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances.md)   
 [sysdac_instances_internal &#40;Transact-SQL&#41;](../../relational-databases/system-tables/data-tier-application-tables-sysdac-instances-internal.md)  
  
  
