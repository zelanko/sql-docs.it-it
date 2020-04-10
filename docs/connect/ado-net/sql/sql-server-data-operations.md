---
title: Operazioni sui dati di SQL Server in ADO.NET
description: Viene descritto come usare i dati in SQL Server. Contiene sezioni sulle operazioni di copia bulk, MARS, le operazioni asincrone e i parametri con valori di tabella.
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f6e842b38291fb704828b9b5a70d0652cfda51e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920985"
---
# <a name="sql-server-data-operations-in-adonet"></a>Operazioni sui dati di SQL Server in ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

In questa sezione vengono descritte le funzionalità di SQL Server specifiche del provider di dati Microsoft SqlClient per SQL Server (<xref:Microsoft.Data.SqlClient>).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Operazioni di copia bulk in SQL Server](bulk-copy-operations-sql-server.md)  
Viene descritta la funzionalità di copia bulk per il provider di dati .NET per SQL Server.  
  
[MARS (Multiple Active Result Sets)](multiple-active-result-sets-mars.md)  
Viene descritto come avere più di un'istanza di <xref:Microsoft.Data.SqlClient.SqlDataReader> aperta su una connessione quando ogni istanza di <xref:Microsoft.Data.SqlClient.SqlDataReader> viene avviata da un comando separato.  
  
[Operazioni asincrone](asynchronous-operations.md)  
Viene descritto come eseguire operazioni di database asincrone usando un'API basata sul modello asincrono usato da .NET Framework.  
  
[Parametri con valori di tabella](table-valued-parameters.md)  
Viene descritto come usare i parametri con valori di tabella introdotti in SQL Server 2008.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
