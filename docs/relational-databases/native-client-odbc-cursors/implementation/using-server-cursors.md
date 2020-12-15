---
description: Utilizzo dei cursori del server
title: Utilizzo di cursori server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6585a9ac0805ec3b730b66bbba8b3694c34133a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438631"
---
# <a name="using-server-cursors"></a>Utilizzo dei cursori del server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Se un'applicazione ODBC imposta uno qualsiasi degli attributi del cursore ODBC su un valore diverso da quello predefinito, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client richiede al server di implementare un cursore API del server dello stesso tipo. L'utilizzo di cursori API del server libera memoria sul client e può ridurre in modo significativo il traffico di rete tra il client e il server.  
  
 Uno dei possibili svantaggi dei cursori API del server è attualmente il mancato supporto di tutte le istruzioni SQL. I cursori API del server non possono essere utilizzati per eseguire:  
  
-   Batch o stored procedure che restituiscono più set di risultati.  
  
-   Istruzioni SELECT che contengono la clausola COMPUTE, COMPUTE BY, FOR BROWSE o INTO.  
  
-   Istruzioni EXECUTE che fanno riferimento a una stored procedure remota.  
  
 In caso di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'esecuzione di un'istruzione con queste caratteristiche attraverso un cursore del server causa la conversione del cursore in un set di risultati predefinito. In caso di connessione a versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], causa un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di implementazione dei cursori](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
