---
title: Scenari di utilizzo ed esempi per l'integrazione Common Language Runtime (CLR) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- scenarios [CLR integration]
- common language runtime [SQL Server], samples
- examples [CLR integration]
- sample applications [CLR integration]
- database objects [CLR integration], samples
- managed code [SQL Server], samples
ms.assetid: 33aac25f-abb4-4f29-af88-4a0dacd80ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3718a084211e7c3b2b7a14973e195a4b1c3b6b1a
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155018"
---
# <a name="usage-scenarios-and-examples-for-common-language-runtime-clr-integration"></a>Scenari di utilizzo ed esempi per l'integrazione con CLR (Common Language Runtime)
  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono inclusi applicazioni e pacchetti di esempio nonché diversi esempi di codice che consentono di acquisire familiarità con le funzionalità di programmabilità dell'integrazione con Common Language Runtime (CLR).  
  
 Per progetti di Visual Studio completi implementati questi esempi e materiali aggiuntivi, visitare [Microsoft SQL Server Community Projects & Samples in CodePlex](https://go.microsoft.com/fwlink/?LinkID=193935).  
  
|Nome|Descrizione|  
|----------|-----------------|  
|[Accesso al codice nativo da un funzione CLR definita dall'utente](../../../2014/database-engine/dev-guide/accessing-native-code-from-a-clr-udf.md)|Viene illustrato come richiamare una funzione in codice C++ nativo (non gestito) da una funzione definita dall'utente in un assembly, nel database.|  
|[Esempio Array Parameter](../../../2014/database-engine/dev-guide/array-parameter-sample.md)|Viene illustrato come creare, aggiornare o eliminare un set di righe in un database passando una matrice di informazioni da un client a una stored procedure per l'integrazione con CLR nel server. A tal scopo, viene utilizzato un tipo definito dall'utente (UDT).|  
|[Esempio di tipo definito dall'utente con supporto del calendario data e ora](../../../2014/database-engine/dev-guide/calendar-aware-date-and-time-udt-sample.md)|Vengono illustrati due tipi definiti dall'utente che consentono la gestione di data e ora con supporto del calendario.|  
|[Esempio CLR Transactions](../../../2014/database-engine/dev-guide/clr-transactions-sample.md)|Viene illustrato il controllo delle transazioni tramite le API gestite nello spazio dei nomi System.Transactions.|  
|[Creazione di informazioni di contatto con CLR e XML](../../../2014/database-engine/dev-guide/contact-creation-using-clr-and-xml.md)|L'esempio Contact per SQL Server offre interessanti utilità che costituiscono un ulteriore livello di funzionalità disponibile per il database di esempio AdventureWorks2012 di base. La prima utilità consente di creare record con informazioni di contatto per i diversi tipi di persone presenti nel database AdventureWorks2012. Le informazioni di contatto vengono specificate tramite XML e vengono passate a una stored procedure basata su C# o VB per creare il codice XML e inserirlo nelle tabelle appropriate con il database.|  
|[Tipo Currency e funzione di conversione](../../../2014/database-engine/dev-guide/currency-type-and-conversion-function.md)|Viene definito un tipo di dati Currency definito dall'utente mediante C#.|  
|[Gestione di oggetti di grandi dimensioni tramite CLR](../../../2014/database-engine/dev-guide/handling-large-objects-using-clr.md)|Viene illustrato il trasferimento di oggetti LOB tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un file system a cui può accedere il server mediante stored procedure CLR.|  
|[Esempio Hello World Ready](../../../2014/database-engine/dev-guide/hello-world-ready-sample.md)|Vengono illustrate le operazioni di base per la creazione, la distribuzione e il test di una stored procedure semplice internazionalizzata basata sull'integrazione con CLR.|  
|[Esempio Hello World](../../../2014/database-engine/dev-guide/hello-world-sample.md)|Vengono illustrate le operazioni di base per la creazione, la distribuzione e il test di una stored procedure semplice basata sull'integrazione con CLR.|  
|[Esempio In-Process Data Access](../../../2014/database-engine/dev-guide/in-process-data-access-sample.md)|Sono incluse diverse funzioni semplici che illustrano le varie funzionalità del provider di accesso ai dati in-process CLR.|  
|[Esempio Result Set](../../../2014/database-engine/dev-guide/result-set-sample.md)|Viene illustrato come eseguire comandi mentre si stanno leggendo i risultati di una query senza dover aprire una nuova connessione e senza dover leggere tutti i risultati in memoria.|  
|[Esempio Send DataSet](../../../2014/database-engine/dev-guide/send-dataset-sample.md)|Viene illustrato come restituire un oggetto DataSet basato su ADO.NET all'interno di una stored procedure basata su CLR sul lato server come set di risultati al client.|  
|[Esempio String Utility Functions](../../../2014/database-engine/dev-guide/string-utility-functions-sample.md)|È inclusa una funzione di flusso con valori di tabella, scritta in Visual C# e Visual Basic, che consente di suddividere una stringa delimitata da virgole in una tabella con una colonna.|  
|[Esempio di modifica di stringhe in grado di riconoscere caratteri supplementari](../../../2014/database-engine/dev-guide/supplementary-aware-string-manipulation-sample.md)|Viene illustrata l'implementazione di cinque funzioni per valori stringa [!INCLUDE[tsql](../../includes/tsql-md.md)] con supporto di caratteri supplementari in grado di gestire sia stringhe Unicode che stringhe surrogate.|  
|[UDT Utilities](../../../2014/database-engine/dev-guide/udt-utilities.md)|Sono incluse diverse serie di funzioni di utilità per tipi di dati definiti dall'utente.|  
|[Pulizia degli assembly inutilizzati](../../../2014/database-engine/dev-guide/unused-assembly-cleanup.md)|È inclusa una stored procedure .NET che consente di eliminare gli assembly inutilizzati nel database corrente tramite l'esecuzione di query sui cataloghi di metadati.|  
|[Tipo definito dall'utente](../../../2014/database-engine/dev-guide/user-defined-type.md)|Vengono illustrati la creazione e l'utilizzo di un tipo definito dall'utente (UDT) semplice sia con [!INCLUDE[tsql](../../includes/tsql-md.md)] che con un'applicazione client tramite System.Data.SqlClient.|  
|[UTF8 Tipo di dati definito dall'utente di stringhe &#40;tipo definito dall'utente&#41;](../../../2014/database-engine/dev-guide/utf8-string-user-defined-data-type-udt.md)|Viene illustrata l'implementazione di un tipo definito dall'utente (UDT) che consente di estendere il sistema di tipi del database per consentire l'archiviazione di valori con codifica UTF8.|  
  
  
