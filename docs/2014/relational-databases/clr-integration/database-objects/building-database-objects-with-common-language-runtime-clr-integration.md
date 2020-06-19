---
title: Compilazione di oggetti di database con l'integrazione con CLR (Common Language Runtime) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: dd5717b545913bd9e5ee98debe670a1af616fc61
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953608"
---
# <a name="building-database-objects-with-common-language-runtime-clr-integration"></a>Compilazione di oggetti di database con l'integrazione con CLR (Common Language Runtime)
  È possibile creare oggetti di database utilizzando l'oggetto [!INCLUDE[ssNoVersion](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] definito "routine CLR". Queste routine includono gli elementi seguenti:  
  
-   Funzioni definite dall'utente con valori scalari  
  
-   Funzioni definite dall'utente con valori di tabella  
  
-   Procedure definite dall'utente  
  
-   Trigger definiti dall'utente  
  
 Le routine CLR hanno la stessa struttura in codice gestito. Viene eseguito il mapping di tali routine a metodi pubblici e statici (condivisi in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET) di una classe. Oltre alle routine, è possibile definire tipi definiti dall'utente e funzioni di aggregazione definite dall'utente utilizzando .NET Framework. Viene eseguito il mapping dei tipi definiti dall'utente (UDT) e delle aggregazioni definite dall'utente a intere classi di .NET Framework.  
  
 Ogni tipo di .NET Framework routine dispone di un oggetto [!INCLUDE[tsql](../../../includes/ssnoversion-md.md)] che [!INCLUDE[tsql](../../../includes/tsql-md.md)] può essere utilizzato dall'oggetto equivalente. Le funzioni scalari definite dall'utente, ad esempio, possono essere utilizzate in qualsiasi espressione scalare. Una funzione con valori di tabella può essere utilizzata in qualsiasi clausola FROM. Una procedura può essere richiamata in un'istruzione EXEC o da un'applicazione client.  
  
> [!NOTE]  
>  L'esecuzione di un oggetto CLR (funzione definita dall'utente, tipo definito dall'utente o trigger) sul Common Language Runtime può avvenire su più thread (piano parallelo), se il Query Optimizer decide che è vantaggioso. Tuttavia, se una funzione definita dall'utente accede ai dati, l'esecuzione sarà su un piano seriale. Anche in caso di esecuzione in una versione server precedente a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] e se in una funzione definita dall'utente sono contenuti parametri LOB o valori restituiti, l'esecuzione deve essere su un piano seriale.  
  
 Nella tabella seguente sono elencati gli argomenti inclusi in questa sezione.  
  
 [Introduzione all'integrazione con CLR](getting-started-with-clr-integration.md)  
 Include una breve panoramica delle librerie e degli spazi dei nomi necessari per compilare l'oggetto utilizzando l'integrazione con CLR con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. È inclusa una stored procedure CLR "Hello World" di esempio.  
  
 [Librerie .NET Framework supportate](supported-net-framework-libraries.md)  
 Include informazioni sulle librerie .NET Framework supportate dall'integrazione CLR.  
  
 [Restrizioni relative al modello di programmazione dell'integrazione con CLR](clr-integration-programming-model-restrictions.md)  
 Include informazioni sulle restrizioni del modello di programmazione dell'integrazione CLR.  
  
 [Tipi di dati di SQL Server in .NET Framework](../../clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
 Panoramica dei tipi di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e degli equivalenti di .NET Framework.  
  
 [Panoramica degli attributi personalizzati dell'integrazione con CLR](../../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)  
 Include informazioni sugli attributi personalizzati dell'integrazione CLR.  
  
 [Funzioni CLR definite dall'utente](../../clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)  
 Viene descritto come implementare e utilizzare i diversi tipi di funzioni CLR, ovvero le funzioni con valori di tabella, le funzioni scalari e le funzioni di aggregazione definite dall'utente.  
  
 [Tipi CLR definiti dall'utente](../../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
 Viene descritto come implementare e utilizzare i tipi CLR definiti dall'utente.  
  
 [Stored procedure CLR](../../../database-engine/dev-guide/clr-stored-procedures.md)  
 Viene descritto come implementare e utilizzare le stored procedure CLR.  
  
 [Trigger CLR](../../../database-engine/dev-guide/clr-triggers.md)  
 Viene descritto come implementare e utilizzare i trigger CLR.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica dell'integrazione di Common Language Runtime &#40;CLR&#41;](../common-language-runtime-integration-overview.md)  
  
  
