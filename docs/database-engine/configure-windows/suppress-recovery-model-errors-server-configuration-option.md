---
title: Non visualizzare gli errori del modello di recupero - Opzione di configurazione del server | Microsoft Docs
ms.custom: ''
ms.date: 07/20/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a59ff201edb153487640b4c5781d38a2df3756f9
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942226"
---
# <a name="suppress-recovery-model-errors-server-configuration-option"></a>Opzione di configurazione del server per non visualizzare gli errori del modello di recupero

[!INCLUDE[tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md](../../includes/tsql-appliesto-xxxxxx-asdbmi-xxxx-xxx-md.md)]

I [modelli di recupero](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server) di SQL Server controllano la manutenzione del log delle transazioni. Il modello di recupero con registrazione completa garantisce che non si verifichi alcuna perdita in seguito alla perdita o al danneggiamento di un file di dati e supporta il ripristino in un punto nel tempo arbitrario nell'ambito dei criteri di conservazione dei backup. Il modello di recupero con registrazione completa è un modello predefinito e l'unico modello di recupero supportato in Istanza gestita di SQL. I tentativi di modificare il modello di recupero in Istanza gestita di SQL restituiranno un messaggio di errore.

Usare l'opzione di configurazione avanzata **suppress recovery model errors** per specificare se i comandi per modificare il modello di recupero del database, eseguiti in Istanza gestita di SQL, restituiranno un errore o solo un avviso. Se questa opzione è impostata su 1 (attivata) in Istanza gestita di SQL, l'esecuzione del comando ALTER DATABASE SET RECOVERY non modificherà il modello di recupero del database. Non restituirà comunque un errore, ma un messaggio di avviso. Quando questa opzione è impostata su 0 (disattivata) in Istanza gestita di SQL, l'esecuzione del comando ALTER DATABASE SET RECOVERY restituirà un messaggio di errore.

L'opzione **suppress recovery model errors** è utile quando applicazioni legacy o di terze parti provano a impostare il modello di recupero su Simple o Bulk logged, anche se non è un requisito critico o obbligatorio. Quando la modifica del modello di recupero è l'unico impedimento all'uso di Istanza gestita di SQL, l'attivazione dell'opzione di configurazione suppress recovery model errors rimuove tale impedimento. Questa opzione è particolarmente utile se non esiste una soluzione alternativa fattibile o conveniente per modificare il codice dell'applicazione.

## <a name="examples"></a>Esempi

L'esempio seguente abilita l'eliminazione dei messaggi di errore relativi alla modifica del modello di recupero del database e quindi esegue il comando per modificare il modello di recupero del database, restituendo solo un avviso. Il modello di recupero non viene effettivamente modificato. Assicurarsi di sostituire *my_database* con il nome effettivo del database.

```sql
-- Turn advanced configuration options on:
sp_configure 'show advanced options', 1 ;  
GO
RECONFIGURE ;  
GO

-- Enable suppression of error messages for recovery model change:
sp_configure 'suppress recovery model errors', 1 ;  
GO
RECONFIGURE ;  
GO

-- Execute command for changing recovery model to Simple:
ALTER DATABASE my_database SET RECOVERY SIMPLE;
GO
```

## <a name="see-also"></a>Vedere anche

[Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)

[sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)

[RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)
