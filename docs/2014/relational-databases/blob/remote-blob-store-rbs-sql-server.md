---
title: Archivio Blob remoto (RBS) (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.technology: filestream
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2d9711b5b9d079df0396ba9874b203a89f26344f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874811"
---
# <a name="remote-blob-store-rbs-sql-server"></a>Archivio Blob remoto (RBS) (SQL Server)
  Archivio BLOB remoti (RBS) di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un componente aggiuntivo facoltativo che consente agli amministratori di database di archiviare oggetti binari di grandi dimensioni in soluzioni di archiviazione apposite anziché direttamente nel server di database principale.  
  
 Tale componente è incluso nei supporti di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ma non viene installato dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per altre informazioni su RBS, vedere [Risorse di RBS](#rbsresources) in questo argomento.  
  
## <a name="benefits-of-rbs"></a>Vantaggi di RBS  
 RBS offre i seguenti vantaggi:  
  
### <a name="optimized-database-storage-and-performance"></a>Archiviazione e prestazioni ottimizzate del database  
 L'archiviazione di BLOB nel database può utilizzare grandi quantità di spazio file e risorse server costose. RBS consente di trasferire in modo efficiente BLOB in una soluzione di archiviazione dedicata selezionata e di archiviare i relativi riferimenti nel database. In questo modo vengono liberate l'archiviazione su server per i dati strutturati e le risorse server per le operazioni del database.  
  
### <a name="efficient-management-of-blobs"></a>Gestione efficiente di BLOB  
 Diverse funzionalità di RBS supportano la gestione semplice di BLOB archiviati:  
  
-   BLOB gestiti con transazioni ACID (Atomic Consistency Isolation Durable).  
  
-   BLOB organizzati in raccolte.  
  
-   Garbage Collection, verifica coerenza e altre funzioni di manutenzione.  
  
### <a name="standardized-api"></a>API standardizzata  
 RBS definisce un set di API che fornisce un modello di programmazione standardizzato affinché le applicazioni possano accedere e modificare gli archivi BLOB. Ogni archivio BLOB può specificare la propria libreria del provider che consente il collegamento alla libreria client di RBS e di specificare la modalità di archiviazione e accesso ai BLOB.  
  
 Molti fornitori di soluzioni di archiviazione di terze parti hanno sviluppato provider RBS conformi a queste API standard e in grado di supportare l'archiviazione BLOB su varie piattaforme di archiviazione.  
  
## <a name="rbs-requirements"></a>Requisiti di RBS  
 Per RBS è necessaria l'edizione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise per il server di database principale in cui vengono archiviati i metadati BLOB. Tuttavia, se si utilizza il provider FILESTREAM fornito, è possibile archiviare BLOB nell'edizione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard.  
  
 In RBS è incluso un provider FILESTREAM che consente di utilizzare tale componente per l'archiviazione di BLOB in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si desidera utilizzare RBS per l'archiviazione di BLOB in una soluzione di archiviazione diversa, è necessario utilizzare un provider RBS di terze parti sviluppato per tale soluzione di archiviazione o sviluppare un provider RBS personalizzato utilizzando l'API di RBS. Un provider di esempio che consenta di archiviare BLOB nel file system NTFS è disponibile come risorsa per l'apprendimento in [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190).  
  
## <a name="rbs-security"></a>Sicurezza relativa a RBS  
 Quando si utilizza un provider personalizzato per archiviare BLOB esterni a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile che siano disponibili altri processi che consentono di ignorare il sistema di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Accertarsi di proteggere i BLOB archiviati con autorizzazioni e opzioni di crittografia adatte al supporto di archiviazione utilizzato dal provider personalizzato.  
  
##  <a name="rbsresources"></a> Risorse di RBS  
 **Documentazione di RBS**  
 La documentazione di RBS è inclusa nel pacchetto di Windows Installer. Per consultare la documentazione di RBS senza installare tale componente, è possibile visualizzare la versione [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] della documentazione[ disponibile online in MSDN Library](https://go.microsoft.com/fwlink/?LinkId=210192).  
  
 **White paper su RBS**  
 Il [white paper sull'archiviazione di BLOB remoti](https://go.microsoft.com/fwlink/?LinkId=210422), disponibile per il download come documento di Microsoft Word, contiene informazioni dettagliate sull'installazione e la configurazione di RBS.  
  
 **Esempi di RBS**  
 Negli esempi di RBS disponibili in [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) viene illustrato come sviluppare un'applicazione RBS e come sviluppare e installare un provider RBS personalizzato.  
  
 **Blog di RBS**  
 Nel [blog di RBS](https://go.microsoft.com/fwlink/?LinkId=210315) sono disponibili informazioni aggiuntive sulla distribuzione e gestione di RBS.  
  
  
