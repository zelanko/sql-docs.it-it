---
title: Installare e disinstallare il componente di origine OData | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0a3ae788-e8c8-4a4d-bb15-34c673abcd17
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7c7edea5701fe784f34375c2ff218fc93e610e8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058035"
---
# <a name="install-and-uninstall-odata-source-component"></a>Installare e disinstallare il componente di origine OData
  In questo argomento vengono fornite le istruzioni per installare il componente di origine OData nel computer o per eseguirne la rimozione.  
  
## <a name="installation"></a>Installazione  
 Per il componente di origine OData devono essere installati nel computer i componenti prerequisiti riportati di seguito.  
  
-   SQL Server Data Tools (per la progettazione di pacchetti)  
  
-   SQL Server Integration Services (per l'esecuzione di pacchetti esternamente a Visual Studio)  
  
 Per installare il componente di origine OData, scaricare [Feature Pack di SQL Server 2014](https://go.microsoft.com/fwlink/p/?LinkId=391999) ed eseguire uno dei seguenti file MSI.  
  
-   ODataSourceForSQLServer2014-amd64.msi per piattaforme a 64 bit  
  
-   ODataSourceForSQLServer2014-x86.msi per piattaforme a 32 bit  
  
> [!IMPORTANT]  
>  Il programma di installazione a 64 bit viene installato sia nella versione a 32 bit sia in quella a 64 bit del componente di origine OData. È sufficiente eseguire il programma di installazione a 32 bit se si utilizza un sistema operativo a 32 bit.  
  
## <a name="uninstallation"></a>Disinstallazione  
 Il componente origine OData può essere disinstallato dal **programmi e funzionalità** menu. Trovare il **Microsoft SQL Server SSIS OData Source Component (x64)** voce e fare clic su **Disinstalla**.  
  
  
