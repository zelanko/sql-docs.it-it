---
title: Modifica di un Assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 780b64f59143d3bf2b8ef99e3da6d32a1fe160cc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874106"
---
# <a name="altering-an-assembly"></a>Modifica di un assembly
  Gli assembly registrati in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] possono essere aggiornati da una versione più recente utilizzando l'istruzione ALTER ASSEMBLY. Per aggiornare un assembly, utilizzare l'istruzione ALTER ASSEMBLY con la sintassi seguente:  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY non interrompe i processi in esecuzione che utilizzano l'assembly. L'esecuzione di tali processi continua con l'assembly non modificato. Non è possibile utilizzare ALTER ASSEMBLY per modificare le firme di funzioni, funzioni di aggregazione, stored procedure e trigger di CLR (Common Language Runtime). Nuovi metodi pubblici possono essere aggiunti all'assembly, i metodi privati possono essere modificati nel modo desiderato e i metodi pubblici possono essere modificati a condizione di non modificare le firme o gli attributi. Non è possibile modificare tramite ALTER ASSEMBLY i campi contenuti in un tipo definito dall'utente con serializzazione nativa, inclusi i membri dei dati o le classi base. Tutte le altre modifiche non sono supportate. Per altre informazioni, vedere [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>Modifica del set di autorizzazioni di un assembly  
 Il set di autorizzazioni di un assembly può essere anch'esso modificato utilizzando l'istruzione ALTER ASSEMBLY. Nell'istruzione seguente il set di autorizzazioni dell'assembly SQLCLRTest viene modificato in `EXTERNAL_ACCESS`.  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 Se il set di autorizzazioni di un assembly viene modificato da `SAFE` a `EXTERNAL_ACCESS` o `UNSAFE`, è innanzitutto necessario creare una chiave asimmetrica e un account di accesso corrispondente con autorizzazione `EXTERNAL ACCESS ASSEMBLY` o `UNSAFE ASSEMBLY` per l'assembly. Per altre informazioni, vedere [Creating an Assembly](creating-an-assembly.md).  
  
## <a name="adding-the-source-code-of-an-assembly"></a>Aggiunta del codice sorgente di un assembly.  
 La clausola ADD FILE nella sintassi ALTER ASSEMBLY non è presente in CREATE ASSEMBLY. È possibile utilizzarla per aggiungere codice sorgente o altri file associati a un assembly. I file vengono copiati dai percorsi originali e vengono archiviati nelle tabelle di sistema del database. In questo modo il codice sorgente o gli altri file saranno sempre disponibili nel caso in cui sia necessario ricreare o documentare la versione corrente del tipo definito dall'utente (UDT).  
  
 L'istruzione seguente aggiunge il codice sorgente della classe Point.cs per il tipo definito dall'utente Point. Il testo contenuto nel file Point.cs viene copiato e archiviato nel database con il nome "PointSource".  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>Vedere anche  
 [La gestione degli assembly dell'integrazione CLR](managing-clr-integration-assemblies.md)   
 [Creazione di un Assembly](creating-an-assembly.md)   
 [Eliminazione di un Assembly](dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
  
