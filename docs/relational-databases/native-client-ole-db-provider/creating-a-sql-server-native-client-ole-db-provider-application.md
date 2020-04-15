---
title: App del provider OLE DB di SQL Native Client
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef8459fb3d906be6efca0e47d83418fb70bdebdb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289725"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>Creazione di un'applicazione del provider OLE DB di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creazione di un'applicazione provider OLE DB Native Client prevede la procedura seguente:Creating a Native Client OLE DB provider application involves these steps:  
  
1.  Avvio di una connessione a un'origine dati.  
  
2.  Esecuzione di un comando.  
  
3.  Elaborazione dei risultati.  

> [!NOTE]  
>  Se possibile, usare l'autenticazione di Windows. Se non è disponibile, agli utenti verrà richiesto di immettere le credenziali in fase di esecuzione. Evitare di archiviare le credenziali in un file. Se è necessario rendere persistenti le credenziali, è consigliabile crittografarle usando [CryptoAPI Win32](https://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Avvio di una connessione a un'origine dati](../../relational-databases/native-client-ole-db-provider/establishing-a-connection-to-a-data-source.md)  
  
-   [Esecuzione di un comando](../../relational-databases/native-client-ole-db-provider/executing-a-command.md)  
  
-   [Risultati dell'elaborazione](../../relational-databases/native-client-ole-db-provider/processing-results.md)  
  
-   [Informazioni sulle proprietà OLE DB](../../relational-databases/native-client-ole-db-provider/about-ole-db-properties.md)  
  
-   [Utilizzo della clausola OUTPUT con OLE DB in SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
