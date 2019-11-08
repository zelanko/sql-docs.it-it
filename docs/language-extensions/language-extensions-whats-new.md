---
title: Novità relative alle estensioni del linguaggio
titleSuffix: SQL Server Language Extensions
description: Informazioni sulle novità relative alle estensioni del linguaggio per SQL Server 2019.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 13a6a0181297fcb05274ba4be726c4e10a445064
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589015"
---
# <a name="what-new-in-sql-server-language-extensions"></a>Novità nelle estensioni del linguaggio di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In ogni versione di SQL Server vengono aggiunte funzionalità di [estensione del linguaggio](language-extensions-overview.md) man mano che l'integrazione tra linguaggi esterni e la piattaforma dati viene espansa, estesa e approfondita. 

## <a name="new-in-sql-server-2019"></a>Novità di SQL Server 2019 

In questa versione è stato aggiunto il supporto per estensioni del linguaggio in SQL Server. Per altre informazioni su tutte le funzionalità di questa versione, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [Note sulla versione per SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

- Il runtime Java predefinito in Windows e Linux è Open Zulu JRE e viene incluso con l'[installazione delle estensioni del linguaggio di SQL Server in Windows](install/install-sql-server-language-extensions-on-windows.md) e con l'[installazione delle estensioni del linguaggio di SQL Server in Linux](../linux/sql-server-linux-setup-language-extensions.md).
- [Tipi di dati Java](how-to/java-to-sql-data-types.md) supportati.
- [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) per la registrazione di un linguaggio esterno (ad esempio, Java) in SQL Server.
- [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md).
- In Windows e Linux è possibile accedere al codice Java in una libreria esterna usando l'istruzione [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md). Altre informazioni: [Come chiamare Java da SQL Server](how-to/call-java-from-sql.md).
- [Estensione del linguaggio Java](language-extensions-overview.md) in Windows e Linux. È possibile rendere disponibile a SQL Server il codice Java compilato assegnando autorizzazioni e impostando il percorso. Le app client con accesso a SQL Server possono usare ed eseguire il codice chiamando [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), ovvero adottando la stessa procedura usata per l'integrazione di R e Python in SQL Server Machine Learning Services.

## <a name="next-steps"></a>Passaggi successivi

+ Installare le [estensioni del linguaggio di SQL Server in Windows](install/install-sql-server-language-extensions-on-windows.md) o [in Linux](../linux/sql-server-linux-setup-language-extensions.md)
