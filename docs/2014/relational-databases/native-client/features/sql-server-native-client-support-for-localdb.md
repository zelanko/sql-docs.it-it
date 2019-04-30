---
title: SQL Server Native Client Support for LocalDB | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a3f5a8214c2966b1958c3a4ea08edbee5af6a2d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225480"
---
# <a name="sql-server-native-client-support-for-localdb"></a>Supporto SQL Server Native Client per il database locale
  A partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], sarà disponibile una versione lightweight di SQL Server, chiamato Database locale. In questo argomento viene discussa la modalità di connessione a un database in un'istanza del database locale.  
  
## <a name="remarks"></a>Note  
 Per ulteriori informazioni sul database locale inclusa la modalità di installazione del database locale e di configurazione della relativa istanza, vedere:  
  
-   [Riferimento al database locale di SQL Server Express](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express Local DB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 Riepilogando, il database locale consente di:  
  
-   utilizzare `sqllocaldb.exe i` per rilevare il nome dell'istanza predefinita.  
  
-   utilizzare la parola chiave della stringa di connessione `AttachDBFilename` per specificare a quale file di database il server si deve collegare. Quando si usa `AttachDBFilename`, se non si specifica il nome del database con il **Database** parola chiave di stringa di connessione, il database verrà rimosso dall'istanza di LocalDB alla chiusura dell'applicazione.  
  
-   Specificare un'istanza del database locale nella stringa di connessione:  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 Se necessario, è possibile creare un'istanza del database locale con sqllocaldb.exe. È possibile utilizzare anche sqlcmd.exe per aggiungere e modificare i database in un'istanza del database locale. Ad esempio `sqlcmd -S (localdb)\v11.0`.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
  
