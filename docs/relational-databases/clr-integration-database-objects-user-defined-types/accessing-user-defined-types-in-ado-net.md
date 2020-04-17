---
title: Accesso ai tipi definiti dall'utente in ADO.NET . Documenti Microsoft
description: I tipi definiti dall'utente, scritti nei linguaggi CLR di .NET Framework, consentono a un database di SQL Server di archiviare oggetti e strutture di dati personalizzate. In ADO.NET, un provider espone i tipi definiti dall'utente.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: d14205a6fb506f5d4fddaac1ab601ff1ee9205b8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488254"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Accesso ai tipi definiti dall'utente in ADO .NET
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  I tipi definiti dall'utente (UDT) vengono scritti [!INCLUDE[msCoName](../../includes/msconame-md.md)] utilizzando uno dei linguaggi supportati da Common Language Runtime (CLR) di .NET Framework che producono codice verificabile. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. I tipi definiti dall'utente consentono l'archiviazione di oggetti e strutture di dati personalizzate in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I dati vengono esposti come membri pubblici di una classe o struttura .NET mentre i comportamenti vengono definiti dai metodi della classe o della struttura. Un tipo definito dall'utente (UDT) può essere usato come definizione di colonna di una tabella, come variabile in un batch [!INCLUDE[tsql](../../includes/tsql-md.md)] o come argomento di una funzione [!INCLUDE[tsql](../../includes/tsql-md.md)] o di una stored procedure.  
  
 In ADO.NET, il provider **System.Data.SqlClient** espone i tipi definiti dall'utente nei modi seguenti:  
  
-   Tramite **System.Data.SqlClient.SqlDataReader** come oggetto.  
  
-   Tramite **il SqlDataReader** come byte non elaborati.  
  
-   Come parametro di un oggetto **System.Data.SqlClient.SqlParameter.**  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Recupero di dati UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-retrieving-udt-data.md)  
 Viene illustrato come recuperare i dati dei tipi definiti dall'utente e come specificare i parametri.  
  
 [Aggiornamento di colonne con tipo definito dall'utente con DataAdapter](../../relational-databases/clr-integration-database-objects-user-defined-types/accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Viene descritto come utilizzare i tipi definiti dall'utente nei **DataSet** e come aggiornare i dati del tipo definito dall'utente utilizzando **DataAdapter .**  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi CLR definiti dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)  
  
  
