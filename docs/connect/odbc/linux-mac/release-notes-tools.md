---
title: Note sulla versione per mssql-tools in Linux e macOS
description: Informazioni sulle novità e le modifiche delle versioni rilasciate di Microsoft SQL Server Tools.
ms.custom: ''
ms.date: 07/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-zhangw
ms.author: v-zhangw
manager: kenvh
ms.openlocfilehash: 85f7115dbf138055df83a7bb07e5a78f505b5794
ms.sourcegitcommit: 6f49804b863fed44968ea5829e2c26edc5988468
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2020
ms.locfileid: "87812356"
---
# <a name="release-notes-for-the-microsoft-sql-server-tools-on-linux-and-macos"></a>Note sulla versione per Microsoft SQL Server Tools in Linux e macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo articolo elenca e descrive le novità delle versioni rilasciate di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] SQL Server Tools in Linux e macOS.

## <a name="17611-july-2020"></a>17.6.1.1, luglio 2020

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Parser della riga di comando sqlcmd aggiornato | Correzione dei bug in cui si è verificato un comportamento imprevisto durante l'uso di determinate opzioni in ordini diversi. |
| Messaggi di errore sqlcmd aggiornati | Sono state risolte diverse incoerenze nella restituzione degli errori in sqlcmd. |
| Opzione -Y di sqlcmd corretta | Correzione del problema per cui l'opzione -Y era inefficace |
| Troncamento del nome di colonna sqlcmd corretto | Correzione del problema per cui i nomi delle colonne venivano troncati in modo errato |
| Codici di uscita Linux sqlcmd | Correzione del problema relativo al codice di uscita del processo mancante in Linux |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sulla connessione con [BCP](connecting-with-bcp.md) ed [SQLCMD](connecting-with-sqlcmd.md).
