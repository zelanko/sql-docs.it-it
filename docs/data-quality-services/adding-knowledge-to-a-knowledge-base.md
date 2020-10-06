---
description: Aggiunta di informazioni a una Knowledge Base
title: Aggiunta di informazioni a una Knowledge Base
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
author: swinarko
ms.author: sawinark
ms.openlocfilehash: bffd325b4c940302ebcc4fef67c17f5f76c03a00
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724661"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>Aggiunta di informazioni a una Knowledge Base

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  In questo argomento vengono descritte le modalità mediante cui è possibile aggiungere informazioni a una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Prima che sia possibile eseguire operazioni relative alla qualità dei dati, è necessario disporre di informazioni in relazione ai dati stessi. Tali informazioni si acquisiscono compilando e gestendo una Data Quality Knowledge Base e aggiungendovi informazioni correlate a un tipo specifico di origine dati. La Knowledge Base è un repository di informazioni sui dati che consente di comprenderli e mantenerne l'integrità.  
  
 In essa sono contenuti domini di dati relativi all'origine dati. Per ogni dominio di dati, nella DQKB vengono archiviati tutti i termini identificati, gli errori di ortografia, le regole di convalida e di business e dati di riferimento che possono essere utilizzati per eseguire azioni relative alla qualità dei dati sull'origine dati. In DQS queste informazioni vengono utilizzate per identificare dati errati o non validi o per eseguire l'individuazione delle corrispondenze.  
  
 È possibile aggiungere informazioni a una Knowledge Base nelle seguenti modalità computerizzate o interattive.  
  
-   [Esecuzione dell'individuazione delle informazioni](#Discovery)  
  
-   [Gestione dei valori dei dati in un dominio](#ManageDomain)  
  
-   [Importazione di informazioni da un file DQS](#DQSFile)  
  
-   [Importazione di informazioni da un file di Excel](#Excel)  
  
-   [Re-importazione di informazioni da un progetto nella Knowledge Base](#Project)  
  
-   [Utilizzo della Knowledge Base DQS predefinita](#Default)  
  
##  <a name="perform-knowledge-discovery"></a><a name="Discovery"></a> Eseguire l'individuazione delle informazioni  
 L'individuazione delle informazioni consente di analizzare un esempio di dati per stabilire i criteri di qualità, quindi di aggiungere le informazioni acquisite alla Knowledge Base. Si tratta di un processo computerizzato che identifica le incoerenze e gli errori di sintassi, proponendo modifiche ai dati. L'attività di individuazione delle informazioni è una procedura guidata che include una pagina in cui è possibile gestire i valori di dominio in modo interattivo.  
  
-   Per ulteriori informazioni, vedere [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
-   Per un video in cui si dimostra come eseguire l'individuazione delle informazioni, fare clic [qui](../sql-server/index.yml).  
  
##  <a name="manage-data-values-in-a-domain"></a><a name="ManageDomain"></a> Gestire i valori dei dati in un dominio  
 DQS consente di modificare e aumentare in modo interattivo i metadati generati dall'attività di individuazione delle informazioni computerizzata. L'operazione viene eseguita nell'attività di gestione del dominio, dove è possibile applicare una modifica a un valore dei dati specifico.  
  
-   Per ulteriori informazioni, vedere [Change Domain Values](../data-quality-services/change-domain-values.md).  
  
-   Per un video in cui si dimostra come eseguire la gestione di un dominio, fare clic [qui](../sql-server/index.yml). Si noti che in questo video si modificano i valori di dominio nella pagina di gestione dei valori di dominio della procedura guidata relativa all'individuazione delle informazioni. È inoltre possibile eseguire questi passaggi nella pagina Valori di dominio dell'attività di gestione del dominio.  
  
##  <a name="import-knowledge-from-a-dqs-file"></a><a name="DQSFile"></a> Importazione di informazioni da un file DQS  
 È possibile importare un dominio da un file dqs in una Knowledge Base esistente oppure importare una Knowledge Base intera da un file dqs in una nuova Knowledge Base. A tale scopo, è prima necessario esportare un dominio o Knowledge Base esistente in un file dqs. Un file dqs che contiene un dominio include tutti i dati del dominio; un file dqs che contiene una Knowledge Base conterrà tutte le informazioni sulla Knowledge Base, inclusi i domini e i criteri di corrispondenza.  
  
-   Per altre informazioni, vedere [Importare un dominio da un file DQS](../data-quality-services/import-a-domain-from-a-dqs-file.md) o [Importare una Knowledge Base da un file DQS](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md).  
  
##  <a name="import-knowledge-from-an-excel-file"></a><a name="Excel"></a> Importa informazioni da un file di Excel  
 È possibile importare valori di dominio da un foglio di calcolo di Excel in un dominio o Knowledge Base esistente. A tale scopo, è necessario prima creare un foglio di calcolo di Excel con i valori di dominio da importare e assicurarsi che Excel sia installato nel computer [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] per essere in grado di importare valori utilizzando [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Non è possibile esportare valori di dominio da un dominio o Knowledge Base a un file di Excel.  
  
-   Per altre informazioni nella documentazione, vedere [Importare i valori da un file di Excel in un dominio](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md) o [Importare i domini da un file di Excel in Individuazione informazioni](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md).  
  
##  <a name="import-knowledge-from-a-project-back-into-the-knowledge-base"></a><a name="Project"></a> Importare le informazioni da un progetto di nuovo nella Knowledge base  
 Dopo aver eseguito un progetto di pulizia o di qualità dei dati corrispondenti utilizzando una Knowledge Base, è possibile re-importare le informazioni create durante la pulizia o l'individuazione delle corrispondenze nella Knowledge Base. Questo consente di conservare le informazioni generate durante il progetto e di continuare l'aggiunta di informazioni alla Knowledge Base.  
  
-   Per altre informazioni, vedere [Importare i valori di un progetto di pulizia in un dominio](../data-quality-services/import-cleansing-project-values-into-a-domain.md).  
  
##  <a name="use-the-default-dqs-knowledge-base"></a><a name="Default"></a> Utilizzare la Knowledge Base DQS predefinita  
 In DQS è disponibile una Knowledge Base precompilata denominata DQS Data che contiene domini con dati relativi nomi e indirizzi di società statunitensi. Questa Knowledge Base può essere utilizzata per avviare rapidamente un progetto senza creare una nuova Knowledge Base. La Knowledge Base DQS Data è di sola lettura, ma l'amministratore dei dati può creare una nuova Knowledge Base basandosi su di essa.  
  
-   Per ulteriori informazioni, vedere [Using the DQS Default Knowledge Base](../data-quality-services/using-the-dqs-default-knowledge-base.md).  
  
