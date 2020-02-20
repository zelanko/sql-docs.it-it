---
title: Dati binari e di grandi dimensioni di SQL Server
description: Viene descritto come usare i tipi di dati con valori di grandi dimensioni in SQL Server.
ms.date: 08/15/2019
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e60f8ce6bc8e7ef05a2de942d8bbc2885095d493
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251120"
---
# <a name="sql-server-binary-and-large-value-data"></a>Dati binari e di grandi dimensioni di SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Scaricare ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server include l'identificatore `max`, che espande la capacità di archiviazione dei tipi di dati `varchar`, `nvarchar` e `varbinary`. I tipi `varchar(max)`, `nvarchar(max)` e `varbinary(max)` vengono collettivamente definiti *tipi di dati con valori di grandi dimensioni*. È possibile usare i tipi di dati per valori di grandi dimensioni per archiviare fino a 2^31-1 byte di dati.  
  
SQL Server 2008 introduce l'attributo FILESTREAM, che non è un tipo di dati, ma piuttosto un attributo che può essere definito per una colonna, consentendo l'archiviazione di dati con valori di grandi dimensioni nel file system invece che nel database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Modifica di dati con valori di grandi dimensioni (max) in ADO.NET](modify-large-value-max-data.md)  
Viene descritto come usare i tipi di dati con valori di grandi dimensioni.  
  
[Dati FILESTREAM](filestream-data.md)  
Viene descritto come usare dati con valori di grandi dimensioni archiviati in SQL Server 2008 con l'attributo FILESTREAM.  
  
## <a name="next-steps"></a>Passaggi successivi
- [Tipi di dati SQL Server e ADO.NET](sql-server-data-types.md)
- [Operazioni sui dati di SQL Server in ADO.NET](sql-server-data-operations.md)
