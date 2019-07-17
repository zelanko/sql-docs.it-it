---
title: SQLXML non è installato in SQL Server | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2adac1703facccda712db1e3f5826f784c0be141
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135318"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>Installazione di SQLXML non inclusa in SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Prima di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 veniva rilasciato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e faceva parte dell'installazione predefinita di tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la versione più recente di SQLXML (SQLXML 4.0 SP1) non è più inclusa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per installare SQLXML 4.0 SP1, scaricarlo dal [Install Location for SQLXML 4.0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Se un'applicazione viene eseguita su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiesto SQLXML 4.0, è necessario scaricare e installare SQLXML 4.0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamento di SQLXML 4.0 SP1 con i nuovi tipi di dati quando si utilizzano il provider OLE DB di SQL Server Native Client e SQLOLEDB  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introdotti i seguenti tipi di dati, quali gli sviluppatori che usano SQLXML potrebbero voler usare:  
  
-   **Data**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Quando si utilizza SQLXML 4.0 SP1 con SQLOLEDB entrambi oppure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB Native Client da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], questi tipi vengono visualizzati come stringhe a uno sviluppatore. SQLXML 4.0 SP1 vengono abilitati i quattro nuovi tipi di dati come tipi scalari predefiniti quando usato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Provider Native Client OLE DB 11.0 e versioni successive. Se non si scarica SQLXML 4.0 SP1, l'esecuzione del mapping di questi tipi ai tipi non stringa può causare il troncamento dei dati. Ad esempio, il mapping **DateTime2** a **xsd: date** determinerà dati troncati per la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** precisione di 3,33 millisecondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
