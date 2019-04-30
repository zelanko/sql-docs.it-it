---
title: Debug del codice di un'estensione per l'elaborazione dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: adecc79256f49aeca9532e50119675515b9939dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164362"
---
# <a name="debugging-data-processing-extension-code"></a>Debug del codice di un'estensione per l'elaborazione dati
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sono disponibili diversi strumenti di debug che consentono di analizzare il codice delle estensioni per l'elaborazione dati e di individuare gli errori. Gli strumenti più appropriati da utilizzare variano in base alla finalità desiderata. In questo esempio viene utilizzato [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>Per eseguire il debug del codice di un'estensione per l'elaborazione dati  
  
1.  Avviare [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] e aprire il progetto di estensione per l'elaborazione dati.  
  
2.  Compilare il progetto e distribuire l'assembly di estensioni per l'elaborazione dati e il file con estensione pdb associato in Gestione report. Per altre informazioni sulla distribuzione, vedere [come: Distribuire un'estensione di elaborazione dei dati in Progettazione Report](deploying-a-data-processing-extension-to-report-designer.md).  
  
3.  Aprire un nuovo progetto report in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] lasciando aperto il codice dell'estensione per l'elaborazione dati in una finestra separata di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
4.  Passare alla finestra di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] che contiene il progetto di estensione per l'elaborazione dati e impostare alcuni punti di interruzione nel codice.  
  
5.  Con la finestra del progetto di estensione per l'elaborazione dati ancora attiva, scegliere **Connetti a processo** dal menu **Debug**.  
  
     Verrà visualizzata la finestra di dialogo **Connetti a processo**.  
  
6.  Nell'elenco di processi selezionare il processo devenv.exe che corrisponde al progetto report e fare clic su **Connetti**.  
  
7.  Definire l'origine dati del report usando la scheda **Dati report** del progetto report. In genere, si utilizza lo strumento generico Progettazione query per eseguire una query sull'origine dati personalizzata. In questo modo, è possibile richiamare il debugger ed eseguire il codice in corrispondenza dei punti di interruzione.  
  
8.  Esaminare il codice istruzione per istruzione premendo F11 Per ulteriori informazioni sull'utilizzo di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] per eseguire il debug, vedere la documentazione di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di un'estensione per l'elaborazione dati](deploying-a-data-processing-extension.md)   
 [Estensioni di Reporting Services](../reporting-services-extensions.md)   
 [Implementazione di un'estensione per l'elaborazione dati](implementing-a-data-processing-extension.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
