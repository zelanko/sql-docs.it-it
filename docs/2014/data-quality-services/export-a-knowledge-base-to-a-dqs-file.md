---
title: Esportare una Knowledge Base in un file DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1d1b2e20347cafb4717880de8fd224950f76b036
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480729"
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>Esportazione di una Knowledge Base in un file DQS
  In questo argomento viene descritto come esportare un'intera Knowledge Base in un file di dati con estensione DQS in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). È possibile esportare un dominio o una Knowledge Base intera in un file di dati. Per informazioni sull'esportazione di un dominio, vedere [Esportare un dominio in un file DQS](../../2014/data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
 L'esportazione di una Knowledge Base in un file con estensione DQS e la successiva importazione in un'altra Knowledge Base semplifica il processo di generazione delle informazioni e consente di risparmiare tempo e impegno. La procedura permette di condividere una Knowledge Base e le relative informazioni con altri utenti. Il file DQS conterrà tutte le informazioni della Knowledge Base, compresi domini e i criteri di corrispondenza, tranne le informazioni sui dati di riferimento collegati. È necessario collegare nuovamente i domini richiesti ai servizi dati di riferimento appropriati, se necessario, dopo avere importato il file DQS. Vengono esportati sia i dati pubblicati che quelli non pubblicati in una Knowledge Base.  
  
 Il file di dati DQS creato dal processo di esportazione viene crittografato, pertanto non è possibile visualizzarne i contenuti.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per esportare una Knowledge Base in un file di dati DQS, è necessario avere creato e aperto una Knowledge Base. Non è necessario disporre di un file DQS in cui esportare, in quanto verrà creato automaticamente.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per esportare una Knowledge Base da un file DQS è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="export-a-knowledge-base-to-a-dqs-file"></a><a name="Export"></a>Esportare una Knowledge base in un file DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire una Knowledge Base nell'attività Gestione dominio.  
  
3.  Nella pagina Gestione dominio (con qualsiasi scheda selezionata), fare clic sull'icona **Esporta dati Knowledge Base** sopra l'elenco di domini, quindi fare clic su **Esporta Knowledge Base**. In alternativa, è possibile fare clic con il pulsante destro del mouse sull'elenco **Dominio** , selezionare **Esporta**, quindi fare clic su **Esporta Knowledge Base**.  
  
4.  Nella finestra di dialogo **Esporta in file di dati** spostarsi nella cartella in cui si vuole salvare il file, denominare il file o mantenere il nome della Knowledge Base, mantenere **File di dati DQS (\*.dqs)** in **Salva come** e fare clic su **Salva**.  
  
5.  Nella finestra di dialogo **Esporta Knowledge Base** verificare che la riga dello stato indichi che l'esportazione è stata completata. Fare clic su **OK**.  
  
##  <a name="follow-up-after-exporting-a-domain-to-a-dqs-file"></a><a name="FollowUp"></a>Completamento: dopo l'esportazione di un dominio in un file DQS  
 Una volta esportata una Knowledge Base in un file DQS, è possibile importarla nello stesso [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (con un nuovo nome) o in un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]diverso.  
  
  
