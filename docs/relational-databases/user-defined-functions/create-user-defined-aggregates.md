---
title: Creare funzioni di aggregazione definite dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: c278b746-6323-4b32-b460-239915acc067
author: rothja
ms.author: jroth
ms.openlocfilehash: d66db5586f5f80f8f0e8954d041befbcd4c5eba4
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053633"
---
# <a name="create-user-defined-aggregates"></a>Creazione di funzioni di aggregazione definite dall'utente
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]
  È possibile creare un oggetto di database all'interno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programmato in un assembly CLR. Gli oggetti di database che possono sfruttare il complesso modello di programmazione fornito da CLR includono trigger, stored procedure, funzioni, funzioni di aggregazione e tipi.  
  
 Analogamente alle funzioni di aggregazione predefinite incluse in [!INCLUDE[tsql](../../includes/tsql-md.md)], le funzioni di aggregazione definite dall'utente eseguono un calcolo su un set di valori e restituiscono un unico valore.  
  
 Per creare una funzione di aggregazione definita dall'utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , eseguire le operazioni descritte di seguito:  
  
-   Impostare la funzione di aggregazione definita dall'utente come una classe utilizzando un linguaggio supportato in [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework. Per altre informazioni sulla programmazione di funzioni di aggregazione definite dall'utente in CLR, vedere [Aggregazioni CLR definite dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md). Compilare questa classe per compilare un assembly CLR utilizzando il compilatore di linguaggio appropriato.  
  
-   Per registrare l'assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizzare l'istruzione CREATE ASSEMBLY. Per altre informazioni sugli assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Assembly &#40;Motore di database&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md).  
  
-   Per creare la funzione di aggregazione definita dall'utente che fa riferimento all'assembly registrato, utilizzare l'istruzione CREATE AGGREGATE.  
  
> [!NOTE]
>  Con la distribuzione di un progetto SQL Server in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] viene registrato un assembly nel database specificato per il progetto. La distribuzione del progetto consente anche di creare una funzione di aggregazione definita dall'utente nel database per tutte le definizioni di classe annotate con l'attributo **SqlUserDefinedAggregate** . Per altre informazioni, vedere [Distribuzione di oggetti di database CLR](../../relational-databases/clr-integration/deploying-clr-database-objects.md).  
> 
> [!NOTE]
>  Per impostazione predefinita, l'esecuzione di codice CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disattivata. È possibile creare, modificare ed eliminare oggetti di database che fanno riferimento a moduli di codice gestito. Tali riferimenti non verranno tuttavia eseguiti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a meno che non si attivi l' [opzione clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) tramite [sp_configure (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 **Per creare, modificare o eliminare un assembly**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **Per creare una funzione di aggregazione definita dall'utente**  
  
-   [CREATE AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
