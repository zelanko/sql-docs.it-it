---
title: Accesso ai tipi definiti dall'utente in ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 893b2c69a20974bb379cc032f442e5fcb3525ec5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62919678"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Accesso ai tipi definiti dall'utente in ADO .NET
  I tipi definiti dall'utente (UDT) vengono scritti utilizzando uno dei linguaggi supportati dalla [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) che producono codice verificabile. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. I tipi definiti dall'utente consentono l'archiviazione di oggetti e strutture di dati personalizzate in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I dati vengono esposti come membri pubblici di una classe o struttura .NET mentre i comportamenti vengono definiti dai metodi della classe o della struttura. Un tipo definito dall'utente (UDT) può essere usato come definizione di colonna di una tabella, come variabile in un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] o come argomento di una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] o di una stored procedure.  
  
 In ADO.NET il provider `System.Data.SqlClient` espone i tipi definiti dall'utente nei modi seguenti:  
  
-   Mediante `System.Data.SqlClient.SqlDataReader` come oggetto.  
  
-   Mediante `SqlDataReader` come byte non elaborati.  
  
-   Come parametro di un oggetto `System.Data.SqlClient.SqlParameter`.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Recupero di dati UDT](accessing-user-defined-types-retrieving-udt-data.md)  
 Viene illustrato come recuperare i dati dei tipi definiti dall'utente e come specificare i parametri.  
  
 [Aggiornamento di colonne con tipo definito dall'utente con DataAdapter](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Viene illustrato come utilizzare i tipi definiti dall'utente in `DataSets` e come aggiornarli utilizzando `DataAdapters`.  
  
## <a name="see-also"></a>Vedi anche  
 [Tipi CLR definiti dall'utente](clr-user-defined-types.md)  
  
  
