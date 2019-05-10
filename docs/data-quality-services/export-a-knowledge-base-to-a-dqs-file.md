---
title: Esportare una Knowledge Base in un file DQS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 13a2805109787b96fd416422bb3f44dbbf512b17
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65487510"
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>Esportazione di una Knowledge Base in un file DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come esportare un'intera Knowledge Base in un file di dati con estensione DQS in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). È possibile esportare un dominio o una Knowledge Base intera in un file di dati. Per informazioni sull'esportazione di un dominio, vedere [Esportare un dominio in un file DQS](../data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
 L'esportazione di una Knowledge Base in un file con estensione DQS e la successiva importazione in un'altra Knowledge Base semplifica il processo di generazione delle informazioni e consente di risparmiare tempo e impegno. La procedura permette di condividere una Knowledge Base e le relative informazioni con altri utenti. Il file DQS conterrà tutte le informazioni della Knowledge Base, compresi domini e i criteri di corrispondenza, tranne le informazioni sui dati di riferimento collegati. È necessario collegare nuovamente i domini richiesti ai servizi dati di riferimento appropriati, se necessario, dopo avere importato il file DQS. Vengono esportati sia i dati pubblicati che quelli non pubblicati in una Knowledge Base.  
  
 Il file di dati DQS creato dal processo di esportazione viene crittografato, pertanto non è possibile visualizzarne i contenuti.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per esportare una Knowledge Base in un file di dati DQS, è necessario avere creato e aperto una Knowledge Base. Non è necessario disporre di un file DQS in cui esportare, in quanto verrà creato automaticamente.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per esportare una Knowledge Base da un file DQS è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="Export"></a> Esportare una knowledge base in un file DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire una Knowledge Base nell'attività Gestione dominio.  
  
3.  Nella pagina Gestione dominio (con qualsiasi scheda selezionata), fare clic sull'icona **Esporta dati Knowledge Base** sopra l'elenco di domini, quindi fare clic su **Esporta Knowledge Base**. In alternativa, è possibile fare clic con il pulsante destro del mouse sull'elenco **Dominio** , selezionare **Esporta**, quindi fare clic su **Esporta Knowledge Base**.  
  
4.  Nella finestra di dialogo **Esporta in file di dati** spostarsi nella cartella in cui si vuole salvare il file, denominare il file o mantenere il nome della Knowledge Base, mantenere **File di dati DQS (\*.dqs)** in **Salva come** e fare clic su **Salva**.  
  
5.  Nella finestra di dialogo **Esporta Knowledge Base** verificare che la riga dello stato indichi che l'esportazione è stata completata. Fare clic su **OK**.  
  
##  <a name="FollowUp"></a> Completamento: fasi successive all'esportazione di un dominio in un file con estensione dqs  
 Una volta esportata una Knowledge Base in un file DQS, è possibile importarla nello stesso [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (con un nuovo nome) o in un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]diverso.  
  
  
