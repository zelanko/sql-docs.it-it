---
title: Informazioni sul motore di database SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6373f67d40b9da97f652f3bcb05b3414deab5c8d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779362"
---
# <a name="about-the-sql-server-database-engine"></a>Informazioni sul Motore di database di SQL Server
  Il componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresenta il servizio principale per l'archiviazione, l'elaborazione e la protezione dei dati. Grazie all'accesso controllato e all'elaborazione rapida delle transazioni, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in grado di soddisfare i requisiti delle applicazioni che richiedono un maggiore utilizzo di dati nell'organizzazione.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta fino a 50 istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in un singolo computer. Per creare un'installazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipica di, vedere [installare SQL Server 2014 dall'installazione guidata &#40;&#41;di ](install-sql-server-from-the-installation-wizard-setup.md)installazione.  
  
 **Importante** Per le installazioni locali, è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.  
  
 Quando si seleziona ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motore di database** nella pagina componenti da installare dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installazione guidata di, vengono installate le funzionalità seguenti:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Replica - componente facoltativo  
  
-   Ricerca full-text - componente facoltativo  
  
-   Data Quality Services - componente facoltativo  
  
    > [!NOTE]  
    >  In questa versione, la selezione della casella di controllo **Data Quality Services** nell'installazione non comporta l'installazione del server Data Quality Services (DQS). Sarà necessario eseguire dei passaggi aggiuntivi postinstallazione per installare server DQS. Per altre informazioni, vedere [Installare Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 Le funzionalità aggiuntive seguenti rappresentano opzioni disponibili per molti scenari utente tipici:  
  
-   Client Data Quality  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Componenti di connettività  
  
-   Modelli di programmazione  
  
-   Strumenti di gestione  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Componenti della documentazione  
  
> [!NOTE]  
>  Per impostazione predefinita, i database di esempio e il codice di esempio non vengono installati come parte dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per installare i database di esempio e il codice di esempio, vedere il sito Web [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Edizioni e componenti di SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Eseguire l'aggiornamento a SQL Server 2014 usando l'installazione guidata &#40;&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
