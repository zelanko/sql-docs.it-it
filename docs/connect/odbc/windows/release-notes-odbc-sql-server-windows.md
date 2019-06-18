---
title: Note sulla versione di ODBC per SQL Server in Windows | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-jizho2, v-chojas, genemi
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: f74d5a70325fdceb311bb3a45ba6824e64242ff0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63031209"
---
# <a name="release-notes-for-odbc-to-sql-server-on-windows"></a>Note sulla versione di ODBC per SQL Server in Windows

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo articolo relativo alle note sulla versione descrive le novità del driver Microsoft ODBC per SQL Server in Windows.

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="173-february-2019"></a>17.3, febbraio 2019

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Modalità di autenticazione dell'identità del servizio gestita di Azure Active Directory (assegnata dal sistema e dall'utente). | Vedere [Uso di Azure Active Directory con il driver ODBC](../using-azure-active-directory.md). |
| Capacità di trasmettere i parametri di input alle colonne Always Encrypted. | Vedere [Limitazioni del driver ODBC quando si usa Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted). |
| Transazioni distribuite XA. | [Uso delle transazioni XA](../use-xa-with-dtc.md). |
| Correzioni di bug. | Vedere [Correzioni di bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, luglio 2018

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Classificazione dei dati per il database SQL di Microsoft Azure e SQL Server. | Vedere [Classificazione dei dati](../data-classification.md). |
| Supporto per la codifica server UTF-8. | &nbsp; |
| Correzioni di bug. | Vedere [Correzioni di bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, marzo 2018

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto degli attributi di connessione `SQL_COPT_SS_CEKCACHETTL` e `SQL_COPT_SS_TRUSTEDCMKPATHS`. | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>Consente di controllare l'ora in cui è presente la cache locale delle chiavi di crittografia di colonna e di scaricarla.<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>Consente all'applicazione di limitare le operazioni Always Encrypted in modo che usi solo l'elenco specificato di chiavi master della colonna.<br/><br/> Per altre informazioni, vedere [Uso di Always Encrypted con ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md). |
| Supporto dell'autenticazione interattiva di Azure Active Directory | &nbsp; |
| Correzioni di bug. | Vedere [Correzioni di bug](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17-february-2018"></a>17, febbraio 2018

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto di Always Encrypted per l'API BCP. | &nbsp; |
| Nuovo attributo della stringa di connessione `UseFMTOnly`. | Il driver userà i metadati legacy nei casi particolari in cui sono richieste tabelle temporanee. |
| Supporto di Istanza gestita di database SQL di Azure. | Anteprima privata estesa.<br/><br/>Vedere l'elenco seguente in [Differenze nell'uso di Istanza gestita (ODBC versione 17)](#diffs-managed-instance-17). |
| &nbsp; | &nbsp; |

| Dipendenza modificata | Dettagli |
| :------------ | :------ |
| Rimosso il servizio Assistente per l'accesso a Microsoft Online Services | La dipendenza è stata rimossa. |
| &nbsp; | &nbsp; |

### <a name="diffs-managed-instance-17"></a> Differenze nell'uso di Istanza gestita (ODBC versione 17)

Questa versione di ODBC contiene il supporto per Istanza gestita del database SQL di Azure (anteprima privata estesa). Vedere l'elenco con le note seguente relativo alle differenze nell'uso di Istanza gestita.

> [!NOTE]
> Esistono molte differenze nell'uso di Istanza gestita:
>
> - FILESTREAM non è supportato.
> - L'accesso al file system locale non è supportato, ma è obbligatorio per elementi come i file di traccia.
> - La creazione di tipi definiti dall'utente dal percorso locale non è supportata.
> - L'autenticazione integrata di Windows non è supportata.
> - DTC non è supportato.
> - L'account `sa` non è presente. L'account predefinito è `cloudSA`.
> - L'errore del token TDS (0xAA) restituisce un nome server non corretto.
> - Non sono supportati i caratteri speciali nel nome del database.
> - ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] non è supportato.
> - I messaggi di errore vengono sempre visualizzati in inglese, indipendentemente dalle impostazioni della lingua (come in Azure).

## <a name="131"></a>13.1

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aggiunge supporto per [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) e [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md). | Questi supporti aggiuntivi sono disponibili quando ci si connette a Microsoft SQL Server 2016 o a una versione successiva. |
| Esistono parole chiave e attributi del pool di connessioni che si riferiscono ai supporti per Always Encrypted e Azure Active Directory. | Le parole chiave e gli attributi sono descritti in [Pool di connessioni compatibile con il driver in ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Aggiunge supporto per Microsoft SQL Server 2016. | Mantiene la funzionalità del driver ODBC versione 11. |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Contiene nuove funzionalità. | Vedere [Funzionalità di Microsoft ODBC Driver for SQL Server in Windows](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md). |
| Contiene tutte le funzionalità disponibili con ODBC in SQL Server 2012 Native Client. | &nbsp; |
| &nbsp; | &nbsp; |
