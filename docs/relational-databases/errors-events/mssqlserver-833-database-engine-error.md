---
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1d71b87d3927e2b79d2147099c50581a3687e32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767831"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|833|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|BUF_LONG_IO|  
|Testo del messaggio|Rilevate %d occorrenze di richieste di I/O che impiegano più di %d secondi per essere completate nel file [%ls] nel database `[%ls] (%d)`.  L'handle di file del sistema operativo è 0x%p.  Offset dell'ultimo I/O lungo: %#016I64x.|  
  
## <a name="explanation"></a>Spiegazione  
Questo messaggio indica che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha eseguito una richiesta di lettura o scrittura dal disco e che la durata dell'operazione è stata superiore a 15 secondi. Questo errore viene segnalato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica un problema relativo al sottosistema di IO.  
  
### <a name="possible-causes"></a>Possibili cause  
Il problema può essere causato da problemi di prestazioni del sistema, errori hardware, errori del firmware, problemi del driver del dispositivo o dall'intervento del driver di filtro nel processo di I/O.  
  
## <a name="user-action"></a>Azione dell'utente  
Per risolvere il problema che ha causato questo errore, individuare nel registro eventi di sistema i messaggi di errore correlati all'hardware. Esaminare inoltre eventuali log specifici dei componenti hardware se disponibili.  
  
Utilizzare Performance Monitor per esaminare i contatori seguenti:  
  
-   **Media secondi/trasf. disco**  
  
-   **Lunghezza media coda del disco**  
  
-   **Lunghezza corrente coda del disco**  
  
Il valore della durata media, ad esempio, di **Disco sec/trasferimento** in un computer che esegue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è in genere inferiore a 15 millisecondi. L'aumento del valore di **Media secondi/trasf. disco** indica che il sottosistema di I/O non è in grado di soddisfare in modo ottimale le richieste di I/O.  
  
> [!NOTE]  
> L'accesso al disco può essere rallentato da un programma antivirus. Per aumentare la velocità di accesso, escludere dalle analisi virus attive i file di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificati nel messaggio di errore.  
  
Per altre informazioni sugli errori di I/O, vedere [Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (Nozioni di base sull'I/O in Microsoft SQL Server, capitolo 2) e l'articolo della Knowledge Base all'indirizzo [https://support.microsoft.com/kb/897284/en-us](https://support.microsoft.com/kb/897284/en-us).  
  
