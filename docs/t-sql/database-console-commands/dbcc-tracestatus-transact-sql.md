---
title: DBCC TRACESTATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs:
- TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
author: pmasl
ms.author: umajay
ms.openlocfilehash: 3d353a6c11d19f96f590e11aa5ebe48677c3cd84
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211234"
---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

Visualizza lo stato dei flag di traccia.
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argomenti  
*trace#*  
Numero del flag di traccia per cui è visualizzato lo stato. Se non vengono specificati *trace#* e -1, vengono visualizzati tutti i flag di traccia abilitati per la sessione.
  
*n*  
Segnaposto che indica la possibilità di specificare più flag di traccia.
  
-1  
Visualizza lo stato dei flag di traccia abilitati a livello globale. Se viene specificato -1 senza *trace#* , vengono visualizzati tutti i flag di traccia abilitati.
  
WITH NO_INFOMSGS  
Evita la visualizzazione di tutti i messaggi informativi con livello di gravità compreso tra 0 e 10.
  
## <a name="result-sets"></a>Set di risultati  
Nella tabella seguente vengono descritte le informazioni del set di risultati.
  
|Nome colonna|Descrizione|  
|---|---|
|**TraceFlag**|Nome del flag di traccia|  
|**Stato**|Indica se il flag di traccia è impostato su ON o OFF, a livello globale o a livello di sessione.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|**Global**|Indica se il flag di traccia è impostato a livello globale<br /><br /> 1 = True<br /><br /> 0 = False|  
|**Session**|Indica se il file di traccia è impostato per la sessione<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS restituisce una colonna per il numero del flag di traccia e una colonna per lo stato. Indica se il flag di traccia è impostato su ON (1) o OFF (0). L'intestazione di colonna per il numero del flag di traccia è **Global Trace Flag** o **Session Trace Flag**, a seconda che si stia controllando lo stato di un flag di traccia globale o di sessione.
  
## <a name="remarks"></a>Remarks  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono disponibili due tipi di flag di traccia: di sessione e globali. I flag di traccia di sessione sono attivi per una connessione e sono visibili solo per tale connessione. I flag di traccia globali vengono impostati a livello del server e sono visibili per tutte le connessioni nel server.
  
## <a name="permissions"></a>Autorizzazioni  
È richiesta l'appartenenza al ruolo **public** .
  
## <a name="examples"></a>Esempi  
Nell'esempio seguente viene visualizzato lo stato di tutti i flag di traccia abilitati a livello globale.
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
Nell'esempio seguente viene visualizzato lo stato dei flag di traccia `2528` e `3205`.
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
Nell'esempio seguente viene indicato se il flag di traccia `3205` è abilitato a livello globale.
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
Nell'esempio seguente vengono elencati tutti i flag di traccia abilitati per la sessione corrente.
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[Flag di traccia &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
