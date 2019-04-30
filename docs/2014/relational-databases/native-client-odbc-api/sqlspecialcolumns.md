---
title: SQLSpecialColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ea811151e9c81ed515b774f279297d236c608f5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188737"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
  Quando richiede gli identificatori di riga (*IdentifierType* SQL_BEST_ROWID), **SQLSpecialColumns** restituisce un set di risultati vuoto (nessuna riga di dati) per tutti gli ambiti diversi da SQL_SCOPE_CURROW richiesti. Il set di risultati generato indica che le colonne sono valide solo all'interno di questo ambito.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta pseudocolonne per gli identificatori. Il **SQLSpecialColumns** set di risultati identificherà tutte le colonne come SQL_PC_NOT_PSEUDO.  
  
 **SQLSpecialColumns** può essere eseguito su un cursore statico. Un tentativo di eseguire **SQLSpecialColumns** su un cursore aggiornabile (dinamico o gestito da keyset) restituirà SQL_SUCCESS_WITH_INFO che indica il tipo di cursore è stato modificato.  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>Supporto di SQLSpecialColumns per le caratteristiche avanzate di data e ora  
 Per informazioni sui valori restituiti per le colonne DATA_TYPE, TYPE_NAME, COLUMN_SIZE, BUFFER_LENGTH e DECIMAL_DIGTS per i tipi di data/ora, vedere [metadati del catalogo](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Per altre informazioni generali, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>Supporto di SQLSpecialColumns per tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLSpecialColumns** supporta grandi CLR tipi definiti dall'utente (UDT). Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLSpecialColumns](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
