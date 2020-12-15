---
description: Connessione a un database SQL di Azure usando SQL Server Native Client
title: Connettersi al database SQL di Azure
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab4f4836d2d0979e6eed68a297f0d583dd612719
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462072"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>Connessione a un database SQL di Azure usando SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Per un esempio che illustra come connettersi a [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] utilizzando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client, vedere procedure [per lo sviluppo (database SQL di Azure)](/previous-versions/azure/ee621787(v=azure.100)).  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>Problemi noti correlati alla connessione a un database SQL  
 Di seguito sono elencati i problemi noti che si verificano durante la connessione a [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   Una connessione eseguita con **SQLBrowseConnect** può essere rifiutata se si utilizza **SQLBrowseConnect** in fasi.  Ad esempio, se il nome del driver viene inviato nella prima chiamata, il server e le credenziali (utente e password) inviati nella seconda chiamata, la connessione e l'impostazione di un linguaggio e di un nome di database hanno luogo nella terza chiamata.  Durante la terza chiamata [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client emetterà un'istruzione USE per modificare i database. Poiché l'istruzione USE non è supportata in [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], viene generato l'errore seguente:  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
