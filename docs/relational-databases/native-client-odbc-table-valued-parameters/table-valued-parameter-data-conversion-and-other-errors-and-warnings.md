---
title: I dati dei parametri con valori di tabella di conversione e altri errori e avvisi | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 45c46e19126921c31120084a9d8e8a7a9a6c51ce
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518711"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversione di dati dei parametri con valori di tabella e altri errori e avvisi
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  I valori delle colonne dei parametri con valori di tabella possono essere convertiti tra tipi di dati client e server in modo analogo agli altri valori di colonna e di parametro. Poiché un parametro con valori di tabella può contenere più colonne e più righe, è importante poter identificare il valore effettivo in cui si è verificato l'errore.  
  
 Quando viene rilevato un errore o un avviso in una colonna dei parametri con valori di tabella, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera un record di diagnostica. Il messaggio di errore conterrà il numero del parametro con valori di tabella, oltre al numero ordinale di colonna e al numero di riga. Un'applicazione può utilizzare anche i campi di diagnostica SQL_DIAG_SS_TABLE_COLUMN_NUMBER e SQL_DIAG_SS_TABLE_ROW_NUMBER all'interno dei record di diagnostica per determinare i valori che vengono associati agli errori e agli avvisi. Questi campi di diagnostica sono disponibili in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive.  
  
 L'identificativo di errore SQLSTATE e il messaggio dei record di diagnostica saranno conformi al comportamento esistente di ODBC in tutti gli altri aspetti, Vale a dire, ad eccezione di parametro, righe e le informazioni di identificazione di colonna, i messaggi di errore hanno gli stessi valori per parametri con valori di tabella come avviene per i parametri di non-con valori di tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [I parametri con valori di tabella &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
