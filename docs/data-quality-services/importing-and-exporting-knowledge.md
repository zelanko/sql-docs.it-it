---
description: Importazione ed esportazione delle informazioni
title: Importazione ed esportazione delle informazioni
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 639e248fd938f3d2429b3d33729414224db1dc8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462128"
---
# <a name="importing-and-exporting-knowledge"></a>Importazione ed esportazione delle informazioni

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  È possibile creare le Knowledge Base e i domini direttamente nell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] oppure è possibile importare le informazioni in una Knowledge Base o esportarle da essa. Nell'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] è possibile utilizzare un file di dati per le operazioni di importazione ed esportazione o un file di Excel per le operazioni di importazione. Il file di dati utilizzato è un file crittografato creato da [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) con un'estensione DQS. I file creati da Microsoft Excel potranno presentare l'estensione xlsx, xls o csv. Queste operazioni offrono una maggiore flessibilità nella compilazione e nella condivisione delle informazioni utilizzate per eseguire la pulizia dei dati e la corrispondenza.  
  
> [!IMPORTANT]  
>  È possibile esportare contemporaneamente *tutte* le Knowledge Base del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] in un file di backup DQS con estensione DQSB eseguendo il file DQSInstaller.exe dal prompt dei comandi. Analogamente, è possibile importare contemporaneamente *tutte* le Knowledge Base da un file di backup DQS con estensione DQSB nel [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] eseguendo il file DQSInstaller.exe dal prompt dei comandi. Per informazioni su questa operazione, vedere [Esportare e importare le Knowledge Base di DQS utilizzando DQSInstaller.exe](../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) nella Guida all'installazione di DQS.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 È possibile eseguire le operazioni di importazione ed esportazione seguenti:  
  
|Descrizione operazione|Argomento|  
|-|-|  
|Esportare un dominio di una Knowledge Base in un file di dati DQS|[Esportazione di un dominio in un file DQS](../data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|Importare un dominio da un file di dati DQS in una Knowledge Base esistente|[Importazione di un dominio da un file DQS](../data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|Esportare un'intera Knowledge Base in un file di dati DQS|[Esportazione di una Knowledge Base in un file DQS](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|Importare un'intera Knowledge Base in un file di dati DQS|[Importazione di una Knowledge Base da un file DQS](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|Importare i valori da un file di Excel in un dominio|[Importare i valori da un file di Excel in un dominio](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|Importare i domini da un file di Excel in una Knowledge Base|[Importare i domini da un file di Excel in Individuazione informazioni](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|Importare le informazioni raccolte durante la pulizia in una Knowledge Base|[Importazione dei valori di un progetto di pulizia in un dominio](../data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## <a name="related-tasks"></a>Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Compilazione di una Knowledge Base eseguendo l'individuazione delle informazioni e gestendo queste ultime in modo interattivo|[Compilazione di una Knowledge Base](../data-quality-services/building-a-knowledge-base.md)|  
|Creazione di un singolo dominio e aggiunta di informazioni al dominio.|[Gestione di un dominio](../data-quality-services/managing-a-domain.md)|  
|Creazione di un dominio composito e aggiunta di informazioni al dominio.|[Gestione di un dominio composito](../data-quality-services/managing-a-composite-domain.md)|  
  
  
