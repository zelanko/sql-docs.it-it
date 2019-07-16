---
title: Comando SQL UPDATE - | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0230329d10d2414724379d4b9d38c4851a031bca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912329"
---
# <a name="update---sql-command"></a>UPDATE (comando SQL)
Aggiorna i record in una tabella con i nuovi valori.  
  
 Il Driver ODBC Visual FoxPro supporta la sintassi del linguaggio Visual FoxPro nativa per questo comando. Per informazioni specifiche del driver, vedere **osservazioni Driver**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>Argomenti  
 AGGIORNAMENTO [ *DatabaseName1!* ] *TableName1*  
 Specifica la tabella in cui vengono aggiornati i record con nuovi valori.  
  
 *DatabaseName1!* Specifica il nome di un database diverso da quello specificato con l'origine dati contenente la tabella. È necessario includere il nome del database contenente la tabella se il database non è quello corrente. Includere il delimitatore punto esclamativo (!) dopo il nome del database e prima del nome di tabella.  
  
 IMPOSTARE *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 Specifica le colonne che vengono aggiornate e i relativi nuovi valori. Se si omette la clausola WHERE, ogni riga nella colonna viene aggiornata con lo stesso valore.  
  
 In cui *FilterCondition1*[AND &#124; oppure *FilterCondition2*...]  
 Specifica i record che vengono aggiornati con nuovi valori.  
  
 *FilterCondition* specifica i criteri che i record devono soddisfare per essere aggiornati con nuovi valori. È possibile includere le condizioni di filtro nel modo desiderato, che li connettono con l'operatore AND o l'operatore OR. È anche possibile usare l'operatore NOT per invertire il valore di un'espressione logica oppure è possibile usare **vuoto**() per verificare la presenza di un campo vuoto.  
  
## <a name="remarks"></a>Note  
 UPDATE - SQL può aggiornare solo i record in un'unica tabella.  
  
 A differenza di sostituire, UPDATE - SQL Usa blocco dei record durante l'aggiornamento di più record nelle tabelle aperto per l'accesso condiviso. Questo riduce la contesa dei record in situazioni multiutente ma può ridurre le prestazioni. Per ottenere prestazioni ottimali, aprire la tabella per esclusivo usare oppure usare **BRANCO**() per bloccare la tabella.  
  
## <a name="driver-remarks"></a>Sezione Osservazioni di driver  
 Quando l'applicazione invia l'istruzione ODBC SQL UPDATE nell'origine dati, il Driver ODBC Visual FoxPro converte il comando al comando FoxProUPDATE Visual senza conversione.  
  
## <a name="see-also"></a>Vedere anche  
 [DELETE - comando SQL](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT (comando SQL)](../../odbc/microsoft/insert-sql-command.md)
