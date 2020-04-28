---
title: Tipi di cursore | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4782c61c2f150e36c9632d09170468229c238cbb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305477"
---
# <a name="cursor-types"></a>Tipi di cursore
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC definisce quattro tipi di cursore supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal driver ODBC di Native Client. Questi cursori variano in base alla capacità di rilevare le modifiche apportate al set di risultati e alle risorse utilizzate, ad esempio la memoria e lo spazio in **tempdb**. Tramite un cursore è possibile rilevare le modifiche apportate alle righe solo quando viene eseguito un secondo tentativo di recupero di tali righe. L'origine dei dati non è in grado di notificare al cursore le eventuali modifiche apportate alle righe in fase di recupero. La capacità di rilevamento delle modifiche non effettuate di un cursore inoltre varia in base al livello di isolamento delle transazioni.  
  
 Di seguito sono indicati i quattro cursori ODBC supportati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   I cursori forward only non supportano lo scorrimento, ma solo le operazioni di recupero seriale delle righe dall'inizio alla fine del cursore.  
  
-   I cursori statici vengono compilati in **tempdb** all'apertura del cursore. Un cursore statico visualizza sempre il set di risultati così come è visualizzato all'apertura del cursore. Non riflettono mai modifiche ai dati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono sempre di sola lettura. Poiché un cursore del server statico viene compilato come una tabella di lavoro in **tempdb**, le dimensioni del set di risultati del cursore non possono superare le dimensioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]massime della riga consentite da.  
  
-   L'appartenenza e l'ordine delle righe di un cursore gestito da keyset vengono fissati al momento dell'apertura del cursore. Eventuali modifiche alle colonne non chiave sono visibili tramite il cursore.  
  
-   I cursori dinamici sono l'opposto dei cursori statici. Essi riflettono tutte le modifiche apportate alle righe del set di risultati corrispondente. I valori di dati, l'ordine e l'appartenenza delle righe del set di risultati possono variare a ogni operazione di recupero.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;&#41;ODBC](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
