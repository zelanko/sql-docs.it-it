---
title: AGGIORNAMENTO - Comando SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818811c18ed52cef5bdb1c4d97f947bb86e67422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307642"
---
# <a name="update---sql-command"></a>UPDATE (comando SQL)
Aggiorna i record in una tabella con nuovi valori.  
  
 Il driver ODBC di Visual FoxPro supporta la sintassi nativa del linguaggio Visual FoxPro per questo comando. Per informazioni specifiche del driver, vedere **Osservazioni del driver**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argomenti  
 AGGIORNAMENTO [ *NomeDatabase1!*] *NomeTabella1*  
 Specifica la tabella in cui i record vengono aggiornati con nuovi valori.  
  
 *NomeDatabase1!* specifica il nome di un database diverso da quello specificato con l'origine dati contenente la tabella. È necessario includere il nome del database contenente la tabella se il database non è quello corrente. Includere il delimitatore punto esclamativo (!) dopo il nome del database e prima del nome della tabella.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Specifica le colonne aggiornate e i nuovi valori. Se si oma la clausola WHERE, ogni riga della colonna viene aggiornata con lo stesso valore.  
  
 WHERE *FilterCondition1*[E &#124; OPPURE *FilterCondition2*...]  
 Specifica i record che vengono aggiornati con nuovi valori.  
  
 *FilterCondition* specifica i criteri che i record devono soddisfare per essere aggiornati con nuovi valori. È possibile includere tutte le condizioni di filtro desiderate, collegandole con l'operatore AND o OR. È inoltre possibile utilizzare l'operatore NOT per invertire il valore di un'espressione logica oppure **EMPTY**( ) per verificare la presenza di un campo vuoto.  
  
## <a name="remarks"></a>Osservazioni  
 AGGIORNAMENTO: SQL può aggiornare solo i record in una singola tabella.  
  
 A differenza di REPLACE, UPDATE: SQL utilizza il blocco dei record durante l'aggiornamento di più record nelle tabelle aperte per l'accesso condiviso. In questo modo si riduce la contesa dei record in situazioni multiutente, ma è possibile ridurre le prestazioni. Per ottenere le massime prestazioni, aprire la tabella per l'utilizzo esclusivo o utilizzare **FLOCK**( ) per bloccare la tabella.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Quando l'applicazione invia l'istruzione SQL ODBC UPDATE all'origine dati, il driver ODBC di Visual FoxPro converte il comando nel comando di Visual FoxProUPDATE senza conversione.  
  
## <a name="see-also"></a>Vedere anche  
 [DELETE - Comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT (comando SQL)](../../odbc/microsoft/insert-sql-command.md)
