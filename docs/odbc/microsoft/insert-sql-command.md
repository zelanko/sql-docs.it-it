---
title: INSERT - Comando SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce00005fb1aa0ca9732fc5e9cfeacd6faf6ef9e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300007"
---
# <a name="insert---sql-command"></a>INSERT (comando SQL)
Aggiunge un record alla fine di una tabella che contiene i valori di campo specificati.  
  
 Il driver ODBC di Visual FoxPro supporta la sintassi nativa del linguaggio Visual FoxPro per questo comando. Per informazioni specifiche del driver, vedere la pagina Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argomenti  
 INSERT INTO *dbf_name*  
 Specifica il nome della tabella a cui viene aggiunto il nuovo record. *dbf_name* può includere un percorso e può essere un'espressione di nome.  
  
 Se la tabella specificata non è aperta, viene aperta esclusivamente in una nuova area di lavoro e il nuovo record viene aggiunto alla tabella. La nuova area di lavoro non è selezionata; l'area di lavoro corrente rimane selezionata.  
  
 Se la tabella specificata è aperta, INSERT aggiunge il nuovo record alla tabella. Se la tabella è aperta in un'area di lavoro diversa dall'area di lavoro corrente, non viene selezionata dopo l'aggiunta del record; l'area di lavoro corrente rimane selezionata.  
  
 [( *fname1*[, *fname2*[, ...]])]  
 Specifica nel nuovo record i nomi dei campi in cui vengono inseriti i valori.  
  
 VALORI ( *eExpression1*[, *eExpression2*[, ...]]  
 Specifica i valori dei campi inseriti nel nuovo record. Se si ostocano i nomi dei campi, è necessario specificare i valori dei campi nell'ordine definito dalla struttura della tabella.  
  
## <a name="remarks"></a>Osservazioni  
 Il nuovo record contiene i dati elencati nella clausola VALUES.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Quando l'applicazione invia l'istruzione SQL ODBC INSERT all'origine dati, il driver ODBC di Visual FoxPro converte il comando nel comando di Visual FoxProINSERT senza conversione.  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE TABLE - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT (comando SQL)](../../odbc/microsoft/select-sql-command.md)
