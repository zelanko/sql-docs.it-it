---
title: Eseguire un file script di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- scripts [Reporting Services], running
ms.assetid: 0de4995c-85ec-4d4c-aaef-fbd30edfb20f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8d4023d5fb434f58fd031e6512f3fa84fa551fec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200972"
---
# <a name="run-a-reporting-services-script-file"></a>Eseguire un file script di Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - I file script vengono eseguiti dal prompt dei comandi usando l'ambiente di script di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (RS.exe). RS.exe dispone di molti argomenti del prompt dei comandi disponibili per l'utilizzo. Per altre informazioni sulle opzioni del prompt dei comandi, vedere [Utilità RS.exe &#40;SSRS&#41;](rs-exe-utility-ssrs.md). Per altri esempi di script, vedere [SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
## <a name="sample-command-lines"></a>Esempi di righe di comando  
  
-   Eseguire Script.rss nell'ambiente di script che definisce il server di report di destinazione. Per impostazione predefinita, viene applicata l'autenticazione di Windows:  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver  
    ```  
  
-   Eseguire Script.rss nell'ambiente di script che specifica un nome utente e una password per l'autenticazione delle chiamate al servizio Web:  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -u myusername -p mypassword  
    ```  
  
-   Eseguire Script.rss nell'ambiente di script che specifica un timeout del server di 30 secondi:  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -l 30  
    ```  
  
-   Eseguire Script.rss nell'ambiente di script che specifica una variabile globale degli script denominata *report*.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -v report="Company Sales"  
    ```  
  
-   Eseguire Script.rss nell'ambiente di script che specifica che le operazioni del servizio Web nel file script vengono eseguite come batch.  
  
    ```  
    rs -i Script.rss -s http://servername/reportserver -b  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento tecnico &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
