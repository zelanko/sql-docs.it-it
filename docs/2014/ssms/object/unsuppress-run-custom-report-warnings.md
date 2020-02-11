---
title: Visualizzare gli avvisi relativi all'esecuzione di report personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 0deed900-c910-4d12-aac0-6ab9e39eb068
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ed653b16fe524f364ba89f13e00715b725080033
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62824395"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Visualizzazione di avvisi relativi all'esecuzione di report personalizzati
  Per i report personalizzati sono disponibili due finestre di dialogo di avviso. In questo argomento vengono descritte le modalità per consentire la visualizzazione delle caselle in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Per impostazione predefinita, prima dell'esecuzione di un report personalizzato viene visualizzata la finestra di dialogo **Esegui report personalizzato** . Se si seleziona la casella di controllo **Non visualizzare più questo avviso** , la finestra di dialogo non verrà più visualizzata. Per impostazione predefinita, la finestra di dialogo **Esegui report personalizzato** viene visualizzata anche quando si apre un report personalizzato e quindi si fa clic su un collegamento a un altro report personalizzato. La finestra di dialogo contiene il percorso del file di report personalizzato drill-through. Se si seleziona la casella di controllo **Non visualizzare più questo avviso** , la finestra di dialogo non verrà più visualizzata.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Per consentire la visualizzazione della finestra di dialogo di avviso relativa al report personalizzato principale  
  
1.  Connetti all' \< **>\\<*unità* \\ \>di*condivisione*>|server\<> \Documents and Settings<UserProfile \Dati Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.XML.  
  
2.  Fare clic con `reports.xml`il pulsante destro del mouse e quindi scegliere **modifica**.  
  
3.  Modificare**\<SuppressWarning>true\</SuppressWarning> \<SuppressWarning>false\</SuppressWarning>**.  
  
4.  Riavviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Per consentire la visualizzazione della finestra di dialogo di avviso relativa al report personalizzato drill-through  
  
1.  Connetti all' \< **>\\<*unità* \\ \>di*condivisione*>|server\<> \Documents and Settings<UserProfile \Dati Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.XML.  
  
2.  Fare clic con `reports.xml`il pulsante destro del mouse e scegliere **modifica**.  
  
3.  Modificare ** \<SuppressDrillthroughWarning>true\</SuppressDrillthroughWarning>\<SuppressDrillthroughWarning>false\</SuppressDrillthroughWarning>**.  
  
4.  Riavviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Report personalizzati in Management Studio](custom-reports-in-management-studio.md)   
 [Aggiungere un report personalizzato a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usare report personalizzati con proprietà dei nodi di Esplora oggetti](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
