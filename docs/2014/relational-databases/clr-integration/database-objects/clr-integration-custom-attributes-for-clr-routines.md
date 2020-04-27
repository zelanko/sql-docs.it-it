---
title: Attributi personalizzati per routine CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 817591cec64a4210c4cc573588be1b8ac6dfb8a7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873801"
---
# <a name="custom-attributes-for-clr-routines"></a>Attributi personalizzati per routine CLR
  Gli attributi elencati possono essere applicati alle routine Common Language Runtime (CLR), ai tipi definiti dall'utente e alle aggregazioni definite dall'utente registrate in [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]. Se l'attributo non viene applicato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assume il valore predefinito. Gli attributi elencati vengono definiti nello spazio dei nomi `Microsoft.SqlServer.Server`.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Attributo SqlUserDefinedAggregate  
 L'attributo `SqlUserDefinedAggregate` indica che il metodo deve essere registrato come aggregazione definita dall'utente. Ogni aggregazione definita dall'utente deve essere annotata con questo attributo.  
  
 Per ulteriori informazioni, vedere [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Attributo SqlFunction  
 L'attributo `SqlFunction` indica che il metodo deve essere registrato come funzione, con il set di attributi delle funzioni appropriato.  
  
 Per ulteriori informazioni, vedere [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Attributo SqlFacet  
 L'attributo `SqlFacet` viene utilizzato per restituire informazioni sul tipo restituito di un'espressione di tipo definito dall'utente.  
  
 Per ulteriori informazioni, vedere [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Attributo SqlProcedure  
 L'attributo `SqlProcedure` indica che il metodo deve essere registrato come stored procedure. Questo attributo viene utilizzato solo da Visual Studio per registrare automaticamente il metodo specificato come stored procedure. Non viene utilizzato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Per ulteriori informazioni, vedere [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Attributo SqlTrigger  
 Tramite l'attributo `SqlTrigger` viene indicato che il metodo deve essere registrato come trigger.  
  
 Per ulteriori informazioni, vedere [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) e [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Attributo SqlUserDefinedTypeAttribute  
 È possibile applicare l'attributo SqlUserDefinedTypeAttribute a una definizione di classe nell'assembly. In questo caso, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene creato un tipo definito dall'utente associato alla definizione di classe che include l'attributo personalizzato.  
  
 Per ulteriori informazioni, vedere [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Attributo SqlMethod  
 L'attributo `SqlMethod` viene utilizzato per indicare le proprietà deterministiche e di accesso ai dati di un metodo o di una proprietà in un tipo definito dall'utente.  
  
 Per ulteriori informazioni, vedere [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Vedi anche  
 [Funzioni di aggregazione CLR definite dall'utente](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funzioni CLR definite dall'utente](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipi CLR definiti dall'utente](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Stored procedure CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)   
 [Trigger CLR](../../../database-engine/dev-guide/clr-triggers.md)  
  
  
