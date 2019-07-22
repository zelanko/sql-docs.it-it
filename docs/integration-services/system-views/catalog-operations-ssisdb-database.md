---
title: catalog.operations (database SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- operations view [Integration Services]
- catalog.operations view [Integration Services]
ms.assetid: 9455c5b1-60ff-45fc-8599-cc3abbd6daf5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5f1f3695854adbb49c57716f3273e176d7e1fa62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045218"
---
# <a name="catalogoperations-ssisdb-database"></a>catalog.operations (database SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Vengono visualizzati i dettagli di tutte le operazioni nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|operation_id|**bigint**|Identificatore (ID) univoco dell'operazione.|  
|operation_type|**smallint**|Tipo di operazione.|  
|created_time|**datetimeoffset**|Ora di creazione dell'operazione.|  
|object_type|**smallint**|Tipo di oggetto interessato dall'operazione. L'oggetto può essere una cartella (`10`), un progetto (`20`), un pacchetto (`30`), un ambiente (`40`) o un'istanza di esecuzione (`50`).|  
|object_id|**bigint**|ID dell'oggetto interessato dall'operazione.|  
|object_name|**nvarchar(260)**|Nome dell'oggetto .|  
|status|**int**|Stato dell'operazione. I valori possibili sono Creata (`1`), In esecuzione (`2`), Operazione annullata (`3`) Operazione non riuscita (`4`), In sospeso (`5`), Terminata in modo inatteso (`6`), Operazione riuscita (`7`), Arresto in corso (`8`) Operazione completata (`9`).|  
|start_time|**datetimeoffset**|Ora di inizio dell'operazione.|  
|end_time|**datetimeoffsset**|Ora di fine dell'operazione.|  
|caller_sid|**varbinary(85)**|ID di sicurezza (SID) dell'utente se per l'accesso è stata utilizzata l'autenticazione di Windows.|  
|caller_name|**nvarchar(128)**|Nome dell'account tramite cui è stata eseguita l'operazione.|  
|process_id|**int**|ID processo del programma esterno, se applicabile.|  
|stopped_by_sid|**varbinary(85)**|SID dell'utente che ha arrestato l'operazione.|  
|stopped_by_name|**nvarchar(128)**|Nome dell'utente che ha arrestato l'operazione.|  
|server_name|**nvarchar(128)**|Informazioni relative al server Windows e all'istanza per un'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|machine_name|**nvarchar(128)**|Nome del computer in cui è in esecuzione l'istanza del server.|  
  
## <a name="remarks"></a>Remarks  
 In questa vista viene visualizzata una riga per ogni operazione nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Tale vista consente all'amministratore di enumerare tutte le operazioni logiche eseguite nel server, ad esempio la distribuzione di un progetto o l'esecuzione di un pacchetto.  
  
 In questa vista vengono visualizzati i tipi di operazione seguenti, come elencati nella colonna **operation_type**:  
  
|Valore **operation_type**|Descrizione **operation_type**|Descrizione **object_id**|Descrizione **object_name**|  
|-------------------------------|-------------------------------------|--------------------------------|----------------------------------|  
|`1`|Inizializzazione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|**NULL**|**NULL**|  
|`2`|Periodo di memorizzazione<br /><br /> (processo di SQL Agent)|**NULL**|**NULL**|  
|`3`|MaxProjectVersion<br /><br /> (processo di SQL Agent)|**NULL**|**NULL**|  
|`101`|**deploy_project**<br /><br /> (stored procedure)|ID progetto|Nome del progetto|  
|`106`|**restore_project**<br /><br /> (stored procedure)|ID progetto|Nome del progetto|  
|`200`|**create_execution** e **start_execution**<br /><br /> (stored procedure)|ID progetto|**NULL**|  
|`202`|**stop_operation**<br /><br /> (stored procedure)|ID progetto|**NULL**|  
|`300`|**validate_project**<br /><br /> (stored procedure)|ID progetto|Nome del progetto|  
|`301`|**validate_package**<br /><br /> (stored procedure)|ID progetto|Nome pacchetto|  
|`1000`|**configure_catalog**<br /><br /> (stored procedure)|**NULL**|**NULL**||  
  
## <a name="permissions"></a>Autorizzazioni  
 Per questa vista è necessaria una delle autorizzazioni seguenti:  
  
-   Autorizzazione READ per l'operazione  
  
-   Appartenenza al ruolo del database **ssis_admin**  
  
-   Appartenenza al ruolo del server **sysadmin**  
  
> [!NOTE]  
>  Quando si dispone delle autorizzazioni per eseguire un'operazione nel server, si dispone anche delle autorizzazioni per visualizzare le informazioni sull'operazione. È applicata la sicurezza a livello di riga, pertanto vengono visualizzate solo le righe per le quali si dispone delle autorizzazioni per la visualizzazione.  
  
  
