---
title: Implementazione di assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dc1bfce77a089b24e68613c94af6e2886e6b5952
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874465"
---
# <a name="implementing-assemblies"></a>Implementazione di assembly
  In questo argomento vengono fornite informazioni sull'implementazione e l'utilizzo degli assembly nei database, suddivise nelle sezioni seguenti:  
  
-   Creazione di assembly  
  
-   Modifica di assembly  
  
-   Eliminazione, disabilitazione e abilitazione di assembly  
  
-   Gestione delle versioni degli assembly  
  
## <a name="creating-assemblies"></a>Creazione di assembly  
 Gli assembly vengono creati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY, oppure in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] utilizzando l'editor di assembly assistito. Inoltre, la distribuzione di un progetto di SQL Server in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registra un assembly nel database che è stato specificato per il progetto. Per altre informazioni, vedere [Distribuzione di oggetti di database CLR](deploying-clr-database-objects.md).  
  
 **Per creare un assembly utilizzando Transact-SQL**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
 **Per creare un assembly utilizzando SQL Server Management Studio**  
  
-   [Proprietà degli assembly &#40;pagina Generale&#41;](assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>Modifica di assembly  
 Gli assembly vengono modificati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY, oppure in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] utilizzando l'editor di assembly assistito. È possibile modificare un assembly quando si desidera allo scopo di:  
  
-   Modificare l'implementazione dell'assembly caricando una versione più recente del file binario dell'assembly. Per altre informazioni, vedere [la gestione delle versioni degli Assembly](#_managing) più avanti in questo argomento.  
  
-   Modificare il set di autorizzazioni dell'assembly. Per altre informazioni, vedere [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md).  
  
-   Modificare la visibilità dell'assembly. Agli assembly visibili è possibile fare riferimento in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli assembly non visibili non sono disponibili, anche se sono stati caricati nel database. Per impostazione predefinita, gli assembly caricati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono visibili.  
  
-   Aggiungere o eliminare un file di debug o di origine associato all'assembly.  
  
 **Per modificare un assembly utilizzando Transact-SQL**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
 **Per modificare un assembly utilizzando SQL Server Management Studio**  
  
-   [Proprietà degli assembly &#40;pagina Generale&#41;](assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>Eliminazione, disabilitazione e abilitazione di assembly  
 Per eliminare gli assembly, utilizzare l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY oppure [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Per eliminare un assembly utilizzando Transact-SQL**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Per eliminare un assembly utilizzando SQL Server Management Studio**  
  
-   [Eliminare oggetti](../../ssms/object/delete-objects.md)  
  
 Per impostazione predefinita, l'esecuzione di tutti gli assembly creati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disabilitata. È possibile usare la **clr abilitato** opzione delle **sp_configure** sistema stored procedure per disabilitare o abilitare l'esecuzione di tutti gli assembly vengono caricati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La disabilitazione dell'esecuzione degli assembly impedisce l'esecuzione di funzioni CRL (Common Language Runtime), stored procedure, trigger, funzioni di aggregazione e tipi definiti dall'utente e arresta le funzioni attualmente in esecuzione. La disabilitazione dell'esecuzione degli assembly non ne impedisce la creazione, la modifica o l'eliminazione. Per altre informazioni, vedere [opzione di configurazione Server clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md).  
  
 **Per disabilitare e abilitare l'esecuzione di assembly**  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
##  <a name="_managing"></a> La gestione delle versioni degli Assembly  
 Quando si carica un assembly in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'assembly viene archiviato e gestito all'interno dei cataloghi di sistema del database. Tutte le modifiche apportate alla definizione dell'assembly nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve essere propagata all'assembly che viene archiviato nel catalogo del database.  
  
 Quando si modifica un assembly, è necessario eseguire un'istruzione ALTER ASSEMBLY per aggiornare l'assembly nel database. In questo modo l'assembly verrà aggiornato in base alla copia più recente dei moduli [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] che ne contengono l'implementazione.  
  
 La clausola WITH UNCHECKED DATA dell'istruzione ALTER ASSEMBLY richiede a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di eseguire anche l'aggiornamento degli assembly dai quali dipendono i dati persistenti del database. In particolare, è necessario specificare WITH UNCHECKED DATA nei seguenti casi:  
  
-   Se esistono colonne calcolate persistenti che fanno riferimento a metodi nell'assembly, direttamente o indirettamente, mediante funzioni o metodi [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Se esistono colonne di un tipo CLR definito dall'utente che dipendono dall'assembly e il tipo implementa un formato di serializzazione **UserDefined** (non **Native**).  
  
> [!CAUTION]  
>  Se non è specificata la clausola WITH UNCHECKED DATA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta di impedire l'esecuzione dell'istruzione ALTER ASSEMBLY nel caso in cui la nuova versione dell'assembly modifichi i dati esistenti in tabelle, indici o altre posizioni persistenti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non garantisce tuttavia che le colonne calcolate, gli indici, le viste indicizzate o le espressioni saranno consistenti con i tipi e le routine sottostanti in caso di aggiornamento dell'assembly CLR. Quando si esegue l'istruzione ALTER ASSEMBLY è pertanto necessario verificare che non vi siano discrepanze tra il risultato di una determinata espressione e il valore basato su tale espressione archiviato nell'assembly.  
  
 Solo i membri del **db_owner** e **db_ddlowner** ruolo predefinito del database può eseguire ALTER ASSEMBLY utilizzando la clausola WITH UNCHECKED DATA.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] invia al registro eventi applicazioni di Windows il messaggio che l'assembly è stato modificato con dati non controllati nelle tabelle. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contrassegna quindi le eventuali tabelle che contengono dati dipendenti dall'assembly come contenenti dati non controllati. Il **has_unchecked_assembly_data** colonna il **Sys. Tables** vista del catalogo contiene il valore 1 per le tabelle che contengono dati non controllati e 0 per le tabelle senza dati non controllati.  
  
 Per verificare l'integrità dei dati non controllati, eseguire DBCC CHECKTABLE su tutte le tabelle contenenti dati non controllati. Se DBCC CHECKTABLE ha esito negativo è necessario eliminare le righe non valide della tabella oppure modificare il codice dell'assembly per risolvere i problemi e quindi eseguire altre istruzioni ALTER ASSEMBLY.  
  
 ALTER ASSEMBLY modifica la versione dell'assembly. Le impostazioni cultura e token di chiave pubblica dell'assembly restano invariati. SQL Server non consente la registrazione di versioni diverse di un assembly con lo stesso nome, le impostazioni cultura e la chiave pubblica.  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>Interazioni con i criteri del computer per l'associazione delle versioni  
 Se i riferimenti agli assembly archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono reindirizzati a versioni specifiche utilizzando i criteri del computer forniti dall'editore o dall'amministratore, è necessario eseguire una delle operazioni seguenti:  
  
-   Verificare che la nuova versione alla quale viene eseguito il reindirizzamento si trovi nel database.  
  
-   Modificare qualsiasi istruzione nei file di criteri esterni del computer o nei criteri editore per assicurarsi che facciano riferimento alla specifica versione presente nel database.  
  
 In caso contrario, il tentativo di caricare una nuova versione dell'assembly nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] avrà esito negativo.  
  
 **Per aggiornare la versione di un assembly**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Gli assembly &#40;motore di Database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Recupero di informazioni sugli assembly](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
