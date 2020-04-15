---
title: Supporto di SQL Server Native Client per LocalDB Documenti Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b5114d0c12fe66b564c0e02ffb951b1ae0be809e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303252"
---
# <a name="sql-server-native-client-support-for-localdb"></a>Supporto SQL Server Native Client per il database locale
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
