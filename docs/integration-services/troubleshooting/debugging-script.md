---
title: Debug degli script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Script task [Integration Services], debugging
- debugging [Integration Services], scripts
- scripts [Integration Services], debugging
ms.assetid: fddf57d8-8607-4f88-85a0-1b683087b491
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a8dee34e6d2bb7cfb858ee1f10378d5ac4916f9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945574"
---
# <a name="debugging-script"></a>Debug degli script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Gli script utilizzati nell'attività e nel componente Script vengono scritti in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA).  
  
 VSTA consente di impostare punti di interruzione negli script. I punti di interruzione possono essere gestiti in VSTA o tramite la finestra di dialogo **Imposta punti di interruzione** disponibile in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Per altre informazioni, vedere [Debug del flusso di controllo](../../integration-services/troubleshooting/debugging-control-flow.md).  
  
 Nella finestra di dialogo **Imposta punti di interruzione** sono inclusi i punti di interruzione degli script. Tali punti di interruzione vengono visualizzati nella parte inferiore dell'elenco dei punti di interruzione, insieme al numero di riga e al nome della funzione in cui sono stati impostati. È possibile eliminare un punto di interruzione di uno script dalla finestra di dialogo **Imposta punti di interruzione** .  
  
 In fase di esecuzione i punti di interruzione impostati per le righe di codice nello script vengono integrati con quelli impostati per il pacchetto o le attività e i contenitori inclusi nel pacchetto. È possibile eseguire il debugger da un punto di interruzione in uno script a un punto di interruzione impostato per un pacchetto, un'attività o un contenitore e viceversa. Si considerino ad esempio un pacchetto in cui sono impostati punti di interruzione per le condizioni di interruzione che si verificano quando il pacchetto riceve gli eventi **OnPreExecute** e **OnPostExecute** e un'attività Script con punti di interruzione impostati per le righe dello script incluso. In questo scenario tramite il pacchetto è possibile sospendere l'esecuzione in corrispondenza della condizione di interruzione associata all'evento **OnPreExecute** , continuare l'esecuzione fino ai punti di interruzione impostati nello script e infine continuare l'esecuzione fino alla condizione di interruzione associata all'evento **OnPostExecute** .  
  
 Per altre informazioni sul debug dell'attività e sul componente Script, vedere [Scrittura di codice e debug dell'attività Script](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) e [Codifica e debug del componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-visual-studio-for-applications"></a>Per impostare un punto di interruzione in Visual Studio for Applications  
  
-   [Eseguire il debug di uno script impostando punti di interruzione in un'attività e in un componente Script](../../integration-services/extending-packages-scripting/debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi relativi agli strumenti per lo sviluppo dei pacchetti](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  
