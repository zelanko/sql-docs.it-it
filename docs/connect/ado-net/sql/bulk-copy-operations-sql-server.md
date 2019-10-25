---
title: Operazioni di copia bulk in SQL Server
description: Viene descritta la funzionalità di copia bulk per il provider di dati .NET per SQL Server.
ms.date: 09/30/2019
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 70eed483eb7cb857e23b110b7149badff14ab46f
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452298"
---
# <a name="bulk-copy-operations-in-sql-server"></a>Operazioni di copia bulk in SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server include una popolare utilità della riga di comando denominata **bcp** per eseguire rapidamente la copia bulk di file di grandi dimensioni in tabelle o viste nei database di SQL Server. La classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> consente di scrivere soluzioni di codice gestito che forniscono funzionalità simili. Esistono altri modi per caricare dati in una tabella di SQL Server (ad esempio, istruzioni INSERT) ma <xref:Microsoft.Data.SqlClient.SqlBulkCopy> offre un significativo vantaggio in termini di prestazioni.  
  
Utilizzando la classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, è possibile eseguire le operazioni seguenti:  
  
- Una singola operazione di copia bulk  
  
- Più operazioni di copia bulk  
  
- Un'operazione di copia bulk all'interno di una transazione  
  
> [!NOTE]
>  Con .NET Framework versione 1.1 o precedenti (in cui non è supportata la classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>), è possibile eseguire l'istruzione **BULK INSERT** di SQL Server Transact-SQL usando l'oggetto <xref:Microsoft.Data.SqlClient.SqlCommand>.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Installazione di esempio della copia bulk](bulk-copy-example-setup.md)  
Descrive le tabelle utilizzate negli esempi di copia bulk e fornisce script SQL per la creazione delle tabelle nel database AdventureWorks.  
  
[Singole operazioni di copia bulk](single-bulk-copy-operations.md)  
Viene descritto come eseguire una singola copia bulk dei dati in un'istanza di SQL Server utilizzando la classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy> e come eseguire l'operazione di copia bulk utilizzando istruzioni Transact-SQL e la classe <xref:Microsoft.Data.SqlClient.SqlCommand>.  
  
[Più operazioni di copia bulk](multiple-bulk-copy-operations.md)  
Viene descritto come eseguire più operazioni di copia bulk dei dati in un'istanza di SQL Server utilizzando la classe <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
[Transazioni e operazioni di copia bulk](transaction-bulk-copy-operations.md)  
Viene descritto come eseguire un'operazione di copia bulk all'interno di una transazione, inclusa la modalità di commit o rollback della transazione.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
