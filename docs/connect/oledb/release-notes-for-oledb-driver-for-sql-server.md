---
title: Note sulla versione (OLE DB Driver for SQL Server) | Microsoft Docs
ms.date: 02/12/2019
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
ms.openlocfilehash: 36dc1b7325265da6231b75e9f4db46854b0b219f
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744361"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>Note sulla versione per il driver Microsoft OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

Questo argomento vengono illustrate le funzionalità aggiunte in ogni versione del Driver OLE DB Microsoft per SQL Server.

## <a name="whats-new-in-version-1821"></a>Novità della versione 18.2.1

**Funzionalità aggiunte:**

* Supporto per la codifica UTF-8 server. Per altre informazioni, vedere: [supporto per UTF-8 nel Driver OLE DB per SQL Server](features/utf-8-support-in-oledb-driver-for-sql-server.md).
* Supporto dell'autenticazione di Azure Active Directory. Per altre informazioni vedere [Uso di Azure Active Directory](features/using-azure-active-directory.md).

## <a name="whats-new-in-version-1810"></a>Novità della versione 18.1.0

**Funzionalità aggiunte:**

* Supporto per `UseFMTONLY` parola chiave di stringa di connessione e `SSPROP_INIT_USEFMTONLY` proprietà di inizializzazione.
`UseFMTONLY` Controlla la modalità di recupero dei metadati durante la connessione a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni successive.  
Per altre informazioni, vedere:
  * [Utilizzo delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

**Problemi risolti:**

* Versione predefinito non corretto del file di formato BCP. Versioni 18.0 Driver OLE DB in modo non corretto imposta la versione del file di formato BCP 18.0 anziché 11.0. I file di formato generati da versioni 18.0 Driver OLE DB possono essere letti 18.1 Driver OLE DB. Se è necessario usare i file di formato generati dalla versione precedente del driver con il nuovo driver, è possibile modificare manualmente i file per modificare la versione a 11.0.

## <a name="whats-new-in-version-1802"></a>Novità della versione 18.0.2

**Funzionalità aggiunte**:

* Supporto per `MultiSubnetFailover` parola chiave di stringa di connessione e `SSPROP_INIT_MULTISUBNETFAILOVER` proprietà di inizializzazione.  
Per altre informazioni, vedere:  
  * [Driver OLE DB per il supporto di SQL Server per il ripristino di emergenza a disponibilità elevata](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  
  * [Utilizzo delle parole chiave delle stringhe di connessione con driver OLE DB per SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)

## <a name="see-also"></a>Vedere anche
[Driver Microsoft OLE DB per SQL Server](oledb-driver-for-sql-server.md)
