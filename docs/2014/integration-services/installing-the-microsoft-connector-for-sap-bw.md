---
title: Installazione di Microsoft Connector 1.1 for SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e43a45f9b21e631638dec43a8a126b4f007429d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394354"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>Installazione di Microsoft Connector 1.1 for SAP BW
  Per installare il [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW e la relativa documentazione, scaricare ed eseguire il pacchetto di Windows installer dalla pagina Web Feature Pack di SQL Server.  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
## <a name="required-sap-files"></a>File SAP richiesti  
 Usare il [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW, non è necessario installare il software Front-End SAP (SAP GUI) nel computer locale.  
  
 È tuttavia necessario copiare il file del connettore SAP .NET, librfc32.dll, nella sottocartella di sistema nella cartella Windows. In genere, il percorso di questa cartella è **C:\Windows\system32**.  
  
## <a name="considerations-for-64-bit-computers"></a>Considerazioni relative ai computer a 64 bit  
 Il [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW supporta completamente la versione a 64 bit di [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. In un computer a 64 bit, il [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector 1.1 for SAP BW prevede i requisiti aggiuntivi seguenti:  
  
-   Per eseguire pacchetti in modalità a 64 bit in qualsiasi sistema operativo Windows a 64 bit, copiare la versione a 64 bit del file SAP GUI, librfc32.dll, nella cartella **system32** della cartella Windows. In genere, il percorso di questo file è **C:\Windows\system32**.  
  
-   Per eseguire pacchetti in modalità a 32 bit in qualsiasi sistema operativo Windows a 64 bit, copiare la versione del file SAP GUI, librfc32.dll, nella cartella **SysWow64** della cartella Windows. In genere, il percorso di questa cartella è **C:\Windows\SysWow64**.  
  
  
