---
title: Conversione di dati dei parametri con valori di tabella e altri errori e avvisi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), data conversion
- table-valued parameters (ODBC), error messages
ms.assetid: edd45234-59dc-4338-94fc-330e820cc248
author: rothja
ms.author: jroth
ms.openlocfilehash: 45b9ba7f91b54548e096bbe47da6e01ba562f59d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999066"
---
# <a name="table-valued-parameter-data-conversion-and-other-errors-and-warnings"></a>Conversione di dati dei parametri con valori di tabella e altri errori e avvisi
  I valori delle colonne dei parametri con valori di tabella possono essere convertiti tra tipi di dati client e server in modo analogo agli altri valori di colonna e di parametro. Poiché un parametro con valori di tabella può contenere più colonne e più righe, è importante poter identificare il valore effettivo in cui si è verificato l'errore.  
  
 Quando viene rilevato un errore o un avviso in una colonna dei parametri con valori di tabella, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client genera un record di diagnostica. Il messaggio di errore conterrà il numero del parametro con valori di tabella, oltre al numero ordinale di colonna e al numero di riga. Un'applicazione può utilizzare anche i campi di diagnostica SQL_DIAG_SS_TABLE_COLUMN_NUMBER e SQL_DIAG_SS_TABLE_ROW_NUMBER all'interno dei record di diagnostica per determinare i valori che vengono associati agli errori e agli avvisi. Questi campi di diagnostica sono disponibili in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive.  
  
 L'identificativo di errore SQLSTATE e il messaggio dei record di diagnostica saranno conformi al comportamento esistente di ODBC in tutti gli altri aspetti, Ovvero, ad eccezione delle informazioni di identificazione di parametri, righe e colonne, i messaggi di errore hanno gli stessi valori per i parametri con valori di tabella come per i parametri non con valori di tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri con valori di tabella &#40;&#41;ODBC](table-valued-parameters-odbc.md)  
  
  
