---
title: Creare funzioni CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CLR functions [SQL Server]
- user-defined functions [SQL Server], CLR
ms.assetid: a82df075-2243-4e19-bfe1-ae6d65dabd0f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1a15690eb5aff48ec0f72df16e8342ed5c0522c9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370813"
---
# <a name="create-clr-functions"></a>Creare funzioni CLR
  È possibile creare un oggetto di database all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programmata in un assembly creato in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR). Gli oggetti di database in grado di sfruttare il ricco modello di programmazione fornito da CLR includono funzioni di aggregazione, funzioni, stored procedure, trigger e tipi.  
  
 La creazione di una funzione CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prevede i seguenti passaggi:  
  
-   Definire la funzione come metodo Static di una classe in un linguaggio supportato da [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Per altre informazioni sulla programmazione di funzioni in CLR, vedere [Funzioni CLR definite dall'utente](../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md). Quindi, compilare la classe per compilare un assembly in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzando il compilatore per il linguaggio appropriato.  
  
-   Registrare l'assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'istruzione CREATE ASSEMBLY. Per altre informazioni sugli assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Assembly &#40;Motore di database&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Creare la funzione che fa riferimento all'assembly registrato usando l'istruzione [CREATE FUNCTION](/sql/t-sql/statements/create-function-transact-sql) .  
  
> [!NOTE]  
>  Con la distribuzione di un progetto SQL Server in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] viene registrato un assembly nel database specificato per il progetto. La distribuzione del progetto consente inoltre di creare funzioni CLR nel database per tutti i metodi annotati con l'attributo `SqlFunction`. Per altre informazioni, vedere [Distribuzione di oggetti di database CLR](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  Per impostazione predefinita, l'esecuzione di codice CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disattivata. È possibile creare, modificare ed eliminare oggetti di database che fanno riferimento a moduli di codice gestito, ma tali riferimenti non verranno eseguiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a meno che non si abiliti l'opzione [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) usando [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
## <a name="accessing-external-resources"></a>Accesso a risorse esterne  
 Le funzioni CLR possono essere utilizzate per accedere a risorse esterne, ad esempio file, risorse di rete, servizi Web o altri database, comprese istanze remote di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A questo scopo è possibile utilizzare varie classi di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], ad esempio `System.IO`, `System.WebServices`, `System.Sql`e così via. L'assembly che contiene tali funzioni deve essere configurato almeno con l'autorizzazione EXTERNAL_ACCESS impostata a questo scopo. Per altre informazioni, vedere [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql). È possibile utilizzare il provider gestito SQL Client per accedere a istanze remote di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia nelle funzioni CLR le connessioni loopback al server di origine non sono supportate.  
  
 **Per creare, modificare o eliminare assembly in SQL Server**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Per creare una funzione CLR**  
  
-   [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
## <a name="accessing-native-code"></a>Accesso al codice nativo  
 Le funzioni CLR possono essere usate per accedere al codice nativo (non gestito), ad esempio codice scritto in C o C++, tramite l'uso di PInvoke da codice gestito. Per informazioni dettagliate, vedere [Chiamata a funzioni native da codice gestito](https://go.microsoft.com/fwlink/?LinkID=181929) . In questo modo è possibile riutilizzare codice legacy, quali funzioni CLR definite dall'utente, o scrivere funzioni definite dall'utente critiche per le prestazioni in codice nativo. Tale operazione richiede l'utilizzo di un assembly UNSAFE. Vedere [Sicurezza dall'accesso di codice dell'integrazione con CLR](../clr-integration/security/clr-integration-code-access-security.md) per le cautele da prendere per l'uso di assembly UNSAFE.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare funzioni definite dall'utente &#40;Motore di database&#41;](create-user-defined-functions-database-engine.md)   
 [Creazione di funzioni di aggregazione definite dall'utente](create-user-defined-aggregates.md)   
 [Eseguire funzioni definite dall'utente](execute-user-defined-functions.md)   
 [Visualizzare le funzioni definite dall'utente](view-user-defined-functions.md)   
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
