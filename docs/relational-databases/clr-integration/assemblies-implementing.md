---
title: Implementazione di assembly | Microsoft Docs
description: Informazioni su come usare gli assembly ospitati in SQL Server, tra cui come creare/modificare assembly, eliminare o abilitare/disabilitare gli assembly e gestire le versioni.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d97ef8c7dfc617cb6cd56dbcc6d83e0540051d7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85695364"
---
# <a name="assemblies---implementing"></a>Assembly - Implementazione
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  In questo argomento vengono fornite informazioni sull'implementazione e l'utilizzo degli assembly nei database, suddivise nelle sezioni seguenti:  
  
-   Creazione di assembly  
  
-   Modifica di assembly  
  
-   Eliminazione, disabilitazione e abilitazione di assembly  
  
-   Gestione delle versioni degli assembly  
  
## <a name="creating-assemblies"></a>Creazione di assembly  
 Gli assembly vengono creati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY, oppure in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] utilizzando l'editor di assembly assistito. Inoltre, la distribuzione di un progetto di SQL Server in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un assembly nel database specificato per il progetto. Per altre informazioni, vedere [Distribuzione di oggetti di database CLR](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
  
 **Per creare un assembly utilizzando Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **Per creare un assembly utilizzando SQL Server Management Studio**  
  
-   [Proprietà assembly &#40;pagina generale&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modifica di assembly  
 Gli assembly vengono modificati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY, oppure in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] utilizzando l'editor di assembly assistito. È possibile modificare un assembly quando si desidera allo scopo di:  
  
-   Modificare l'implementazione dell'assembly caricando una versione più recente del file binario dell'assembly. Per ulteriori informazioni, vedere [gestione delle versioni degli assembly](#_managing) più avanti in questo argomento.  
  
-   Modificare il set di autorizzazioni dell'assembly. Per altre informazioni, vedere [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Modificare la visibilità dell'assembly. Agli assembly visibili è possibile fare riferimento in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli assembly non visibili non sono disponibili, anche se sono stati caricati nel database. Per impostazione predefinita, gli assembly caricati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono visibili.  
  
-   Aggiungere o eliminare un file di debug o di origine associato all'assembly.  
  
 **Per modificare un assembly utilizzando Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **Per modificare un assembly utilizzando SQL Server Management Studio**  
  
-   [Proprietà assembly &#40;pagina generale&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Eliminazione, disabilitazione e abilitazione di assembly  
 Per eliminare gli assembly, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY oppure [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Per eliminare un assembly utilizzando Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Per eliminare un assembly utilizzando SQL Server Management Studio**  
  
-   [Elimina oggetti](../../ssms/object/delete-objects.md)  
  
 Per impostazione predefinita, l'esecuzione di tutti gli assembly creati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disabilitata. È possibile utilizzare l'opzione **clr enabled** del sistema **sp_configure** stored procedure per disabilitare o abilitare l'esecuzione di tutti gli assembly caricati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La disabilitazione dell'esecuzione degli assembly impedisce l'esecuzione di funzioni CRL (Common Language Runtime), stored procedure, trigger, funzioni di aggregazione e tipi definiti dall'utente e arresta le funzioni attualmente in esecuzione. La disabilitazione dell'esecuzione degli assembly non ne impedisce la creazione, la modifica o l'eliminazione. Per ulteriori informazioni, vedere [opzione di configurazione del server clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md).  
  
 **Per abilitare e disabilitare l'esecuzione degli assembly**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="managing-assembly-versions"></a><a name="_managing"></a>Gestione delle versioni degli assembly  
 Quando si carica un assembly in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'assembly viene archiviato e gestito all'interno dei cataloghi di sistema del database. Tutte le modifiche apportate alla definizione dell'assembly in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] devono essere propagate all'assembly archiviato nel catalogo del database.  
  
 Quando si modifica un assembly, è necessario eseguire un'istruzione ALTER ASSEMBLY per aggiornare l'assembly nel database. In questo modo l'assembly verrà aggiornato in base alla copia più recente dei moduli [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] che ne contengono l'implementazione.  
  
 La clausola WITH UNCHECKED DATA dell'istruzione ALTER ASSEMBLY richiede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di eseguire anche l'aggiornamento degli assembly dai quali dipendono i dati persistenti del database. In particolare, è necessario specificare WITH UNCHECKED DATA nei seguenti casi:  
  
-   Se esistono colonne calcolate persistenti che fanno riferimento a metodi nell'assembly, direttamente o indirettamente, mediante funzioni o metodi [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Se esistono colonne di un tipo CLR definito dall'utente che dipendono dall'assembly e il tipo implementa un formato di serializzazione **UserDefined** (non **Native**).  
  
> [!CAUTION]  
>  Se non è specificata la clausola WITH UNCHECKED DATA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di impedire l'esecuzione dell'istruzione ALTER ASSEMBLY nel caso in cui la nuova versione dell'assembly modifichi i dati esistenti in tabelle, indici o altre posizioni persistenti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non garantisce tuttavia che le colonne calcolate, gli indici, le viste indicizzate o le espressioni saranno consistenti con i tipi e le routine sottostanti in caso di aggiornamento dell'assembly CLR. Quando si esegue l'istruzione ALTER ASSEMBLY è pertanto necessario verificare che non vi siano discrepanze tra il risultato di una determinata espressione e il valore basato su tale espressione archiviato nell'assembly.  
  
 Solo i membri del ruolo predefinito del database **db_owner** e **DB_DDLOWNER** possono eseguire ALTER assembly utilizzando la clausola with unchecked data.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] invia al registro eventi applicazioni di Windows il messaggio che l'assembly è stato modificato con dati non controllati nelle tabelle. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contrassegna quindi le eventuali tabelle che contengono dati dipendenti dall'assembly come contenenti dati non controllati. La colonna **has_unchecked_assembly_data** della vista del catalogo **sys. Tables** contiene il valore 1 per le tabelle che contengono dati non verificati e 0 per le tabelle senza dati non verificati.  
  
 Per risolvere l'integrità dei dati non verificati, eseguire DBCC CHECKDB con EXTENDED_LOGICAL_CHECKS su ogni tabella che contiene dati non verificati. Se DBCC CHECKDB con EXTENDED_LOGICAL_CHECKS ha esito negativo, è necessario eliminare le righe della tabella non valide o modificare il codice dell'assembly per risolvere i problemi, quindi eseguire istruzioni ALTER ASSEMBLY aggiuntive.  
  
 ALTER ASSEMBLY modifica la versione dell'assembly. Le impostazioni cultura e il token di chiave pubblica dell'assembly rimangono invariati. SQL Server non consente la registrazione di versioni diverse di un assembly con lo stesso nome, lingua e chiave pubblica.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interazioni con i criteri del computer per l'associazione delle versioni  
 Se i riferimenti agli assembly archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono reindirizzati a versioni specifiche utilizzando i criteri del computer forniti dall'editore o dall'amministratore, è necessario eseguire una delle operazioni seguenti:  
  
-   Verificare che la nuova versione alla quale viene eseguito il reindirizzamento si trovi nel database.  
  
-   Modificare qualsiasi istruzione nei file di criteri esterni del computer o nei criteri editore per assicurarsi che facciano riferimento alla specifica versione presente nel database.  
  
 In caso contrario, il tentativo di caricare una nuova versione dell'assembly nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avrà esito negativo.  
  
 **Per aggiornare la versione di un assembly**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly &#40;motore di database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Recupero di informazioni sugli assembly](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
