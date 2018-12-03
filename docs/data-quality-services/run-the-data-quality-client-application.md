---
title: Eseguire l'applicazione Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a0ed4ad06e5e2db6594e467cbab392a75797289f
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616271"
---
# <a name="run-the-data-quality-client-application"></a>Eseguire l'applicazione client Data Quality

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Eseguire il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e accedere a un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 È necessario aver completato l'installazione di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] tramite l'esecuzione del file DQSInstaller.exe. Per altre informazioni, vedere [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per potere accedere al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], è necessario disporre di uno dei tre ruoli DQS (dqs_adminstrator, dqs_kb_editor o dqs_kb_operator) concessi per il database DQS_MAIN.  
  
##  <a name="Run"></a> Eseguire il client Data Quality  
 Per eseguire il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] nel computer in cui è stato installato:  
  
1.  Fare clic su **Start**, puntare **Tutti i programmi**, fare clic su **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, su **Data Quality Services**, quindi su **Client Data Quality**.  
  
2.  Nella finestra di dialogo **Connetti al server** :  
  
    1.  Specificare il server a cui si desidera connettere l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Selezionare **(LOCAL)** per connettersi al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] nel computer locale. È anche possibile fare clic sulla freccia in giù e selezionare **\<Cerca altri server nella rete>** per connettersi a un server diverso, o al server locale in base al nome. Verrà visualizzata la finestra di dialogo **Cerca server** . È possibile selezionare un server nella scheda **Server locali** o nella scheda **Server di rete** .  
  
    2.  Per crittografare il trasferimento dei dati tra [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], fare clic su **Opzioni**e quindi selezionare la casella di controllo **Crittografa connessione** .  
  
3.  Fare clic su **Connetti**.  
  
 Verrà visualizzata la schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Per altre informazioni, vedere [Schermata iniziale del client Data Quality](../data-quality-services/data-quality-client-home-screen.md).  
  
  
