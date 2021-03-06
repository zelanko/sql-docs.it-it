---
title: Che cos'è l'estensione per il linguaggio Java?
titleSuffix: SQL Server Language Extensions
description: L'estensione per il linguaggio Java è una funzionalità di SQL Server usata per l'esecuzione di codice Java esterno. È possibile usare dati relazionali nel codice Java esterno tramite il framework di estendibilità.
author: dphansen
ms.author: davidph
ms.date: 11/10/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: f68821900b2e304028bccfd79e96f988f02267e9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471722"
---
# <a name="what-is-java-language-extension"></a>Che cos'è l'estensione per il linguaggio Java?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

L'estensione per il linguaggio Java è una funzionalità di SQL Server usata per l'esecuzione di codice Java esterno. È possibile usare dati relazionali nel codice Java esterno tramite il [framework di estendibilità](concepts/extensibility-framework.md). L'estensione per il linguaggio Java è inclusa nelle [estensioni del linguaggio di SQL Server](language-extensions-overview.md).

Il runtime Java predefinito è Zulu Open JRE. È anche possibile usare un altro JRE o SDK Java.

## <a name="what-you-can-do-with-the-java-language-extension"></a>Potenzialità dell'estensione del linguaggio Java

L'estensione del linguaggio Java usa il framework di estendibilità per l'esecuzione di codice Java esterno. L'esecuzione del codice è isolata dai processi del motore di base, ma completamente integrata con l'esecuzione delle query di SQL Server. È possibile eseguire il codice Java nell'origine dati, eliminando la necessità di eseguire il pull dei dati attraverso la rete.

Il linguaggio Java esterno è definito con [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql). La stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) viene usata come interfaccia per l'esecuzione del codice Java.

## <a name="get-started-with-java-language-extension"></a>Introduzione all'estensione del linguaggio Java

1. [Installare l'estensione del linguaggio Java di SQL Server in Windows](install/windows-java.md) o [in Linux](../linux/sql-server-linux-setup-language-extensions-java.md).

1. Configurare uno strumento di sviluppo.

    + Usare l'ambiente di sviluppo integrato (IDE) preferito per lo sviluppo di codice Java.
    + Installare [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md) per eseguire codice Java in SQL Server.
    + Usare [Azure Data Studio](../azure-data-studio/what-is.md) per l'esecuzione di codice esterno in SQL Server.
    + Usare la stored procedure di sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) per eseguire codice Java in SQL Server.

1. Scrivere il primo codice Java.

    + [Esercitazione: Espressioni regolari con Java](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>Limitazioni

Il numero dei valori nei buffer di input e output non può superare `MAX_INT (2^31-1)` perché questo è il numero massimo di elementi che possono essere allocati in una matrice in Java.

## <a name="next-steps"></a>Passaggi successivi

+ Installare l'[estensione del linguaggio Java di SQL Server in Windows](install/windows-java.md) o [in Linux](../linux/sql-server-linux-setup-language-extensions-java.md)
+ Installare [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md)
