---
title: Esportazione di un dominio in un file DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 518b393b296425c1aaf54229a8a843576c6a628a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75251621"
---
# <a name="export-a-domain-to-a-dqs-file"></a>Esportazione di un dominio in un file DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come esportare un dominio in un file DQS [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). È possibile esportare un dominio o una Knowledge Base intera in un file di dati. Per informazioni sull'esportazione di una Knowledge Base, vedere [Esportare una Knowledge Base in un file DQS](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 L'esportazione di un dominio da una Knowledge Base a un file di dati DQS e la successiva importazione in un'altra semplifica il processo di generazione delle informazioni e consente di risparmiare tempo e impegno. La procedura permette di condividere un dominio e la relativa Knowledge Base con altri utenti.  
  
 È possibile esportare un dominio singolo o composito. Un file DQS contenente un singolo dominio include tutti i dati del dominio stesso tra cui le proprietà, i valori e le regole, tranne le informazioni sui dati di riferimento collegati. Un file DQS che contiene un dominio composito include tutti i dati di tale dominio, compresi i dati dei domini singoli contenuti al suo interno, nonché le proprietà, le relazioni e le regole del dominio composito stesso, tranne le informazioni sui dati di riferimento. È necessario collegare il dominio o il dominio composito nuovamente ai servizi dati di riferimento appropriati, se necessario, dopo avere importato il file DQS. Vengono esportati sia i dati pubblicati che quelli non pubblicati.  
  
 Il file di dati DQS creato dal processo di esportazione viene crittografato, pertanto non è possibile visualizzarne i contenuti.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Per esportare un dominio in un file di dati DQS, è necessario avere creato e selezionato un dominio singolo o composito contenente più domini singoli. Non è necessario disporre di un file DQS in cui esportare, in quanto verrà creato automaticamente.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per esportare un dominio in un file DQS è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="export-a-domain-to-a-dqs-file"></a><a name="Export"></a>Esportare un dominio in un file DQS  
 È possibile esportare da qualsiasi pagina Gestione dominio. Il comando di esportazione è disponibile sia da un controllo nell'interfaccia utente che da un comando nel menu di scelta rapida del riquadro Elenco domini.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] aprire una Knowledge Base nell'attività Gestione dominio.  
  
3.  Nella pagina **Gestione dominio** (con qualsiasi scheda selezionata), selezionare un dominio singolo nell'elenco **Dominio** .  
  
4.  Fare clic sull'icona **Esporta dati Knowledge Base** sopra l'elenco di domini, quindi fare clic su **Esporta dominio**. In alternativa, è possibile fare clic con il pulsante destro del mouse sul dominio nell'elenco **Dominio** , selezionare **Esporta**, quindi fare clic su **Esporta dominio**.  
  
5.  Nella finestra di dialogo **Esporta in file di dati** spostarsi nella cartella in cui si vuole salvare il file, denominare il file o mantenere il nome predefinito, mantenere **File di dati DQS (\*.dqs)** in **Salva come** e fare clic su **Salva**.  
  
6.  Nella finestra di dialogo **Esporta dominio** verificare che la riga dello stato indichi che l'esportazione è stata completata. Fare clic su **OK**.  
  
##  <a name="follow-up-after-exporting-a-domain-to-a-dqs-file"></a><a name="FollowUp"></a>Completamento: dopo l'esportazione di un dominio in un file DQS  
 Dopo avere esportato un dominio in un file DQS, è possibile importare il dominio in un'altra Knowledge Base.  
  
  
