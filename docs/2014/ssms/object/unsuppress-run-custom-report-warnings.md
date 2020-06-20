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
ms.openlocfilehash: ae7f4d08ac613113d715728a5cb78ae37bd6f99b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058532"
---
# <a name="unsuppress-run-custom-report-warnings"></a>Visualizzazione di avvisi relativi all'esecuzione di report personalizzati
  Per i report personalizzati sono disponibili due finestre di dialogo di avviso. In questo argomento vengono descritte le modalità per consentire la visualizzazione delle caselle in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Per impostazione predefinita, prima dell'esecuzione di un report personalizzato viene visualizzata la finestra di dialogo **Esegui report personalizzato** . Se si seleziona la casella di controllo **Non visualizzare più questo avviso** , la finestra di dialogo non verrà più visualizzata. Per impostazione predefinita, la finestra di dialogo **Esegui report personalizzato** viene visualizzata anche quando si apre un report personalizzato e quindi si fa clic su un collegamento a un altro report personalizzato. La finestra di dialogo contiene il percorso del file di report personalizzato drill-through. Se si seleziona la casella di controllo **Non visualizzare più questo avviso** , la finestra di dialogo non verrà più visualizzata.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-unsuppress-the-main-custom-report-warning-dialog-box"></a>Per consentire la visualizzazione della finestra di dialogo di avviso relativa al report personalizzato principale  
  
1.  Connettersi a \<*Server*> \\ < *Condividi* >| \<*Drive*> \Documents and Settings \\<UserProfile \> \Dati Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Fare clic con il pulsante destro del mouse `reports.xml` e quindi scegliere **modifica**.  
  
3.  Modificare** \<SuppressWarning> true \</SuppressWarning> in \<SuppressWarning> false \</SuppressWarning> **.  
  
4.  Riavviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-unsuppress-the-drill-through-custom-report-warning-dialog-box"></a>Per consentire la visualizzazione della finestra di dialogo di avviso relativa al report personalizzato drill-through  
  
1.  Connettersi a \<*Server*> \\ < *Condividi* >| \<*Drive*> \Documents and Settings \\<UserProfile \> \Dati Data\Microsoft\Microsoft SQL Server\120\Tools\Shell\reports.xml.  
  
2.  Fare clic con il pulsante destro del mouse `reports.xml` e scegliere **modifica**.  
  
3.  Modificare ** \<SuppressDrillthroughWarning> true \</SuppressDrillthroughWarning> in \<SuppressDrillthroughWarning> false \</SuppressDrillthroughWarning> **.  
  
4.  Riavviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Report personalizzati in Management Studio](custom-reports-in-management-studio.md)   
 [Aggiungere un report personalizzato a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Usare report personalizzati con proprietà dei nodi di Esplora oggetti](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
