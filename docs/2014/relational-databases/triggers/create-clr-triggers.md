---
title: Creare trigger CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- CRL triggers
- DML triggers, CLR triggers
- DDL triggers, CLR triggers
ms.assetid: 31f41703-134d-49fc-9850-76c297351c2c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b68531b962b10785927c6212b2483f2d9c1d7d3a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62698824"
---
# <a name="create-clr-triggers"></a>Creazione di trigger CLR
  È possibile creare un oggetto di database all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programmato in un assembly creato in Common Language Runtime (CLR) di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Tra gli oggetti di database che consentono l'utilizzo del ricco modello di programmazione offerto da CLR vi sono trigger DML, trigger DDL, stored procedure, funzioni, funzioni di aggregazione e tipi.  
  
 Per creare un trigger CLR (DML o DDL) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , eseguire le operazioni seguenti:  
  
-   Definire il trigger come una classe in un linguaggio supportato da .NET Framework. Per altre informazioni sulla programmazione di trigger in CLR, vedere [Trigger CLR](../../database-engine/dev-guide/clr-triggers.md). Compilare quindi la classe per ottenere un assembly in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] utilizzando il compilatore appropriato.  
  
-   Per registrare l'assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizzare l'istruzione CREATE ASSEMBLY. Per altre informazioni sugli assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Assembly &#40;Motore di database&#41;](../clr-integration/assemblies-database-engine.md).  
  
-   Creare il trigger che fa riferimento all'assembly registrato.  
  
> [!NOTE]  
>  Con la distribuzione di un progetto SQL Server in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] viene registrato un assembly nel database specificato per il progetto. La distribuzione del progetto crea inoltre trigger CLR nel database per tutti i metodi annotati con l'attributo `SqlTrigger`. Per altre informazioni, vedere [Distribuzione di oggetti di database CLR](../clr-integration/deploying-clr-database-objects.md).  
  
> [!NOTE]  
>  Per impostazione predefinita, l'esecuzione di codice CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disattivata. È possibile creare, modificare ed eliminare oggetti di database che fanno riferimento a moduli di codice gestito. Tali riferimenti non verranno tuttavia eseguiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a meno che non si attivi [l'opzione clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) usando [sp_configure (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql).  
  
 **Per creare, modificare o eliminare un assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-assembly-transact-sql)  
  
 **Per creare un trigger CLR**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger DML](dml-triggers.md)   
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](../clr-integration/common-language-runtime-clr-integration-programming-concepts.md)   
 [Accesso ai dati da oggetti di database CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
