---
title: Cosa sono le estensioni del linguaggio di SQL Server?
titleSuffix: ''
description: Le estensioni del linguaggio sono una funzionalità di SQL Server usata per l'esecuzione di codice esterno. In SQL Server 2019 sono supportati Java, R e Python. I dati relazionali possono essere usati nel codice esterno tramite il framework di estendibilità.
author: dphansen
ms.author: davidph
ms.date: 08/19/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a7e79d6253c531ef2a008a7284fa8d7cd0365999
ms.sourcegitcommit: 346a37242f889d76cd783f55aeed98023c693610
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2020
ms.locfileid: "91765787"
---
# <a name="what-is-sql-server-language-extensions"></a>Cosa sono le estensioni del linguaggio di SQL Server?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Le estensioni del linguaggio sono una funzionalità di SQL Server usata per l'esecuzione di codice esterno. I dati relazionali possono essere usati nel codice esterno tramite il [framework di estendibilità](concepts/extensibility-framework.md).

Java è supportato in SQL Server 2019. Il runtime Java predefinito è Zulu Open JRE. È anche possibile usare un altro JRE o SDK Java.

> [!NOTE]
> Per l'esecuzione di Python o R in SQL Server, vedere la documentazione di [Machine Learning Services](../machine-learning/sql-server-machine-learning-services.md).

## <a name="what-you-can-do-with-language-extensions"></a>Potenzialità delle estensioni del linguaggio

Le estensioni del linguaggio usano il framework di estendibilità per l'esecuzione di codice esterno. L'esecuzione del codice è isolata dai processi del motore di base, ma completamente integrata con l'esecuzione delle query di SQL Server. Le estensioni consentono di eseguire il codice in cui risiedono i dati, eliminando la necessità di eseguire il pull dei dati attraverso la rete.

I linguaggi esterni sono definiti con [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). La stored procedure di sistema [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) viene usata come interfaccia per l'esecuzione del codice.

Le estensioni del linguaggio offrono diversi vantaggi:

+ Sicurezza dei dati. L'esecuzione di un linguaggio esterno più vicino all'origine dei dati evita spostamenti di dati inutili e non sicuri.
+ Velocità. I database sono ottimizzati per le operazioni basate su set. Le recenti innovazioni dei database, come le tabelle in memoria, rendono più rapidi i riepiloghi e le aggregazioni e costituiscono un complemento perfetto per la data science.
+ Facilità di distribuzione e integrazione. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è il punto centrale delle operazioni per molte altre attività di gestione dati e applicazioni. Usando i dati che risiedono nel database, si garantisce che i dati usati da Java siano coerenti e aggiornati.

## <a name="how-to-get-started"></a>Come iniziare

### <a name="step-1-install-the-software"></a>Passaggio 1: installare il software

+ [Estensioni del linguaggio di SQL Server in Windows](install/install-sql-server-language-extensions-on-windows.md)
+ [Estensioni del linguaggio di SQL Server in Linux](../linux/sql-server-linux-setup-language-extensions.md)

### <a name="step-2-configure-a-development-tool"></a>Passaggio 2: configurare uno strumento di sviluppo

In genere gli sviluppatori scrivono codice dai loro portatili o dalle workstation di sviluppo. Con le estensioni del linguaggio in SQL Server non è necessario modificare questo processo. Al termine dell'installazione, è possibile eseguire codice Java in SQL Server.

+ **Usare l'ambiente di sviluppo integrato (IDE) preferito** per lo sviluppo di codice Java.

+ **Installare [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md)** per eseguire codice Java in SQL Server.

+ **Usare [Azure Data Studio](../azure-data-studio/what-is.md) o [SQL Server Management Studio](../ssms/sql-server-management-studio-ssms.md)** per l'esecuzione di codice esterno in SQL Server.

+ **Usare la stored procedure di sistema [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)** per eseguire codice Java in SQL Server.

### <a name="step-3-write-your-first-code"></a>Passaggio 3: scrivere il primo codice

Eseguire il codice Java dall'interno dello script T-SQL:

+ [Esercitazione: Espressioni regolari con Java](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>Limitazioni

+ Il numero dei valori nei buffer di input e output non può superare `MAX_INT (2^31-1)` perché è il numero massimo di elementi che possono essere allocati in una matrice in Java.

## <a name="next-steps"></a>Passaggi successivi

+ Installare un [runtime personalizzato di Python per SQL Server](../machine-learning/install/custom-runtime-python.md)
+ Installare un [runtime personalizzato di R per SQL Server](../machine-learning/install/custom-runtime-r.md)
+ Installare le [estensioni del linguaggio di SQL Server in Windows](install/install-sql-server-language-extensions-on-windows.md) o [in Linux](../linux/sql-server-linux-setup-language-extensions.md)
+ Installare [Microsoft Extensibility SDK per Java](how-to/extensibility-sdk-java-sql-server.md)