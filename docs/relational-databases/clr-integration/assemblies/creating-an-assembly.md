---
title: Creazione di un assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 9493567f33cf07dbfa9ae4f19d037a7db6157eda
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907394"
---
# <a name="creating-an-assembly"></a>Creazione di un assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gli oggetti di database gestiti, ad esempio le stored procedure o i trigger, vengono compilati e quindi distribuiti in unità denominate assembly. Gli assembly DLL gestiti devono essere registrati in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] prima di poter usare la funzionalità fornita dall'assembly. Per registrare l'assembly in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], utilizzare l'istruzione CREATE ASSEMBLY. In questo argomento viene descritto come registrare un assembly in un database tramite l'istruzione CREATE ASSEMBLY e specificare le impostazioni di sicurezza per l'assembly.  
  
## <a name="the-create-assembly-statement"></a>Istruzione CREATE ASSEMBLY  
 L'istruzione CREATE ASSEMBLY viene utilizzata per creare un assembly in un database. Esempio:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 La clausola FROM specifica il percorso dell'assembly da creare. Questo percorso può essere un percorso UNC (Universal Naming Convention) o un percorso di file fisico locale rispetto al computer.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non consente la registrazione di versioni diverse di un assembly con lo stesso nome, lingua e chiave pubblica.  
  
 È possibile creare assembly che fanno riferimento ad altri assembly. Quando si crea un assembly in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea anche gli assembly cui fa riferimento l'assembly di livello radice, se non sono già stati creati nel database.  
  
 Agli utenti del database o ai ruoli utente vengono concesse autorizzazioni per creare, e pertanto possedere, assembly in un database. Per creare assembly, l'utente o il ruolo del database deve disporre dell'autorizzazione CREATE ASSEMBLY.  
  
 Un assembly può fare riferimento ad altri assembly solo nei casi seguenti:  
  
-   L'assembly chiamato o cui si fa riferimento è di proprietà dello stesso utente o ruolo.  
  
-   L'assembly chiamato o cui si fa riferimento è stato creato nello stesso database.  
  
## <a name="specifying-security-when-creating-assemblies"></a>Configurazione della sicurezza durante la creazione di assembly  
 Quando si crea un assembly in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è possibile specificare uno dei tre diversi livelli di sicurezza in cui è possibile eseguire il codice: **Safe**, **EXTERNAL_ACCESS**o **unsafe**. Quando viene eseguita l'istruzione **create assembly** , vengono eseguiti alcuni controlli sull'assembly del codice che potrebbero causare la mancata registrazione dell'assembly nel server. Per ulteriori informazioni, vedere l'esempio di rappresentazione in [codeplex](https://msftengprodsamples.codeplex.com/).  
  
 **Safe** è il set di autorizzazioni predefinito e funziona per la maggior parte degli scenari. Per specificare un determinato livello di sicurezza, è necessario modificare la sintassi dell'istruzione CREATE ASSEMBLY come indicato di seguito:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 È anche possibile creare un assembly con il set di autorizzazioni **Safe** omettendo semplicemente la terza riga di codice precedente:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Quando il codice in un assembly viene eseguito con il set di autorizzazioni **Safe** , può eseguire solo calcoli e accesso ai dati all'interno del server tramite il provider gestito in-process.  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>Creazione di assembly EXTERNAL_ACCESS e UNSAFE  
 **EXTERNAL_ACCESS** risolve scenari in cui il codice deve accedere a risorse esterne al server, ad esempio file, rete, registro di sistema e variabili di ambiente. Ogni volta che il server accede a una risorsa esterna, rappresenta il contesto di sicurezza dell'utente che chiama il codice gestito.  
  
 L'autorizzazione per il codice non **sicuro** è per le situazioni in cui un assembly non è verificabile in modo sicuro o richiede un accesso aggiuntivo alle risorse limitate, ad esempio l'API Win32 [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
 Per creare un assembly **EXTERNAL_ACCESS** o **unsafe** in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario che venga soddisfatta una delle due condizioni seguenti:  
  
1.  L'assembly è firmato con nome sicuro o dispone di firma Authenticode con un certificato. Questo nome sicuro (o certificato) viene creato all'interno [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] come chiave asimmetrica (o certificato) e dispone di un account di accesso corrispondente con autorizzazione **External Access assembly** (per assembly di accesso esterni) o autorizzazione **UNSAFE assembly** (per assembly UNSAFE).  
  
2.  Il proprietario del database (DBO) dispone dell'autorizzazione **External Access assembly** (per gli assembly di **accesso esterni** ) o dell' **assembly UNSAFE** (per assembly **unsafe** ) e il database dispone della [proprietà di database TRUSTWORTHY](../../../relational-databases/security/trustworthy-database-property.md) impostata su  **IL**.  

 Le due condizioni elencate in precedenza vengono verificate in fase di caricamento dell'assembly (fase che include l'esecuzione). Per caricare l'assembly, è necessario che si verifichi almeno una delle due condizioni.  
  
 Si consiglia di non impostare la [proprietà di database TRUSTWORTHY](../../../relational-databases/security/trustworthy-database-property.md) in un database **su on** solo per eseguire il codice Common Language Runtime (CLR) nel processo server. È invece consigliabile creare una chiave asimmetrica dal file di assembly nel database master. È necessario creare un account di accesso di cui è stato eseguito il mapping a questa chiave asimmetrica e all'account di accesso deve essere concessa l'autorizzazione **External Access assembly** o **UNSAFE assembly** .  
  
 Le seguenti istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] eseguono i passaggi necessari per creare una chiave asimmetrica, eseguire il mapping di un account di accesso a questa chiave e quindi concedere l'autorizzazione **EXTERNAL_ACCESS** all'account di accesso. Prima di eseguire l'istruzione CREATE ASSEMBLY, è necessario eseguire le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguenti.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  È necessario creare un nuovo account di accesso da associare alla chiave asimmetrica. Questo account di accesso viene utilizzato solo per concedere le autorizzazioni e non è necessario che sia associato a un utente o utilizzato nell'applicazione.  
  
 Per creare un assembly di **accesso esterno** , l'autore deve avere l'autorizzazione di **accesso esterno** . Questa autorizzazione viene specificata durante la creazione dell'assembly:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 Le seguenti istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] eseguono i passaggi necessari per creare una chiave asimmetrica, eseguire il mapping di un account di accesso a questa chiave e quindi concedere l'autorizzazione **unsafe** all'account di accesso. Prima di eseguire l'istruzione CREATE ASSEMBLY, è necessario eseguire le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguenti.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Per specificare che un assembly viene caricato con l'autorizzazione **unsafe** , è necessario specificare il set di autorizzazioni **unsafe** durante il caricamento dell'assembly nel server:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Per ulteriori informazioni sulle autorizzazioni per ognuna delle impostazioni, vedere sicurezza dell' [integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli assembly di integrazione CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Modifica di un Assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Eliminazione di un Assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [Sicurezza dall'accesso di codice per l'integrazione con CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Proprietà di database TRUSTWORTHY](../../../relational-databases/security/trustworthy-database-property.md)   
 [Accettazione di chiamanti parzialmente attendibili](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
