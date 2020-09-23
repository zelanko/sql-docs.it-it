---
title: Creazione di un driver OLE DB per applicazione SQL Server | Microsoft Docs
description: Informazioni sui passaggi necessari per creare un'applicazione OLE DB Driver per SQL Server e per trovare risorse aggiuntive.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49a9f20904c5719960cbffc7ca94c825def7231c
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862331"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>Creazione di un'applicazione del driver OLE DB per SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La creazione di un'applicazione OLE DB Driver per SQL Server prevede questi passaggi:  
  
1.  Avvio di una connessione a un'origine dati.  
  
2.  Esecuzione di un comando.  
  
3.  Elaborazione dei risultati.  
  
> [!NOTE]  
>  Se possibile, usare l'autenticazione di Windows. Se non è disponibile, agli utenti verrà richiesto di immettere le credenziali in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando [CryptoAPI Win32](https://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Avvio di una connessione a un'origine dati](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [Esecuzione di un comando](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [Elaborazione dei risultati](../../oledb/ole-db-driver/processing-results.md)  
  
-   [Informazioni sulle proprietà OLE DB](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [Uso della clausola OUTPUT con OLE DB nel driver OLE DB per SQL Server](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per programmazione con SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
