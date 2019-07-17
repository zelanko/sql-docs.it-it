---
title: Gli attributi personalizzati per routine CLR | Microsoft Docs
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
ms.openlocfilehash: 1c1105579dc5da82a66fb101e559e1fb96feac1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138627"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>Attributi personalizzati di integrazione con CLR per routine CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gli attributi elencati è applicabile per le routine di common language runtime (CLR), tipi definiti dall'utente e aggregazioni definite dall'utente registrati nel [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se l'attributo non viene applicato, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assume il valore predefinito. Gli attributi elencati vengono definiti nel **SQLServer** dello spazio dei nomi.  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>Attributo SqlUserDefinedAggregate  
 Il **SqlUserDefinedAggregate** attributo indica che il metodo deve essere registrato come aggregazione definita dall'utente. Ogni aggregazione definita dall'utente deve essere annotata con questo attributo.  
  
 Per altre informazioni, vedere [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="the-sqlfunction-attribute"></a>Attributo SqlFunction  
 Il **SqlFunction** attributo indica il metodo deve essere registrato come una funzione, con il set di attributi di funzione appropriata.  
  
 Per altre informazioni, vedere [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019).  
  
## <a name="the-sqlfacet-attribute"></a>Attributo SqlFacet  
 Il **SqlFacet** attributo viene utilizzato per restituire le informazioni sul tipo restituito di un'espressione di tipo definito dall'utente (UDT).  
  
 Per altre informazioni, vedere [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020).  
  
## <a name="the-sqlprocedure-attribute"></a>Attributo SqlProcedure  
 Il **SqlProcedure** attributo indica il metodo deve essere registrato come stored procedure. Questo attributo viene utilizzato solo da Visual Studio per registrare automaticamente il metodo specificato come stored procedure. Non viene utilizzato da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Per altre informazioni, vedere [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021).  
  
## <a name="the-sqltrigger-attribute"></a>Attributo SqlTrigger  
 Il **SqlTrigger** attributo indica il metodo deve essere registrato come trigger.  
  
 Per altre informazioni, vedere [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022) e [SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898).  
  
## <a name="the-sqluserdefinedtypeattribute"></a>Attributo SqlUserDefinedTypeAttribute  
 È possibile applicare l'attributo SqlUserDefinedTypeAttribute a una definizione di classe nell'assembly. In questo caso, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene creato un tipo definito dall'utente associato alla definizione di classe che include l'attributo personalizzato.  
  
 Per altre informazioni, vedere [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024).  
  
## <a name="the-sqlmethod-attribute"></a>Attributo SqlMethod  
 Il **SqlMethod** attributo viene utilizzato per indicare le proprietà di accesso di determinismo e i dati di un metodo o una proprietà in un tipo definito dall'utente.  
  
 Per altre informazioni, vedere [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggregazioni CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [Funzioni CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [Tipi CLR definiti dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Stored procedure CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [Trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
