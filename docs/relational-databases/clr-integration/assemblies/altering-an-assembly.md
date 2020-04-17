---
title: Modifica di un assieme Documenti Microsoft
description: Utilizzare ALTER ASSEMBLY per aggiornare gli assembly registrati in SQL ServerSQL Server.Use ALTER ASSEMBLY to update assemblies registered in SQL ServerSQL Server. È inoltre possibile modificare il set di autorizzazioni e aggiungere codice sorgente o altri file per un assembly.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
author: rothja
ms.author: jroth
ms.openlocfilehash: 07fd94c855a81a8d58ac1ed4b578edf478dc77aa
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81486852"
---
# <a name="altering-an-assembly"></a>Modifica di un assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gli assembly registrati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possono essere aggiornati da una versione più recente utilizzando l'istruzione ALTER ASSEMBLY. Per aggiornare un assembly, utilizzare l'istruzione ALTER ASSEMBLY con la sintassi seguente:  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY non interrompe i processi in esecuzione che utilizzano l'assembly. L'esecuzione di tali processi continua con l'assembly non modificato. Non è possibile utilizzare ALTER ASSEMBLY per modificare le firme di funzioni, funzioni di aggregazione, stored procedure e trigger di CLR (Common Language Runtime). Nuovi metodi pubblici possono essere aggiunti all'assembly, i metodi privati possono essere modificati nel modo desiderato e i metodi pubblici possono essere modificati a condizione di non modificare le firme o gli attributi. Non è possibile modificare tramite ALTER ASSEMBLY i campi contenuti in un tipo definito dall'utente con serializzazione nativa, inclusi i membri dei dati o le classi base. Tutte le altre modifiche non sono supportate. Per ulteriori informazioni, vedere [ALTER ASSEMBLY &#40;Transact-SQLTransact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md).  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>Modifica del set di autorizzazioni di un assembly  
 Il set di autorizzazioni di un assembly può essere anch'esso modificato utilizzando l'istruzione ALTER ASSEMBLY. L'istruzione che segue modifica il set di autorizzazioni dell'assembly SQLCLRTest in **EXTERNAL_ACCESS**.  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 Se il set di autorizzazioni di un assembly viene modificato da **SAFE** a **EXTERNAL_ACCESS** o **UNSAFE**, è necessario innanzitutto creare una chiave asimmetrica e un account di accesso corrispondente con autorizzazione **EXTERNAL ACCESS ASSEMBLY** o **UNSAFE ASSEMBLY** per l'assembly. Per altre informazioni, vedere [Creating an Assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
## <a name="adding-the-source-code-of-an-assembly"></a>Aggiunta del codice sorgente di un assembly.  
 La clausola ADD FILE nella sintassi ALTER ASSEMBLY non è presente in CREATE ASSEMBLY. È possibile utilizzarla per aggiungere codice sorgente o altri file associati a un assembly. I file vengono copiati dai percorsi originali e vengono archiviati nelle tabelle di sistema del database. In questo modo il codice sorgente o gli altri file saranno sempre disponibili nel caso in cui sia necessario ricreare o documentare la versione corrente del tipo definito dall'utente (UDT).  
  
 L'istruzione seguente aggiunge il codice sorgente della classe Point.cs per il tipo definito dall'utente Point. Il testo contenuto nel file Point.cs viene copiato e archiviato nel database con il nome "PointSource".  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione degli assembly di integrazione CLRManaging CLR Integration Assemblies](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Creazione di un assieme](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Eliminazione di un assieme](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
