---
title: Note sulla versione (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 05/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 969caa46506c9fd19410c5ace753076b3ba02fbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65619992"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Note sulla versione per il driver Microsoft OLE DB per SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Questa pagina elenca le nuove funzionalità aggiunte o modificate in ogni versione di Microsoft OLE DB Driver for SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1822"></a>18.2.2

Maggio 2019

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione dell'autenticazione non interattiva di Azure Active Directory nell'apartment a thread multipli (MTA). | OLE DB Driver 18.2.1 prova erroneamente a modificare il modello di concorrenza COM in un apartment che è stato inizializzato in precedenza con thread multipli (MTA). Di conseguenza, in un'applicazione che effettua più di una chiamata successiva a [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) o a [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) prima di chiamare l'interfaccia [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522), il driver non riesce a connettersi quando si usa una qualsiasi modalità di autenticazione di Azure Active Directory. |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

Febbraio 2019

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la codifica server UTF-8. | &bull; &nbsp; [Supporto UTF-8 in OLE DB Driver for SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Supporto dell'autenticazione di Azure Active Directory. | &bull; &nbsp; [Uso di Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Luglio 2018

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la parola chiave della stringa di connessione `UseFMTONLY` e per la proprietà di inizializzazione `SSPROP_INIT_USEFMTONLY`. | `UseFMTONLY` controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.<br/><br/>&bull; &nbsp; [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Correzione della versione errata del file di formato BCP. | OLE DB Driver 18.0 imposta in modo errato la versione del file di formato BCP su 18.0, anziché su 11.0.<br/><br/>OLE DB Driver 18.1 non è in grado di leggere file di formato generati da OLE DB Driver 18.0.<br/><br/>Se è necessario usare con il nuovo driver file di formato generati con la versione precedente, è possibile modificare manualmente i file in modo da impostare la versione su 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Funzionalità aggiunte

| Funzionalità aggiunta | Dettagli |
| :------------ | :------ |
| Supporto per la parola chiave della stringa di connessione `MultiSubnetFailover` e la proprietà di inizializzazione `SSPROP_INIT_MULTISUBNETFAILOVER`. | &bull; &nbsp; [Supporto di OLE DB Driver for SQL Server per il ripristino di emergenza a disponibilità elevata](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche

[Driver Microsoft OLE DB per SQL Server](oledb-driver-for-sql-server.md)
