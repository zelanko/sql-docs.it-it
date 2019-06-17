---
title: Utilizzo di cursori Server | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7c49926705e0e2b7dc189ae46dda7b8ec2a9ff1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013963"
---
# <a name="using-server-cursors"></a>Utilizzo dei cursori del server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Se un'applicazione ODBC imposta uno degli attributi del cursore ODBC su un valore qualsiasi diverso da quelli predefiniti, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client richiede al server di implementare un cursore API del server dello stesso tipo. L'utilizzo di cursori API del server libera memoria sul client e può ridurre in modo significativo il traffico di rete tra il client e il server.  
  
 Uno dei possibili svantaggi dei cursori API del server è attualmente il mancato supporto di tutte le istruzioni SQL. I cursori API del server non possono essere utilizzati per eseguire:  
  
-   Batch o stored procedure che restituiscono più set di risultati.  
  
-   Istruzioni SELECT che contengono la clausola COMPUTE, COMPUTE BY, FOR BROWSE o INTO.  
  
-   Istruzioni EXECUTE che fanno riferimento a una stored procedure remota.  
  
 In caso di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'esecuzione di un'istruzione con queste caratteristiche attraverso un cursore del server causa la conversione del cursore in un set di risultati predefinito. In caso di connessione a versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], causa un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di implementazione dei cursori](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
