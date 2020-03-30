---
title: Uso di dati di grandi dimensioni | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 425beac7bcae36170ff378b59d36da05838df645
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028248"
---
# <a name="working-with-large-data"></a>Uso di dati di grandi dimensioni

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

Il driver JDBC fornisce supporto per la memorizzazione nel buffer adattiva, che consente di recuperare qualsiasi tipo di dati con valori di grandi dimensioni senza l'overhead dei cursori server. Grazie al buffering adattivo, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] può recuperare i risultati dell'esecuzione di istruzioni da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando questi sono necessari per l'applicazione e non tutti contemporaneamente. Quando l'applicazione non necessita più di accedere ai dati, questi vengono inoltre eliminati dal driver.  
  
In [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] JDBC Driver versione 1.2 la modalità di buffering predefinita era "**full**". Se l'applicazione non impostava la proprietà di connessione "responseBuffering" su "**adaptive**" nelle proprietà di connessione oppure tramite il metodo [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) dell'oggetto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md), il driver supportava la lettura dell'intero risultato dal server. Per ottenere il comportamento di buffering adattivo, l'applicazione doveva impostare esplicitamente la proprietà di connessione "responseBuffering" su "**adaptive**".  
  
il valore **adaptive** è la modalità di buffering predefinita e il driver JDBC memorizza nel buffer la quantità minima possibile di dati quando necessario. Per altre informazioni sull'uso del buffer adattivo, vedere [Uso del buffer adattivo](../../../connect/jdbc/using-adaptive-buffering.md).  
  
Gli argomenti in questa sezione descrivono vari modi per recuperare dati per valori di grandi dimensioni da un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
| Argomento                                                                                                                         | Descrizione                                                              |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [Esempio di lettura di dati di grandi dimensioni](../../../connect/jdbc/code-samples/reading-large-data-sample.md)                                               | Descrive come utilizzare un'istruzione SQL per recuperare dati per valori di grandi dimensioni.       |
| [Esempio di lettura di dati di grandi dimensioni con una stored procedure](../../../connect/jdbc/code-samples/reading-large-data-with-stored-procedures-sample.md) | Descrive come recuperare un valore del parametro OUT CallableStatement di grandi dimensioni. |
| [Esempio di aggiornamento di dati di grandi dimensioni](../../../connect/jdbc/code-samples/updating-large-data-sample.md)                                             | Descrive come aggiornare dati per valori di grandi dimensioni in un database.                |
  
## <a name="see-also"></a>Vedere anche

[Applicazioni di esempio del driver JDBC](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  
