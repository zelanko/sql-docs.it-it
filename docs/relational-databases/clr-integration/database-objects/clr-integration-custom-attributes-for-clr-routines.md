---
title: Attributi personalizzati per routine CLR | Microsoft Docs
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
ms.openlocfilehash: f1ff346abc41ee4589a8d0b2193b167fb2cf24e0
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212382"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Attributi personalizzati di integrazione con CLR per routine CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Gli attributi elencati possono essere applicati alle routine Common Language Runtime (CLR), ai tipi definiti dall'utente e alle aggregazioni definite dall'utente registrate in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se l'attributo non viene applicato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assume il valore predefinito. Gli attributi elencati sono definiti nello spazio dei nomi **Microsoft. SqlServer. Server** .  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Attributo SqlUserDefinedAggregate  
 L'attributo **SqlUserDefinedAggregate** indica che il metodo deve essere registrato come aggregazione definita dall'utente. Ogni aggregazione definita dall'utente deve essere annotata con questo attributo.  
  
 Per ulteriori informazioni, vedere [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Attributo SqlFunction  
 L'attributo **SqlFunction** indica che il metodo deve essere registrato come funzione con gli attributi di funzione appropriati impostati.  
  
 Per ulteriori informazioni, vedere [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Attributo SqlFacet  
 L'attributo **SqlFacet** viene utilizzato per restituire informazioni sul tipo restituito di un'espressione di tipo definito dall'utente (UDT).  
  
 Per ulteriori informazioni, vedere [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Attributo SqlProcedure  
 L'attributo **SqlProcedure** indica che il metodo deve essere registrato come stored procedure. Questo attributo viene utilizzato solo da Visual Studio per registrare automaticamente il metodo specificato come stored procedure. Non viene utilizzato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Per ulteriori informazioni, vedere [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Attributo SqlTrigger  
 L'attributo **SqlTrigger** indica che il metodo deve essere registrato come trigger.  
  
 Per ulteriori informazioni, vedere [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) e [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Attributo SqlUserDefinedTypeAttribute  
 È possibile applicare l'attributo SqlUserDefinedTypeAttribute a una definizione di classe nell'assembly. In questo caso, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene creato un tipo definito dall'utente associato alla definizione di classe che include l'attributo personalizzato.  
  
 Per ulteriori informazioni, vedere [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Attributo SqlMethod  
 L'attributo **SqlMethod** viene usato per indicare il determinismo e le proprietà di accesso ai dati di un metodo o di una proprietà in un tipo definito dall'utente.  
  
 Per ulteriori informazioni, vedere [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Vedere anche  
 Funzioni [di aggregazione CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funzioni CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipi CLR definiti dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Stored procedure CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
