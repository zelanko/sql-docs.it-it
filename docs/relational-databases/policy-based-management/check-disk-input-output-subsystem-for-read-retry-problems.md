---
title: Verificare la presenza di problemi nel sottosistema di I/O del disco - gestione basata su criteri
description: Questa regola consente di controllare il messaggio di errore 825 di SQL Server nel registro eventi, che indica che SQL Server non è in grado di leggere i dati dal disco al primo tentativo.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0f894452dd056cf0e613100a5d1a7ee2d5e9ae0c
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558191"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Verifica dei problemi correlati ai tentativi di lettura nel sottosistema di input/output del disco
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare il messaggio di errore 825 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel registro eventi. Tale messaggio indica che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è stato in grado per di leggere dati dal disco al primo tentativo. Il messaggio indica un problema grave relativo al sottosistema di I/O del disco Questo messaggio non indica attualmente un problema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se non viene risolto, tuttavia, il problema del disco potrebbe provocare la perdita di dati o il danneggiamento del database.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Le azioni seguenti possono contribuire a individuare e risolvere il problema hardware sottostante:  
  
-   Esaminare il log degli errori e il testo delle variabili di questo messaggio per individuare eventuali indizi che consentano di spiegare il problema.  
  
-   Controllare il sistema di dischi. Il problema potrebbe essere correlato ai dischi, ai controller dei dischi, alle schede di array o ai driver dei dischi.  
  
-   Contattare il produttore dei dischi e richiedere le utilità più recenti per verificare lo stato del sistema di dischi.  
  
-   Contattare il produttore dei dischi e richiedere gli ultimi aggiornamenti dei driver.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
