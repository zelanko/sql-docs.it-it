---
title: INSERT - comando SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44e773248cd2d61e211f6de98d5a0f81acc78bd1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471176"
---
# <a name="insert---sql-command"></a>INSERT (comando SQL)
Accoda un record alla fine di una tabella che contiene i valori di campo specificato.  
  
 Il Driver ODBC Visual FoxPro supporta la sintassi del linguaggio Visual FoxPro nativa per questo comando. Per informazioni specifiche del driver, vedere la sezione Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>Argomenti  
 INSERT INTO *dbf_name*  
 Specifica il nome della tabella a cui viene aggiunto il nuovo record. *dbf_name* può includere un percorso e può essere un'espressione di nome.  
  
 Se la tabella specificata non è aperta, aprirlo esclusivamente in una nuova area di lavoro e il nuovo record viene aggiunto alla tabella. La nuova area di lavoro non è selezionata; l'area di lavoro corrente rimanga selezionata.  
  
 Se la tabella specificata è aperta, l'istruzione INSERT Accoda il nuovo record alla tabella. Se la tabella è aperta in un'area di lavoro diverso da area di lavoro corrente, non è selezionato dopo che il record è stato aggiunto; l'area di lavoro corrente rimanga selezionata.  
  
 [( *fname1*[, *fname2*[, ...]])]  
 Specifica i nomi dei campi nel nuovo record in cui vengono inseriti i valori.  
  
 VALUES ( *eExpression1*[, *eExpression2*[, ...]])  
 Specifica i valori di campo inseriti un nuovo record. Se si omette i nomi dei campi, è necessario specificare i valori dei campi nell'ordine definito dalla struttura di tabella.  
  
## <a name="remarks"></a>Note  
 Il nuovo record contiene i dati elencati nella clausola VALUES.  
  
## <a name="driver-remarks"></a>Sezione Osservazioni di driver  
 Quando l'applicazione invia l'istruzione ODBC SQL INSERT per l'origine dati, il Driver ODBC Visual FoxPro converte il comando al comando FoxProINSERT Visual senza conversione.  
  
## <a name="see-also"></a>Vedere anche  
 [Crea tabella - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT (comando SQL)](../../odbc/microsoft/select-sql-command.md)
