---
title: DELETE - Comando SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9757fd57d999815964266c035963de1129eaf5e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303552"
---
# <a name="delete---sql-command"></a>DELETE (comando SQL)
Contrassegna i record per l'eliminazione.  
  
 Il driver ODBC di Visual FoxPro supporta la sintassi nativa del linguaggio Visual FoxPro per questo comando. Per informazioni specifiche del driver, vedere la pagina Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>Argomenti  
 FROM [ *NomeDatabase!*] *NomeTabella*  
 Specifica la tabella in cui i record sono contrassegnati per l'eliminazione.  
  
 *Databasename!* specifica il nome di un database che contiene la tabella se il database che lo contiene non è il database specificato con l'origine dati. È necessario includere il nome di un database che contiene la tabella se il database non è il database specificato con l'origine dati. Includere il delimitatore punto esclamativo (!) dopo il nome del database e prima del nome della tabella.  
  
 WHERE *FilterCondition1*[E &#124; OPPURE *FilterCondition2*...]  
 Specifica che Visual FoxPro contrassegna solo determinati record per l'eliminazione.  
  
 *FilterCondition* specifica i criteri che i record devono soddisfare per essere contrassegnati per l'eliminazione. È possibile includere tutte le condizioni di filtro desiderate, collegandole con l'operatore AND o OR. È inoltre possibile utilizzare l'operatore NOT per invertire il valore di un'espressione logica oppure **EMPTY**( ) per verificare la presenza di un campo vuoto.  
  
## <a name="remarks"></a>Osservazioni  
 Se SET DELETED è impostato su ON, i record contrassegnati per l'eliminazione vengono ignorati da tutti i comandi che includono un ambito.  
  
 DELETE: SQL utilizza il blocco dei record quando si contrassegnano più record per l'eliminazione nelle tabelle aperte per l'accesso condiviso. In questo modo si riduce la contesa dei record in situazioni multiutente, ma è possibile ridurre le prestazioni. Per ottenere le massime prestazioni, aprire la tabella per l'utilizzo esclusivo.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Quando l'applicazione invia l'istruzione SQL ODBC DELETE all'origine dati, il driver ODBC di Visual FoxPro converte il comando nel comando di Visual FoxPro DELETE senza conversione.  
  
## <a name="see-also"></a>Vedere anche  
 [SET DELETED (comando)](../../odbc/microsoft/set-deleted-command.md)
