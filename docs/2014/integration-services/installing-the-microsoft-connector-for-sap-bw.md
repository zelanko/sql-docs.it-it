---
title: Installazione di Microsoft Connector per 1,1 SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3bfb9023-9597-4f59-9085-4b9057e7702e
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ae4c48d26814b606b4be18ae0c0c21c73f8bf6b1
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968291"
---
# <a name="installing-the-microsoft-connector-for-11-sap-bw"></a>Installazione di Microsoft Connector 1.1 for SAP BW
  Per installare il [!INCLUDE[msCoName](../includes/msconame-md.md)] connettore 1,1 per SAP BW e la relativa documentazione, scaricare ed eseguire il pacchetto di Windows Installer dalla pagina Web SQL Server Feature Pack.  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
## <a name="required-sap-files"></a>File SAP richiesti  
 Per usare il [!INCLUDE[msCoName](../includes/msconame-md.md)] connettore 1,1 per SAP BW, non è necessario installare il software front-end SAP (SAP GUI) nel computer locale.  
  
 È tuttavia necessario copiare il file del connettore SAP .NET, librfc32.dll, nella sottocartella di sistema nella cartella Windows. In genere, il percorso di questa cartella è **C:\Windows\system32**.  
  
## <a name="considerations-for-64-bit-computers"></a>Considerazioni relative ai computer a 64 bit  
 Il [!INCLUDE[msCoName](../includes/msconame-md.md)] connettore 1,1 per SAP BW supporta completamente la versione a 64 bit di [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. In un computer a 64 bit, il [!INCLUDE[msCoName](../includes/msconame-md.md)] connettore 1,1 per SAP BW presenta i requisiti aggiuntivi seguenti:  
  
-   Per eseguire pacchetti in modalità a 64 bit in qualsiasi sistema operativo Windows a 64 bit, copiare la versione a 64 bit del file SAP GUI, librfc32.dll, nella cartella **system32** della cartella Windows. In genere, il percorso di questo file è **C:\Windows\system32**.  
  
-   Per eseguire pacchetti in modalità a 32 bit in qualsiasi sistema operativo Windows a 64 bit, copiare la versione del file SAP GUI, librfc32.dll, nella cartella **SysWow64** della cartella Windows. In genere, il percorso di questa cartella è **C:\Windows\SysWow64**.  
  
  
