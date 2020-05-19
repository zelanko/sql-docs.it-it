---
title: Utilizzo di cursori server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4e8bcae5ab64fff47528c30a67c13fd1c859ea4e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702034"
---
# <a name="using-server-cursors"></a>Utilizzo dei cursori del server
  Se un'applicazione ODBC imposta uno qualsiasi degli attributi del cursore ODBC su un valore diverso da quello predefinito, il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client richiede al server di implementare un cursore API del server dello stesso tipo. L'utilizzo di cursori API del server libera memoria sul client e può ridurre in modo significativo il traffico di rete tra il client e il server.  
  
 Uno dei possibili svantaggi dei cursori API del server è attualmente il mancato supporto di tutte le istruzioni SQL. I cursori API del server non possono essere utilizzati per eseguire:  
  
-   Batch o stored procedure che restituiscono più set di risultati.  
  
-   Istruzioni SELECT che contengono la clausola COMPUTE, COMPUTE BY, FOR BROWSE o INTO.  
  
-   Istruzioni EXECUTE che fanno riferimento a una stored procedure remota.  
  
 In caso di connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], l'esecuzione di un'istruzione con queste caratteristiche attraverso un cursore del server causa la conversione del cursore in un set di risultati predefinito. In caso di connessione a versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], causa un errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità di implementazione dei cursori](how-cursors-are-implemented.md)  
  
  
