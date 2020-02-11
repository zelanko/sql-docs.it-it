---
title: Panoramica del processo di aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server
- Upgrade Advisor [SQL Server], process description
- SQL Server Upgrade Advisor, process description
- upgrade process [Upgrade Advisor]
ms.assetid: f77ffbab-a195-4124-acce-9c538f7ca9ce
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb4bfb2073427d0f48b3d4a7ac7b7ab496299030
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091516"
---
# <a name="upgrade-process-overview"></a>Panoramica del processo di aggiornamento
  In questo argomento vengono fornite informazioni sulle procedure consigliate per Preparazione aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e viene riportato un riepilogo del processo consigliato per eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="upgrade-process"></a>Processo di aggiornamento  
 I server che eseguono [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] possono essere aggiornati a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Mentre alcuni componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere aggiornati sul posto, altri devono essere migrati e altri ancora sono stati sostituiti da nuovi componenti. Ad esempio, a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) sostituisce Data Transformation Services (DTS) e DTS non è più supportato in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Quando si formula il piano di aggiornamento, è possibile che sia necessario pianificare l'aggiornamento dei pacchetti DTS correnti ai pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Preparazione aggiornamento consente di valutare le installazioni, i componenti e i file correlati correnti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per identificare i problemi noti che si verificano durante e dopo l'aggiornamento o la migrazione a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Alcuni di questi problemi noti bloccano l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Nel report di Preparazione aggiornamento, questi problemi sono identificati come blocchi di aggiornamento. Prima di eseguire il programma di installazione è necessario risolvere i blocchi di aggiornamento, altrimenti il programma di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] viene terminato e viene consigliato di eseguire Preparazione aggiornamento per identificare i problemi specifici che bloccano l'esecuzione dell'aggiornamento.  
  
 Prima di eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è consigliabile eseguire il backup dei dati e delle impostazioni di sistema ed effettuare le operazioni strategiche come descritto nelle linee guida per il funzionamento definite per la propria organizzazione. Per completare l'aggiornamento, eseguire le operazioni seguenti:  
  
1.  Esaminare le informazioni contenute in [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md).  
  
2.  Eseguire il backup di dati e impostazioni del sistema.  
  
3.  Eseguire Preparazione aggiornamento.  
  
     I dati o le impostazioni del computer non verranno modificate.  
  
4.  Esaminare i problemi identificati nel report di Preparazione aggiornamento.  
  
5.  Risolvere eventuali problemi di blocco che potrebbero impedire l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
6.  Risolvere eventuali altri problemi di pre-aggiornamento.  
  
7.  Eseguire Preparazione aggiornamento per verificare che tutti i problemi noti siano stati risolti.  
  
8.  Eseguire il programma di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
9. Risolvere eventuali problemi di post-aggiornamento e migrazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di preparazione aggiornamento &#40;interfaccia utente&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Utilizzo dei report](../../../2014/sql-server/install/using-reports.md)   
 [Utilizzo di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
