---
title: MSSQLSERVER_825 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 825 (Database Engine error)
ms.assetid: f69f8214-5af1-4769-878b-117ad6eaff52
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a78f8068283c709eee395e6d5cbe92edf28bc1bd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053642"
---
# <a name="mssqlserver_825"></a>MSSQLSERVER_825
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|825|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|B_RETRYWORKED|  
|Testo del messaggio|Operazione di lettura del file '%ls', offset %#016I64x, riuscita dopo %d tentativo/i con errore: %ls. Per informazioni più dettagliate, vedere i messaggi aggiuntivi nel log degli errori di SQL Server e nel registro eventi di sistema. Questa condizione di errore può costituire un rischio per l'integrità del database e deve essere risolta. Eseguire un controllo di consistenza completo del database (DBCC CHECKDB). L'errore può essere causato da molti fattori. Per ulteriori informazioni, vedere la documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo messaggio segnala che è stato necessario eseguire nuovamente l'operazione di lettura almeno una volta e indica un problema grave relativo ai componenti hardware del disco. Non indica attualmente un problema relativo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tuttavia, se irrisolto, il problema relativo al disco potrebbe causare perdite di dati o il danneggiamento del database. Il log degli eventi di sistema potrebbe includere eventi correlati che consentono di diagnosticare il problema. Per altre informazioni sugli errori di I/O, vedere il capitolo 2 della pagina relativa alle [nozioni fondamentali sull'I/O in Microsoft SQL Server](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)).  
  
## <a name="user-action"></a>Azione dell'utente  
 Le azioni seguenti possono contribuire a identificare e risolvere il problema sottostante:  
  
-   Esaminare il log degli errori e il testo delle variabili di questo messaggio per individuare eventuali indizi che consentano di spiegare il problema.  
  
-   Controllare il sistema di dischi. Il problema potrebbe essere correlato ai dischi, ai controller dei dischi, alle schede di array o ai driver dei dischi.  
  
-   Contattare il produttore dei dischi e richiedere le utilità più recenti per verificare lo stato del sistema di dischi.  
  
-   Contattare il produttore dei dischi e richiedere gli ultimi aggiornamenti dei driver.  
  
  
