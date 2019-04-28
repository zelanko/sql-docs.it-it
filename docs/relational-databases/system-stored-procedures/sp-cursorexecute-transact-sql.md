---
title: sp_cursorexecute (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fcc62c09d42adb10f8984a8f48d8b70e2f5c78de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62723996"
---
# <a name="spcursorexecute-transact-sql"></a>sp_cursorexecute (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea e popola un cursore in base al piano di esecuzione creato da sp_cursorprepare. Questa routine, insieme a sp_cursorprepare, svolge la stessa funzione di sp_cursoropen, ma viene suddivisa in due fasi. è possibile richiamare sp_cursorexecute specificando ID = 4 in un pacchetto del flusso TDS.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>Argomenti  
 *prepared_handle*  
 L'istruzione preparata *gestire* valore restituito da sp_cursorprepare. *prepared_handle* è un parametro obbligatorio che richiede un **int** valore di input.  
  
 *cursor*  
 Identificatore del cursore generato da SQL Server. *cursore* è un parametro obbligatorio che deve essere fornito su tutte le routine successive che agiscono sul cursore, ad esempio sp_cursorfetch  
  
 *scrollopt*  
 Opzione di scorrimento. *scrollopt* è un parametro facoltativo che richiede un **int** valore di input. Il sp_cursorexecute*scrollopt* parametro ha le stesse opzioni dei valori di quelle per sp_cursoropen.  
  
> [!NOTE]  
>  Il valore PARAMETERIZED_STMT non è supportato.  
  
> [!IMPORTANT]  
>  Se un *scrollopt* valore viene omesso, il valore predefinito è KEYSET indipendentemente *scrollopt* valore specificato in sp_cursorprepare.  
  
 *ccopt*  
 Opzione del controllo della valuta. *ccopt* è un parametro facoltativo che richiede un **int** valore di input. Il sp_cursorexecute*ccopt* parametro ha le stesse opzioni dei valori di quelle per sp_cursoropen.  
  
> [!IMPORTANT]  
>  Se un *ccopt* valore viene omesso, il valore predefinito è OPTIMISTIC indipendentemente *ccopt* valore specificato in sp_cursorprepare.  
  
 *rowcount*  
 Parametro facoltativo che indica il numero di righe del buffer di recupero da utilizzare con AUTO_FETCH. Il valore predefinito è 20 righe. *conteggio delle righe* si comporta in modo diverso quando assegnato come valore di input rispetto a un valore restituito.  
  
|Come valore di input|Come valore restituito|  
|--------------------|---------------------|  
|Quando viene specificato AUTO_FETCH con i cursori FAST_FORWARD *rowcount* rappresenta il numero di righe da inserire nel buffer di recupero.|Rappresenta il numero di righe nel set di risultati. Quando la *scrollopt* viene specificato il valore AUTO_FETCH, *rowcount* restituisce il numero di righe recuperate nel buffer di recupero.|  
  
 *bound_param*  
 Indica l'utilizzo facoltativo di parametri aggiuntivi.  
  
> [!NOTE]  
>  I parametri dopo il quinto vengono passati insieme sul piano dell'istruzione come parametri di input.  
  
## <a name="code-return-value"></a>Valore restituito del codice  
 *conteggio delle righe* potrebbe restituire i valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|-1|Numero di righe non note.|  
|-n|Un popolamento asincrono è attivo.|  
  
## <a name="remarks"></a>Note  
  
## <a name="scrollopt-and-ccopt-parameters"></a>Parametri scrollopt e ccopt  
 *scrollopt* e *ccopt* risultano utili per i piani memorizzati nella cache vengono interrotti per la cache del server, vale a dire che è necessario ricompilare l'handle preparato che identifica l'istruzione. Il *scrollopt* e *ccopt* valori di parametro devono corrispondere i valori inviati nella richiesta originale a sp_cursorprepare.  
  
> [!NOTE]  
>  PARAMETERIZED_STMT non deve essere assegnato a *scrollopt*.  
  
 Se non si riesce a fornire valori corrispondenti, i piani verranno ricompilati impedendo le operazioni di preparazione ed esecuzione.  
  
## <a name="rpc-and-tds-considerations"></a>Considerazioni su RPC e TDS  
 Per richiedere che vengano restituiti metadati sull'elenco di selezione del cursore nel flusso TDS, è possibile impostare il flag di input RPC RETURN_METADATA su 1.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_cursoropen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
