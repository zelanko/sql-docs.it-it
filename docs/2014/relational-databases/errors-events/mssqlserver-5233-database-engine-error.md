---
title: MSSQLSERVER_5233 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5233 (Database Engine error)
ms.assetid: 7a855afa-2d3b-49b7-adef-197b99fc98b1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a54c45746ec786461135fb3f2a50f4753dbe2df5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867905"
---
# <a name="mssqlserver5233"></a>MSSQLSERVER_5233
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|5233|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC4_INCORRECT_VALUE_IN_PAGE_HEADER_NO_METADATA|  
|Testo del messaggio|Errore di tabella: ID di unità di allocazione A_ID, pagina P_ID. Test (TEST) non riuscito. Valori: VAL1 e VAL2.|  
  
## <a name="explanation"></a>Spiegazione  
 Il controllo sulla pagina *P_ID* non è riuscito poiché l'intestazione della pagina è danneggiata. La stringa presente in TEST indica il test effettivo che non è riuscito.  
  
### <a name="look-for-hardware-failure"></a>Individuare errori hardware  
 Eseguire gli strumenti di diagnostica hardware e risolvere eventuali problemi. Esaminare inoltre il registro di sistema di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e il registro delle applicazioni, nonché il log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per stabilire se l'errore è dovuto a un problema hardware. Risolvere tutti i problemi relativi all'hardware indicati nei log.  
  
 In caso di problemi persistenti che provocano il danneggiamento dei dati, provare a sostituire i vari componenti hardware per isolare il problema. Verificare che nel sistema non sia abilitata la memorizzazione nella cache in scrittura sul controller del disco. Se si ritiene che il problema sia dovuto alla memorizzazione nella cache in scrittura, rivolgersi al fornitore dell'hardware.  
  
 Infine, potrebbe essere conveniente passare a un nuovo sistema hardware. A tale scopo può essere necessario riformattare le unità disco e reinstallare il sistema operativo.  
  
### <a name="restore-from-backup"></a>Eseguire un ripristino da backup  
 Se il problema non è correlato all'hardware ed è disponibile un backup valido noto, ripristinare il database dal backup.  
  
### <a name="run-dbcc-checkdb"></a>Eseguire DBCC CHECKDB  
 Non applicabile. Impossibile correggere questo errore. Se non è possibile ripristinare il database da un backup, contattare il Servizio Supporto Tecnico Clienti Microsoft.  
  
  
