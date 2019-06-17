---
title: Tipi CLR definiti dall'utente | Documenti di Microsoft
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- validation [CLR integration]
- types [CLR integration]
- UserDefined serialization format [CLR integration]
- null values [CLR integration]
- serialization
- Native serialization format [CLR integration]
- databases [CLR integration]
- building database objects [CLR integration], user-defined types
- user-defined types [CLR integration]
- common language runtime [SQL Server], user-defined types
- UDTs [CLR integration]
- database objects [CLR integration], user-defined types
- turning on CLR functionality
- customizing UDT expression return types [CLR integration]
- UDTs [CLR integration], about UDTs
- comparing UDT values
- annotations [CLR integration]
- user-defined types [CLR integration], about UDTs
- variables [CLR integration]
- invoking UDT methods
- indexes [CLR integration]
ms.assetid: 27c4889b-c543-47a8-a630-ad06804f92df
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7044fdc4c29110870e20cd2f9fe4f2140659e551
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874442"
---
# <a name="clr-user-defined-types"></a>Tipi CLR definiti dall'utente
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di creare oggetti di database programmati in un assembly creato in Common Language Runtime (CLR) di .NET Framework. Tra gli oggetti di database che consentono l'utilizzo del ricco modello di programmazione offerto da CLR vi sono trigger, stored procedure, funzioni, funzioni di aggregazione e tipi.  
  
> [!NOTE]  
>  Per impostazione predefinita, l'esecuzione di codice CLR in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disattivata. CLR può essere abilitato usando il **sp_configure** stored procedure di sistema.  
  
 A partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], è possibile usare tipi definiti dall'utente (UDT) per estendere il sistema di tipo scalare del server, consentendo l'archiviazione di oggetti CLR in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. I tipi definiti dall'utente possono contenere più elementi e assumere vari comportamenti. Questo li differenzia dai tipi di dati alias tradizionali costituiti da un singolo tipo di dati di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Poiché il sistema accede ai tipi definiti dall'utente nella loro interezza, l'utilizzo che ne viene fatto per i tipi di dati complessi può influire negativamente sulle prestazioni. Il modo migliore per modellare i dati complessi in genere consiste nell'utilizzare righe e tabelle tradizionali. I tipi definiti dall'utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] risultano particolarmente adatti per:  
  
-   Data, ora, valuta e tipi numerici estesi  
  
-   Applicazioni Geospatial  
  
-   Dati codificati o crittografati  
  
 Il processo di sviluppo dei tipi definiti dall'utente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituito dai passaggi seguenti:  
  
1.  **Il codice e compilare l'assembly che definisce il tipo definito dall'utente.** I tipi definiti dall'utente vengono definiti utilizzando uno dei linguaggi supportati da CLR (Common Language Runtime) di .NET Framework che generano codice verificabile, tra cui, ad esempio, Microsoft Visual C# e Visual Basic .NET. I dati vengono esposti come campi e proprietà di una classe o una struttura .NET Framework mentre i comportamenti vengono definiti dai metodi della classe o della struttura.  
  
2.  **Registrare l'assembly.** I tipi definiti dall'utente possono essere distribuiti attraverso l'interfaccia utente di Visual Studio in un progetto di database o mediante l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY, che copia l'assembly contenente la classe o la struttura in un database.  
  
3.  **Creare il tipo definito dall'utente in SQL Server.** Dopo aver caricato un assembly in un database host, viene utilizzata l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE per creare un tipo definito dall'utente e vengono esposti i membri della classe o della struttura come membri del tipo in questione. I tipi definiti dall'utente esistono solo nel contesto di un singolo database e dopo la registrazione non hanno dipendenze sui file esterni da cui sono stati creati.  
  
    > [!NOTE]  
    >  Prima di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], i tipi definiti dall'utente creati dagli assembly di .NET Framework non erano supportati. Tuttavia, è comunque possibile usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati alias tramite **sp_addtype**. La sintassi CREATE TYPE può essere utilizzata per creare tipi di dati definiti dall'utente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativi e tipi definiti dall'utente.  
  
4.  **Creare tabelle, variabili o parametri mediante il tipo definito dall'utente** a partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], un tipo definito dall'utente può essere utilizzato come definizione di colonna di una tabella, come una variabile in un [!INCLUDE[tsql](../../includes/tsql-md.md)] batch, o come argomento di un [!INCLUDE[tsql](../../includes/tsql-md.md)] funzionare o archiviati procedura.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Creazione di un tipo definito dall'utente](creating-user-defined-types.md)  
 Viene illustrato come creare tipi definiti dall'utente.  
  
 [Registrazione dei tipi definiti dall'utente in SQL Server](registering-user-defined-types-in-sql-server.md)  
 Viene illustrato come registrare e gestire i tipi definiti dall'utente (UDT) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Uso di tipi definiti dall'utente in SQL Server](working-with-user-defined-types-in-sql-server.md)  
 Viene descritto come creare query mediante i tipi definiti dall'utente.  
  
 [Accesso ai tipi definiti dall'utente in ADO.NET](accessing-user-defined-types-in-ado-net.md)  
 Viene illustrato come utilizzare i tipi definiti dall'utente mediante il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in ADO.NET.  
  
  
