---
title: sp_cursoroption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a686f78ea5dff8a3ea551016d9fbe9c9046b110
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545496"
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta le opzioni del cursore o restituisce informazioni sul cursore create dalla routine sp_cursoropen archiviati. richiamare sp_cursoroption specificando ID = 8 in un pacchetto del flusso TDS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor*  
 È un *gestiscono* valore generato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e restituito dalla routine sp_cursoropen archiviati. *cursore* richiede un' **int** valore di input per l'esecuzione.  
  
 *codice*  
 Consente di specificare i vari fattori dei valori restituiti del cursore. *codice* richiede uno dei seguenti **int** valori di input:  
  
|Value|nome|Descrizione|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|Restituisce il puntatore di testo, anziché i dati effettivi, per determinate colonne di tipo text o image designate.<br /><br /> TEXTPTR_ONLY consente i puntatori di testo da utilizzare come *handle* agli oggetti blob che possono essere recuperati in seguito in modo selettivo o l'aggiornamento usando [!INCLUDE[tsql](../../includes/tsql-md.md)] o funzionalità DBLIB (ad esempio, [!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT o DBLIB DBWRITETEXT).<br /><br /> Se viene assegnato il valore "0", tutte le colonne di tipo text e image nell'elenco di selezione restituiranno puntatori di testo anziché dati.|  
|0x0002|CURSOR_NAME|Assegna il nome specificato nel *valore* fino al cursore. A sua volta, consente a ODBC di utilizzare [!INCLUDE[tsql](../../includes/tsql-md.md)] posizionate le istruzioni di aggiornamento ed eliminazione sui cursori aperti mediante sp_cursoropen.<br /><br /> La stringa può essere specificata come qualsiasi tipo di dati Unicode o character.<br /><br /> Poiché [!INCLUDE[tsql](../../includes/tsql-md.md)] le istruzioni UPDATE/DELETE posizionate operano, per impostazione predefinita, nella prima riga in un cursore con sp_cursor SETPOSITION deve essere usato per posizionare il cursore prima di eseguire l'istruzione UPDATE/DELETE posizionata.|  
|0x0003|TEXTDATA|Restituisce i dati effettivi, anziché il puntatore di testo, per determinate colonne di tipo text o image in recuperi successivi, ovvero annulla l'effetto di TEXTPTR_ONLY.<br /><br /> Se per una colonna specifica è abilitato TEXTDATA, la riga viene nuovamente recuperata o aggiornata e può quindi essere nuovamente impostata su TEXTPTR_ONLY. Analogamente a quanto accade per TEXTPTR_ONLY, il parametro di valore è un intero che specifica il numero di colonna e un valore zero restituisce tutte le colonne di tipo text o image.|  
|0x0004|SCROLLOPT|Opzione di scorrimento. Per ulteriori informazioni, vedere "Valori dei codici restituiti" più avanti in questo argomento.|  
|0x0005|CCOPT|Opzioni del controllo della concorrenza. Per ulteriori informazioni, vedere "Valori dei codici restituiti" più avanti in questo argomento.|  
|0x0006|ROWCOUNT|Numero di righe correntemente nel set di risultati.<br /><br /> Nota: È possibile che ROWCOUNT sia modificato rispetto al valore restituito da sp_cursoropen, se viene utilizzato il popolamento asincrono. Viene restituito il valore -1 se il numero di righe è sconosciuto.|  
  
 *Valore*  
 Definisce il valore restituito da *codice*. *valore* è un parametro obbligatorio che richiede un 0x0001, 0x0002 o 0x0003 *codice* valore di input.  
  
> [!NOTE]  
>  Oggetto *codice* valore 2 è un tipo di dati stringa. Qualsiasi altra *codice* valore di input o restituito da *valore* è un numero intero.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Il *valore* possono restituire uno dei seguenti parametri *codice* valori.  
  
|Valore restituito|Descrizione|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 Il *valore* parametro restituisce uno dei valori di SCROLLOPT seguenti.  
  
|Valore restituito|Descrizione|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 Il *valore* parametro restituisce uno dei valori di CCOPT seguenti.  
  
|Valore restituito|Descrizione|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 o 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
