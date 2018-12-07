---
title: Installare il motore di database di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 83fb5aa641537e99f7562f6c4fd7981b8e2233b5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532768"
---
# <a name="install-sql-server-database-engine"></a>Installare il motore di database di SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Il componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresenta il servizio principale per l'archiviazione, l'elaborazione e la protezione dei dati. Grazie all'accesso controllato e all'elaborazione rapida delle transazioni, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in grado di soddisfare i requisiti delle applicazioni che richiedono un maggiore utilizzo di dati nell'organizzazione.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta fino a 50 istanze del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in un singolo computer. Per creare un'installazione tipica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Installare SQL Server dall'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
>[!IMPORTANT]
>Per le installazioni locali è necessario eseguire il programma di installazione come amministratore. Se si installa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da una condivisione remota, è necessario utilizzare un account di dominio con autorizzazioni di lettura ed esecuzione relative a tale condivisione.  
  
## <a name="related-features"></a>Funzionalità correlate

Quando si seleziona **Motore di database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** nella pagina Componenti da installare dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vengono installate le funzionalità seguenti:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Replica - componente facoltativo  

-   [Machine Learning Services (In-Database) con R e Python](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) - componente facoltativo

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
>  Per impostazione predefinita, i database di esempio e il codice di esempio non vengono installati come parte dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per installare i database di esempio e il codice di esempio, vedere [Esempi di Microsoft SQL Server](../../sample/microsoft-sql-server-samples.md). Per esempi precedenti, accedere a [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Vedere anche  
 [Edizioni e funzionalità supportate di SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Eseguire l'aggiornamento a SQL Server usando l'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
