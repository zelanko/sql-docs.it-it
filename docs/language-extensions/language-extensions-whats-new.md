---
title: Novità nelle estensioni del linguaggio di SQL Server
titleSuffix: ''
description: Informazioni sulle novità delle estensioni del linguaggio di SQL Server che espande, estende e approfondisce l'integrazione tra i linguaggi esterni e la piattaforma dati.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1583ab8c54d16d7bcf129e401c2e540fabb342b3
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155091"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>Novità nelle estensioni del linguaggio di SQL Server
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

In ogni versione di SQL Server vengono aggiunte funzionalità di [estensione del linguaggio](language-extensions-overview.md) man mano che l'integrazione tra linguaggi esterni e la piattaforma dati viene espansa, estesa e approfondita.

## <a name="new-python-and-r-language-extensions-in-sql-server-2019"></a>Nuove estensioni di linguaggio Python e R in SQL Server 2019

+ È disponibile un runtime personalizzato per [Python in Windows](../machine-learning/install/custom-runtime-python.md). Per eseguire l'installazione in Linux, vedere [Installare un runtime personalizzato di Python per SQL Server in Linux](../machine-learning/install/custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true).

+ È disponibile un runtime personalizzato per [R in Windows](../machine-learning/install/custom-runtime-r.md). Per eseguire l'installazione in Linux, vedere [Installare un runtime personalizzato di R per SQL Server in Linux](../machine-learning/install/custom-runtime-r.md?view=sql-server-linux-ver15&preserve-view=true).


## <a name="new-java-language-extension-in-sql-server-2019"></a>Nuova estensione del linguaggio Java in SQL Server 2019

Per altre informazioni su tutte le funzionalità di questa versione, vedere [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [Note sulla versione per SQL Server 2019](../sql-server/sql-server-version-15-release-notes.md).

- Il runtime Java predefinito in Windows e Linux è Open Zulu JRE e viene incluso con l'[installazione delle estensioni del linguaggio di SQL Server in Windows](install/windows-java.md) e con l'[installazione delle estensioni del linguaggio di SQL Server in Linux](../linux/sql-server-linux-setup-language-extensions-java.md).
- [Tipi di dati Java](how-to/java-to-sql-data-types.md) supportati.
- [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) per la registrazione di un linguaggio esterno (ad esempio, Java) in SQL Server.
- [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md).
- In Windows e Linux è possibile accedere al codice Java in una libreria esterna usando l'istruzione [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md). Altre informazioni: [Come chiamare Java da SQL Server](how-to/call-java-from-sql.md).
- [Estensione del linguaggio Java](language-extensions-overview.md) in Windows e Linux. È possibile rendere disponibile a SQL Server il codice Java compilato assegnando autorizzazioni e impostando il percorso. Le app client con accesso a SQL Server possono usare ed eseguire il codice chiamando [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), ovvero adottando la stessa procedura usata per l'integrazione di R e Python in SQL Server Machine Learning Services.

## <a name="next-steps"></a>Passaggi successivi

+ Installare le [estensioni del linguaggio di SQL Server in Windows](install/windows-java.md) o [in Linux](../linux/sql-server-linux-setup-language-extensions-java.md).