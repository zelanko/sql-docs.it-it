---
title: Cosa sono le estensioni del linguaggio di SQL Server?
titleSuffix: ''
description: Le estensioni del linguaggio sono una funzionalità di SQL Server usata per l'esecuzione di codice esterno. In SQL Server 2019 sono supportati Java, Python e R. I dati relazionali possono essere usati nel codice esterno tramite il framework di estendibilità.
author: dphansen
ms.author: davidph
ms.date: 10/07/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c4482adb86f9a2f205bd64044a18f342cf3e13c5
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/17/2020
ms.locfileid: "92154945"
---
# <a name="what-is-sql-server-language-extensions"></a>Cosa sono le estensioni del linguaggio di SQL Server?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Le estensioni del linguaggio sono una funzionalità di SQL Server usata per l'esecuzione di codice esterno. I dati relazionali possono essere usati nel codice esterno tramite il [framework di estendibilità](concepts/extensibility-framework.md).

In SQL Server 2019 sono supportati Java, Python e R.

> [!NOTE]
> Per l'esecuzione di Python o R in SQL Server, vedere la documentazione relativa a [Machine Learning in SQL](../machine-learning/index.yml). Con SQL Server 2019 e versioni successive, è possibile usare un runtime personalizzato di Python e R con le estensioni del linguaggio. Per altre informazioni, vedere il [runtime personalizzato di Python](../machine-learning/install/custom-runtime-python.md) e il [runtime personalizzato di R](../machine-learning/install/custom-runtime-r.md).

## <a name="what-you-can-do-with-language-extensions"></a>Potenzialità delle estensioni del linguaggio

Le estensioni del linguaggio usano il framework di estendibilità per l'esecuzione di codice esterno. L'esecuzione del codice è isolata dai processi del motore di base, ma completamente integrata con l'esecuzione delle query di SQL Server. È possibile eseguire il codice nell'origine dati, eliminando la necessità di eseguire il pull dei dati attraverso la rete.

I linguaggi esterni sono definiti con [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). La stored procedure di sistema [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) viene usata come interfaccia per l'esecuzione del codice.

Le estensioni del linguaggio offrono diversi vantaggi:

+ Sicurezza dei dati. L'esecuzione di un linguaggio esterno più vicino all'origine dei dati evita spostamenti di dati inutili e non sicuri.
+ Velocità. I database sono ottimizzati per le operazioni basate su set. Le recenti innovazioni dei database, come le tabelle in memoria, rendono più rapidi i riepiloghi e le aggregazioni e costituiscono un complemento perfetto per la data science.
+ Facilità di distribuzione e integrazione. [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)] è il punto centrale delle operazioni per molte altre attività di gestione dati e applicazioni. Usando i dati nel database, è possibile assicurarsi che i dati usati dall'estensione del linguaggio siano coerenti e aggiornati.

## <a name="next-steps"></a>Passaggi successivi

+ Installare un [runtime personalizzato di Python per SQL Server](../machine-learning/install/custom-runtime-python.md)
+ Installare un [runtime personalizzato di R per SQL Server](../machine-learning/install/custom-runtime-r.md)
+ Installare le [estensioni del linguaggio di SQL Server in Windows](install/windows-java.md) o [in Linux](../linux/sql-server-linux-setup-language-extensions-java.md)
+ Installare [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md)
