---
title: Oggetti di database di compilazione CLR (Common Language Runtime)
description: Compilare oggetti di database utilizzando l'integrazione di SQL Server con il Common Language Runtime di .NET Framework (CLR).
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- database objects [CLR integration], building
- common language runtime [SQL Server], building database objects
- managed code [SQL Server], database objects
- building database objects [CLR integration]
- .NET Framework routines [SQL Server]
ms.assetid: ce34132c-bfa3-447b-9131-b6e17c672efe
author: rothja
ms.author: jroth
ms.openlocfilehash: 902685dcf1f8c743453285820faa67bb70830614
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75258348"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>Compilazione di oggetti di database con l'integrazione con CLR (Common Language Runtime)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  È possibile compilare oggetti di database utilizzando l'integrazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con CLR (Common Language Runtime) di .NET Framework. Il codice gestito in esecuzione all' [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] interno di viene definito "routine CLR". Queste routine includono gli elementi seguenti:  
  
-   Funzioni definite dall'utente con valori scalari  
  
-   Funzioni definite dall'utente con valori di tabella  
  
-   Procedure definite dall'utente  
  
-   Trigger definiti dall'utente  
  
 Le routine CLR hanno la stessa struttura in codice gestito. Viene eseguito il mapping di tali routine a metodi pubblici e statici (condivisi in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET) di una classe. Oltre alle routine, è possibile definire tipi definiti dall'utente e funzioni di aggregazione definite dall'utente utilizzando .NET Framework. Viene eseguito il mapping dei tipi definiti dall'utente (UDT) e delle aggregazioni definite dall'utente a intere classi di .NET Framework.  
  
 Ogni tipo di routine .NET Framework include una dichiarazione [!INCLUDE[tsql](../../../includes/tsql-md.md)] e può essere utilizzato in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ovunque sia possibile utilizzare l'equivalente [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Le funzioni scalari definite dall'utente, ad esempio, possono essere utilizzate in qualsiasi espressione scalare. Una funzione con valori di tabella può essere utilizzata in qualsiasi clausola FROM. Una procedura può essere richiamata in un'istruzione EXEC o da un'applicazione client.  
  
> [!NOTE]  
>  L'esecuzione di un oggetto CLR (funzione definita dall'utente, tipo definito dall'utente o trigger) sul Common Language Runtime può avvenire su più thread (piano parallelo), se il Query Optimizer decide che è vantaggioso. Tuttavia, se una funzione definita dall'utente accede ai dati, l'esecuzione sarà su un piano seriale. Anche in caso di esecuzione in una versione server precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e se in una funzione definita dall'utente sono contenuti parametri LOB o valori restituiti, l'esecuzione deve essere su un piano seriale.  
  
 Nella tabella seguente sono elencati gli argomenti inclusi in questa sezione.  
  
 [Introduzione all'integrazione con CLR](../../../relational-databases/clr-integration/database-objects/getting-started-with-clr-integration.md)  
 Include una breve panoramica delle librerie e degli spazi dei nomi necessari per compilare l'oggetto utilizzando l'integrazione con CLR con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È inclusa una stored procedure CLR "Hello World" di esempio.  
  
 [Librerie .NET Framework supportate](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)  
 Include informazioni sulle librerie .NET Framework supportate dall'integrazione CLR.  
  
 [Restrizioni relative al modello di programmazione dell'integrazione con CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)  
 Include informazioni sulle restrizioni del modello di programmazione dell'integrazione CLR.  
  
 [Tipi di dati di SQL Server in .NET Framework](../../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 Panoramica dei tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e degli equivalenti di .NET Framework.  
  
 [Panoramica degli attributi personalizzati dell'integrazione con CLR](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)  
 Include informazioni sugli attributi personalizzati dell'integrazione CLR.  
  
 [Funzioni CLR definite dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 Viene descritto come implementare e utilizzare i diversi tipi di funzioni CLR, ovvero le funzioni con valori di tabella, le funzioni scalari e le funzioni di aggregazione definite dall'utente.  
  
 [Tipi CLR definiti dall'utente](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Viene descritto come implementare e utilizzare i tipi CLR definiti dall'utente.  
  
 [Stored procedure CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)  
 Viene descritto come implementare e utilizzare le stored procedure CLR.  
  
 [Trigger CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
 Viene descritto come implementare e utilizzare i trigger CLR.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dell'integrazione di Common Language Runtime &#40;CLR&#41;](../../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)  
  
  
