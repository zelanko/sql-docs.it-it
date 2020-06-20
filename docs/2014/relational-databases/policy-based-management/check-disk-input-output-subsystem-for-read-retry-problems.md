---
title: Controllare il sottosistema di output di input del disco per i problemi di lettura dei tentativi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 19809b1554e435600eb4eeae424bed17dc27bdbb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068985"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>Verifica dei problemi relativi ai tentativi di lettura nel sottosistema di input/output del disco
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
  
  
