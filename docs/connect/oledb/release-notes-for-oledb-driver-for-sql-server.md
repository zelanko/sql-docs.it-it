---
title: Note sulla versione (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 02/13/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: 2a1d6d216f4f7ec7fee0f5f9aa5810c78f1936e6
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161768"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Note sulla versione per Microsoft OLE DB Driver for SQL Server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Questo argomento vengono illustrate le funzionalità aggiunte in ogni versione del Driver OLE DB Microsoft per SQL Server.

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1821"></a>18.2.1

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

Febbraio 2019

### <a name="features-added"></a>Funzionalità aggiunte

| Aggiungere funzionalità | Dettagli |
| :------------ | :------ |
| Supporto per la codifica UTF-8 server. | &bull; &nbsp; [Supporto UTF-8 in OLE DB Driver for SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md). |
| Supporto dell'autenticazione di Azure Active Directory. | &bull; &nbsp; [Uso di Azure Active Directory](features/using-azure-active-directory.md). |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

Luglio 2018

### <a name="features-added"></a>Funzionalità aggiunte

| Aggiungere funzionalità | Dettagli |
| :------------ | :------ |
| Supporto per la `UseFMTONLY` parola chiave di stringa di connessione e per il `SSPROP_INIT_USEFMTONLY` proprietà di inizializzazione. | `UseFMTONLY` Controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.<br/><br/>&bull; &nbsp; [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>Bug risolti

| Bug risolto | Dettagli |
| :-------- | :------ |
| Versione predefinito non corretto del file di formato BCP. | Versioni 18.0 Driver OLE DB imposta in modo non corretto la versione del file di formato BCP per versioni 18.0, anziché su 11.0.<br/><br/>I file di formato generati da versioni 18.0 Driver OLE DB possono essere letti 18.1 Driver OLE DB.<br/><br/>Se è necessario usare i file di formato generati dalla versione precedente del driver con il nuovo driver, è possibile modificare manualmente i file per modificare la versione a 11.0. |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

### <a name="features-added"></a>Funzionalità aggiunte

| Aggiungere funzionalità | Dettagli |
| :------------ | :------ |
| Supporto per il `MultiSubnetFailover` parola chiave della stringa, connessione e il `SSPROP_INIT_MULTISUBNETFAILOVER` proprietà di inizializzazione. | &bull; &nbsp; [Supporto di OLE DB Driver for SQL Server per il ripristino di emergenza a disponibilità elevata](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).<br/><br/>&bull; &nbsp; [Uso delle parole chiave delle stringhe di connessione con OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche

[Driver Microsoft OLE DB per SQL Server](oledb-driver-for-sql-server.md)
