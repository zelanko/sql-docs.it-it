---
title: Tipi di cursore | Documenti di Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 437b2d21e6441c3c6f6d94291d3f25d8546ddec4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134075"
---
# <a name="cursor-types"></a>Tipi di cursore
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC definisce quattro tipi di cursore supportati da Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client. I cursori si differenziano in relazione alla capacità di rilevare le modifiche al set di risultati e nelle risorse che utilizzano, ad esempio la memoria e lo spazio **tempdb**. Tramite un cursore è possibile rilevare le modifiche apportate alle righe solo quando viene eseguito un secondo tentativo di recupero di tali righe. L'origine dei dati non è in grado di notificare al cursore le eventuali modifiche apportate alle righe in fase di recupero. La capacità di rilevamento delle modifiche non effettuate di un cursore inoltre varia in base al livello di isolamento delle transazioni.  
  
 Di seguito sono indicati i quattro cursori ODBC supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   I cursori forward only non supportano lo scorrimento, ma solo le operazioni di recupero seriale delle righe dall'inizio alla fine del cursore.  
  
-   I cursori statici vengono compilati **tempdb** quando il cursore è aperto. Un cursore statico visualizza sempre il set di risultati così come è visualizzato all'apertura del cursore. Non riflettono mai modifiche ai dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono sempre di sola lettura. Poiché un cursore server statico viene compilato come una tabella di lavoro in **tempdb**, le dimensioni del set di risultati del cursore non possono superare le dimensioni di riga massime consentite dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   L'appartenenza e l'ordine delle righe di un cursore gestito da keyset vengono fissati al momento dell'apertura del cursore. Eventuali modifiche alle colonne non chiave sono visibili tramite il cursore.  
  
-   I cursori dinamici sono l'opposto dei cursori statici. Essi riflettono tutte le modifiche apportate alle righe del set di risultati corrispondente. I valori di dati, l'ordine e l'appartenenza delle righe del set di risultati possono variare a ogni operazione di recupero.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
