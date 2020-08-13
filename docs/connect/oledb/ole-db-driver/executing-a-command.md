---
title: Esecuzione di un comando (OLE DB Driver) | Microsoft Docs
description: Esecuzione di un comando
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5077f621e8a3698e5aec09b79f28a2f5cf9257e7
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244850"
---
# <a name="executing-a-command"></a>Esecuzione di un comando
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Una volta stabilita la connessione a un'origine dati, il consumer chiama il metodo **IDBCreateSession::CreateSession** per creare una sessione. La sessione funge da comando, set di righe o factory di transazioni.  
  
 Per lavorare direttamente con singoli indici o tabelle, il consumer richiede l'interfaccia **IOpenRowset**. Il metodo **IOpenRowset::OpenRowset** apre e restituisce un set di righe che include tutte le righe di un singolo indice o tabella di base.  
  
 Per eseguire un comando, ad esempio SELECT \* FROM Authors, il consumer richiede l'interfaccia **IDBCreateCommand**. Il consumer può eseguire il metodo **IDBCreateCommand::CreateCommand** per creare un oggetto comando e richiedere l'interfaccia **ICommandText**. Il metodo **ICommandText::SetCommandText** viene usato per specificare il comando da eseguire.  
  
 Per eseguire il comando viene usato il comando **Esegui**. Il comando può essere qualsiasi nome di istruzione o di procedura SQL. Non tutti i comandi producono un oggetto set di risultati (set di righe). Comandi come SELECT * FROM Authors producono un set di risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un driver OLE DB per applicazione SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
