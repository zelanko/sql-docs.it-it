---
title: Installazione di SQLXML non inclusa in SQL Server
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
ms.openlocfilehash: c666d02449190ca6a88ac43c96ab7aee9676be4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75242650"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>Installazione di SQLXML non inclusa in SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Prima di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 veniva rilasciato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e faceva parte dell'installazione predefinita di tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la versione più recente di SQLXML (SQLXML 4.0 SP1) non è più inclusa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per installare SQLXML 4,0 SP1, scaricarlo dal [percorso di installazione per sqlxml 4,0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Se un'applicazione viene eseguita [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in e richiede SQLXML 4,0, è necessario scaricare e installare SQLXML 4,0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamento di SQLXML 4.0 SP1 con i nuovi tipi di dati quando si utilizzano il provider OLE DB di SQL Server Native Client e SQLOLEDB  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]in sono stati introdotti i tipi di dati seguenti, che possono essere utilizzati dagli sviluppatori che utilizzano SQLXML:  
  
-   **Data**  
  
-   **Tempo**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Quando si utilizza SQLXML 4,0 SP1 con SQLOLEDB o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client OLE DB da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], questi tipi vengono visualizzati come stringhe per uno sviluppatore. In SQLXML 4,0 SP1 questi quattro nuovi tipi di dati vengono abilitati come tipi scalari predefiniti se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzati con Native client OLE DB provider 11,0 o versione successiva. Se non si scarica SQLXML 4.0 SP1, l'esecuzione del mapping di questi tipi ai tipi non stringa può causare il troncamento dei dati. Ad esempio, il mapping di **datetime2** a **xsd: date** provocherà il [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] troncamento dei dati alla precisione **DateTime** di 3,33 millisecondi.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
