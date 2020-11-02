---
description: MSSQLSERVER_
title: MSSQLSERVER_4214
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4214 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0a04ec00e94dca9a4d940a3b0182123f0716d472
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418841"
---
# <a name="mssqlserver_4214"></a>MSSQLSERVER_4214
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Dettagli

|Attributo|valore|
|---|---|
|Nome prodotto|SQL Server|
|ID evento|4214|
|Origine evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbolico|DMPX_NODBBACKUP|
|Testo del messaggio|Impossibile eseguire BACKUP LOG perché non è disponibile un backup di database corrente|
||

## <a name="explanation"></a>Spiegazione

L'errore viene generato quando si tenta di eseguire un backup del log delle transazioni prima di eseguire un backup completo di un database. Prima di provare a eseguire il backup del log delle transazioni per un database, è necessario eseguire un backup completo del database. Nel log degli errori viene inoltre visualizzato il messaggio seguente:

> \<Datetime> Errore di backup: 3041, gravità: 16, stato: 1.  
\<Datetime>  Backup     BACKUP non è in grado di completare il comando BACKUP LOG. \<db_name>. Per messaggi più dettagliati, controllare il log dell'applicazione di backup.

## <a name="user-action"></a>Azione utente

Eseguire un backup completo del database prima di provare a eseguire il backup del log delle transazioni per un database.

## <a name="more-information"></a>Ulteriori informazioni

Per altre informazioni, vedere: [Backup e ripristino di database SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).