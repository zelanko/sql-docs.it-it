---
title: Driver OLE DB per il supporto SQL Server per LocalDB | Microsoft Docs
description: Informazioni su come connettersi a una versione lightweight di SQL Server, denominata LocalDB, usando OLE DB Driver per SQL Server.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c7f5ac94ff64ef32aaee793c59529ad0377b2f5
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860685"
---
# <a name="ole-db-driver-for-sql-server-support-for-localdb"></a>Supporto del driver OLE DB per SQL Server per Local DB
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], sarà disponibile una versione lightweight di SQL Server, chiamato Database locale. In questo argomento viene discussa la modalità di connessione a un database in un'istanza del database locale.  
  
## <a name="remarks"></a>Osservazioni  
 Per ulteriori informazioni sul database locale inclusa la modalità di installazione del database locale e di configurazione della relativa istanza, vedere:  
  
-   [Riferimento al database locale di SQL Server Express](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 Riepilogando, il database locale consente di:  
  
-   Usare **sqllocaldb.exe** per individuare il nome dell'istanza predefinita.  
  
-   Usare la parola chiave della stringa di connessione **AttachDBFilename** per specificare a quale file di database si deve collegare il server. Quando si usa **AttachDBFilename**, se non viene specificato il nome del database con la parola chiave della stringa di connessione **Database**, il database sarà rimosso dall'istanza di Local DB quando l'applicazione viene chiusa.  
  
-   Specificare un'istanza del database locale nella stringa di connessione:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Se necessario, è possibile creare un'istanza del database locale con sqllocaldb.exe. È possibile utilizzare anche sqlcmd.exe per aggiungere e modificare i database in un'istanza del database locale. Ad esempio, **sqlcmd -S (localdb)\v11.0**.  
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
