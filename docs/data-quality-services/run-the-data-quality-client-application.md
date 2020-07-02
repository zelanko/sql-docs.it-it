---
title: Eseguire l'applicazione client Data Quality
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
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 7179387d5ae3d2dd045332d0dd5d0fad7fcdebd8
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813768"
---
# <a name="run-the-data-quality-client-application"></a>Eseguire l'applicazione client Data Quality

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Eseguire il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e accedere a un [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 È necessario aver completato l'installazione di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] tramite l'esecuzione del file DQSInstaller.exe. Per altre informazioni, vedere [Eseguire DQSInstaller.exe per completare l'installazione del server DQS](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per potere accedere al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], è necessario disporre di uno dei tre ruoli DQS (dqs_adminstrator, dqs_kb_editor o dqs_kb_operator) concessi per il database DQS_MAIN.  
  
##  <a name="run-data-quality-client"></a><a name="Run"></a>Esegui Data Quality Client  
 Per eseguire il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] nel computer in cui è stato installato:  
  
1.  Fare clic su **Start**, puntare **Tutti i programmi**, fare clic su **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, su **Data Quality Services**, quindi su **Client Data Quality**.  
  
2.  Nella finestra di dialogo **Connetti al server** :  
  
    1.  Specificare il server a cui si desidera connettere l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Selezionare **(LOCAL)** per connettersi al [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] nel computer locale. È anche possibile fare clic sulla freccia in giù e selezionare **\<Browse network for more servers>** per connettersi a un server diverso (o per connettersi al server locale in base al nome). Verrà visualizzata la finestra di dialogo **Cerca server** . È possibile selezionare un server nella scheda **Server locali** o nella scheda **Server di rete** .  
  
    2.  Per crittografare il trasferimento dei dati tra [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], fare clic su **Opzioni**e quindi selezionare la casella di controllo **Crittografa connessione** .  
  
3.  Fare clic su **Connetti**.  
  
 Verrà visualizzata la schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Per altre informazioni, vedere [Schermata iniziale del client Data Quality](../data-quality-services/data-quality-client-home-screen.md).  
  
  
