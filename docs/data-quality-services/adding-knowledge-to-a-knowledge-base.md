---
title: Aggiunta di informazioni a una Knowledge Base | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 15802f061f9996d377aa5110b180e0a1fb065081
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020353"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>Aggiunta di informazioni a una Knowledge Base

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento vengono descritte le modalità mediante cui è possibile aggiungere informazioni a una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Prima che sia possibile eseguire operazioni relative alla qualità dei dati, è necessario disporre di informazioni in relazione ai dati stessi. Tali informazioni si acquisiscono compilando e gestendo una Data Quality Knowledge Base e aggiungendovi informazioni correlate a un tipo specifico di origine dati. La Knowledge Base è un repository di informazioni sui dati che consente di comprenderli e mantenerne l'integrità.  
  
 In essa sono contenuti domini di dati relativi all'origine dati. Per ogni dominio di dati, nella DQKB vengono archiviati tutti i termini identificati, gli errori di ortografia, le regole di convalida e di business e dati di riferimento che possono essere utilizzati per eseguire azioni relative alla qualità dei dati sull'origine dati. In DQS queste informazioni vengono utilizzate per identificare dati errati o non validi o per eseguire l'individuazione delle corrispondenze.  
  
 È possibile aggiungere informazioni a una Knowledge Base nelle seguenti modalità computerizzate o interattive.  
  
-   [Esecuzione dell'individuazione di informazioni](#Discovery)  
  
-   [Gestione dei valori dei dati in un dominio](#ManageDomain)  
  
-   [Importazione di informazioni da un file DQS](#DQSFile)  
  
-   [Importazione di informazioni da un file di Excel](#Excel)  
  
-   [Re-importazione di informazioni da un progetto nella Knowledge Base](#Project)  
  
-   [Utilizzo della Knowledge Base DQS predefinita](#Default)  
  
##  <a name="Discovery"></a> Esecuzione dell'individuazione di informazioni  
 L'individuazione delle informazioni consente di analizzare un esempio di dati per stabilire i criteri di qualità, quindi di aggiungere le informazioni acquisite alla Knowledge Base. Si tratta di un processo computerizzato che identifica le incoerenze e gli errori di sintassi, proponendo modifiche ai dati. L'attività di individuazione delle informazioni è una procedura guidata che include una pagina in cui è possibile gestire i valori di dominio in modo interattivo.  
  
-   Per ulteriori informazioni, vedere [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
-   Per un video in cui si dimostra come eseguire l'individuazione delle informazioni, fare clic [qui](https://msdn.microsoft.com/sqlserver/hh323825.aspx).  
  
##  <a name="ManageDomain"></a> Gestione dei valori dei dati in un dominio  
 DQS consente di modificare e aumentare in modo interattivo i metadati generati dall'attività di individuazione delle informazioni computerizzata. L'operazione viene eseguita nell'attività di gestione del dominio, dove è possibile applicare una modifica a un valore dei dati specifico.  
  
-   Per ulteriori informazioni, vedere [Change Domain Values](../data-quality-services/change-domain-values.md).  
  
-   Per un video in cui si dimostra come eseguire la gestione di un dominio, fare clic [qui](https://msdn.microsoft.com/sqlserver/hh323825.aspx). Si noti che in questo video si modificano i valori di dominio nella pagina di gestione dei valori di dominio della procedura guidata relativa all'individuazione delle informazioni. È inoltre possibile eseguire questi passaggi nella pagina Valori di dominio dell'attività di gestione del dominio.  
  
##  <a name="DQSFile"></a> Importazione di informazioni da un file DQS  
 È possibile importare un dominio da un file dqs in una Knowledge Base esistente oppure importare una Knowledge Base intera da un file dqs in una nuova Knowledge Base. A tale scopo, è prima necessario esportare un dominio o Knowledge Base esistente in un file dqs. Un file dqs che contiene un dominio include tutti i dati del dominio; un file dqs che contiene una Knowledge Base conterrà tutte le informazioni sulla Knowledge Base, inclusi i domini e i criteri di corrispondenza.  
  
-   Per altre informazioni, vedere [Importare un dominio da un file DQS](../data-quality-services/import-a-domain-from-a-dqs-file.md) o [Importare una Knowledge Base da un file DQS](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md).  
  
##  <a name="Excel"></a> Importazione di informazioni da un file di Excel  
 È possibile importare valori di dominio da un foglio di calcolo di Excel in un dominio o Knowledge Base esistente. A tale scopo, è necessario prima creare un foglio di calcolo di Excel con i valori di dominio da importare e assicurarsi che Excel sia installato nel computer [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] per essere in grado di importare valori utilizzando [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Non è possibile esportare valori di dominio da un dominio o Knowledge Base a un file di Excel.  
  
-   Per altre informazioni nella documentazione, vedere [Importare i valori da un file di Excel in un dominio](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md) o [Importare i domini da un file di Excel in Individuazione informazioni](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md).  
  
##  <a name="Project"></a> Re-importazione di informazioni da un progetto nella Knowledge Base  
 Dopo aver eseguito un progetto di pulizia o di qualità dei dati corrispondenti utilizzando una Knowledge Base, è possibile re-importare le informazioni create durante la pulizia o l'individuazione delle corrispondenze nella Knowledge Base. Questo consente di conservare le informazioni generate durante il progetto e di continuare l'aggiunta di informazioni alla Knowledge Base.  
  
-   Per altre informazioni, vedere [Importare i valori di un progetto di pulizia in un dominio](../data-quality-services/import-cleansing-project-values-into-a-domain.md).  
  
##  <a name="Default"></a> Utilizzo della Knowledge Base DQS predefinita  
 In DQS è disponibile una Knowledge Base precompilata denominata DQS Data che contiene domini con dati relativi nomi e indirizzi di società statunitensi. Questa Knowledge Base può essere utilizzata per avviare rapidamente un progetto senza creare una nuova Knowledge Base. La Knowledge Base DQS Data è di sola lettura, ma l'amministratore dei dati può creare una nuova Knowledge Base basandosi su di essa.  
  
-   Per ulteriori informazioni, vedere [Using the DQS Default Knowledge Base](../data-quality-services/using-the-dqs-default-knowledge-base.md).  
  
  
