---
title: Creazione di un assieme Documenti Microsoft
description: Utilizzare CREATE ASSEMBLY per registrare un assembly in SQL Server e specificarne le impostazioni di sicurezza. Registrare un assembly per utilizzarne la funzionalità.
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
ms.openlocfilehash: 6ca6787abae22722a7bbb99d335e63d47051bb46
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486835"
---
# <a name="creating-an-assembly"></a>Creazione di un assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gli oggetti di database gestiti, ad esempio le stored procedure o i trigger, vengono compilati e quindi distribuiti in unità denominate assembly. Gli assembly DLL gestiti devono essere registrati prima [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di poter utilizzare la funzionalità fornita dall'assembly. Per registrare l'assembly in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], utilizzare l'istruzione CREATE ASSEMBLY. In questo argomento viene descritto come registrare un assembly in un database tramite l'istruzione CREATE ASSEMBLY e specificare le impostazioni di sicurezza per l'assembly.  
  
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
 Quando si crea [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] un assembly in un database, è possibile specificare uno dei tre diversi livelli di sicurezza in cui eseguire il codice: **SAFE**, **EXTERNAL_ACCESS**o **UNSAFE**. Quando viene eseguita l'istruzione **CREATE ASSEMBLY,** vengono eseguiti alcuni controlli sull'assembly del codice che possono causare la mancata registrazione dell'assembly sul server. Per ulteriori informazioni, vedere l'esempio Impersonation su [CodePlex](https://msftengprodsamples.codeplex.com/).  
  
 **SAFE** è il set di autorizzazioni predefinito e funziona per la maggior parte degli scenari. Per specificare un determinato livello di sicurezza, è necessario modificare la sintassi dell'istruzione CREATE ASSEMBLY come indicato di seguito:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 È anche possibile creare un assembly con il set di autorizzazioni **SAFE** semplicemente omettendo la terza riga di codice precedente:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Quando il codice in un assembly viene eseguito con il set di autorizzazioni **SAFE,** può eseguire il calcolo e l'accesso ai dati all'interno del server solo tramite il provider gestito in-process.  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>Creazione di assembly EXTERNAL_ACCESS e UNSAFE  
 **EXTERNAL_ACCESS** vengono illustrati gli scenari in cui il codice deve accedere alle risorse esterne al server, ad esempio file, rete, Registro di sistema e variabili di ambiente. Ogni volta che il server accede a una risorsa esterna, rappresenta il contesto di sicurezza dell'utente che chiama il codice gestito.  
  
 L'autorizzazione per il codice **UNSAFE** è per le situazioni in cui un assembly non [!INCLUDE[msCoName](../../../includes/msconame-md.md)] è sicuro per verificalmente o richiede un accesso aggiuntivo alle risorse limitate, ad esempio l'API Win32.  
  
 Per creare **EXTERNAL_ACCESS** un assembly EXTERNAL_ACCESS [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]o **UNSAFE** in , è necessario che venga soddisfatta una delle due condizioni seguenti:  
  
1.  L'assembly è firmato con nome sicuro o dispone di firma Authenticode con un certificato. Questo nome sicuro (o certificato) viene creato all'interno come chiave asimmetrica (o certificato) e dispone di un account di accesso corrispondente con l'autorizzazione **EXTERNAL ACCESS ASSEMBLY** (per gli assembly di accesso esterno) o l'autorizzazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **ASSEMBLY UNSAFE** (per gli assembly non sicuri).  
  
2.  Il proprietario del database (DBO) dispone dell'autorizzazione **EXTERNAL ACCESS ASSEMBLY** (per gli assembly EXTERNAL **ACCESS)** o **UNSAFE ASSEMBLY** (per gli assembly **UNSAFE)** e il database ha la [proprietà trustWORTHY del database](../../../relational-databases/security/trustworthy-database-property.md) impostata su **ON**.  

 Le due condizioni elencate in precedenza vengono verificate in fase di caricamento dell'assembly (fase che include l'esecuzione). Per caricare l'assembly, è necessario che si verifichi almeno una delle due condizioni.  
  
 È consigliabile che la [proprietà trustWORTHY](../../../relational-databases/security/trustworthy-database-property.md) del database in un database non sia impostata su **ON** solo per eseguire codice CLR (Common Language Runtime) nel processo server. È invece consigliabile creare una chiave asimmetrica dal file di assembly nel database master. È quindi necessario creare un account di accesso mappato a questa chiave asimmetrica e all'account di accesso deve essere concessa l'autorizzazione **EXTERNAL ACCESS ASSEMBLY** o **UNSAFE ASSEMBLY.**  
  
 Le [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzioni seguenti eseguono i passaggi necessari per creare una chiave asimmetrica, eseguire il mapping di un account di accesso a questa chiave e quindi concedere **EXTERNAL_ACCESS'autorizzazione** all'account di accesso. Prima di eseguire l'istruzione CREATE ASSEMBLY, è necessario eseguire le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguenti.  
  
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
  
 Per creare un assembly **EXTERNAL ACCESS,** il creatore deve disporre dell'autorizzazione **EXTERNAL ACCESS.** Questa autorizzazione viene specificata durante la creazione dell'assembly:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 Le [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzioni seguenti eseguono i passaggi necessari per creare una chiave asimmetrica, eseguire il mapping di un account di accesso a questa chiave e quindi concedere l'autorizzazione **UNSAFE** all'account di accesso. Prima di eseguire l'istruzione CREATE ASSEMBLY, è necessario eseguire le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] seguenti.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Per specificare che un assembly viene caricato con l'autorizzazione **UNSAFE,** specificare il set di autorizzazioni **UNSAFE** durante il caricamento dell'assembly nel server:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Per ulteriori informazioni sulle autorizzazioni per ognuna delle impostazioni, vedere [Sicurezza dell'integrazione CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli assembly di integrazione CLRManaging CLR Integration Assemblies](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Modifica di un assieme](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Eliminazione di un assieme](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [Sicurezza dall'accesso di codice dell'integrazione CLRCLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Proprietà di database TRUSTWORTHY](../../../relational-databases/security/trustworthy-database-property.md)   
 [Accettazione di chiamanti parzialmente attendibili](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
