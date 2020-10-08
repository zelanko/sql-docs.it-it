---
title: Attributi personalizzati per routine CLR | Microsoft Docs
description: Gli attributi personalizzati possono essere applicati a routine CLR, tipi definiti dall'utente e aggregazioni definite dall'utente registrate in Microsoft SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: bad209c4ddb516167b8048ae73680bc9ea59cc05
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810807"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Attributi personalizzati di integrazione con CLR per routine CLR
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Gli attributi elencati possono essere applicati alle routine Common Language Runtime (CLR), ai tipi definiti dall'utente e alle aggregazioni definite dall'utente registrate in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se l'attributo non viene applicato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assume il valore predefinito. Gli attributi elencati sono definiti nello spazio dei nomi **Microsoft. SqlServer. Server** .  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Attributo SqlUserDefinedAggregate  
 L'attributo **SqlUserDefinedAggregate** indica che il metodo deve essere registrato come aggregazione definita dall'utente. Ogni aggregazione definita dall'utente deve essere annotata con questo attributo.  
  
 Per ulteriori informazioni, vedere [SqlUserDefinedAggregateAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedaggregateattribute).  
  
## <a name="the-sqlfunction-attribute"></a>Attributo SqlFunction  
 L'attributo **SqlFunction** indica che il metodo deve essere registrato come funzione con gli attributi di funzione appropriati impostati.  
  
 Per ulteriori informazioni, vedere [SqlFunctionAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfunctionattribute).  
  
## <a name="the-sqlfacet-attribute"></a>Attributo SqlFacet  
 L'attributo **SqlFacet** viene utilizzato per restituire informazioni sul tipo restituito di un'espressione di tipo definito dall'utente (UDT).  
  
 Per ulteriori informazioni, vedere [SqlFacetAttribute](/dotnet/api/microsoft.sqlserver.server.sqlfacetattribute).  
  
## <a name="the-sqlprocedure-attribute"></a>Attributo SqlProcedure  
 L'attributo **SqlProcedure** indica che il metodo deve essere registrato come stored procedure. Questo attributo viene utilizzato solo da Visual Studio per registrare automaticamente il metodo specificato come stored procedure. Non viene utilizzato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Per ulteriori informazioni, vedere [SqlProcedureAttribute](/dotnet/api/microsoft.sqlserver.server.sqlprocedureattribute).  
  
## <a name="the-sqltrigger-attribute"></a>Attributo SqlTrigger  
 L'attributo **SqlTrigger** indica che il metodo deve essere registrato come trigger.  
  
 Per ulteriori informazioni, vedere [SqlTriggerContext](/dotnet/api/microsoft.sqlserver.server.sqltriggercontext) e [SqlTriggerAttribute](/dotnet/api/microsoft.sqlserver.server.sqltriggerattribute).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Attributo SqlUserDefinedTypeAttribute  
 È possibile applicare l'attributo SqlUserDefinedTypeAttribute a una definizione di classe nell'assembly. In questo caso, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene creato un tipo definito dall'utente associato alla definizione di classe che include l'attributo personalizzato.  
  
 Per ulteriori informazioni, vedere [SqlUserDefinedTypeAttribute](/dotnet/api/microsoft.sqlserver.server.sqluserdefinedtypeattribute).  
  
## <a name="the-sqlmethod-attribute"></a>Attributo SqlMethod  
 L'attributo **SqlMethod** viene usato per indicare il determinismo e le proprietà di accesso ai dati di un metodo o di una proprietà in un tipo definito dall'utente.  
  
 Per ulteriori informazioni, vedere [SqlMethodAttribute](/dotnet/api/microsoft.sqlserver.server.sqlmethodattribute).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di aggregazione CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funzioni CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipi CLR definiti dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Stored procedure CLR](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [Trigger CLR](/dotnet/framework/data/adonet/sql/clr-triggers)  
  
