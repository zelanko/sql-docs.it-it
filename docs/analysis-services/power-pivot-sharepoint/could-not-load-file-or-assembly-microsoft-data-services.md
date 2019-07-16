---
title: Impossibile caricare il file o l'assembly Microsoft-Data-Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9472fffb790d8d18ced8d2a528011927717aabc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164163"
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>Impossibile caricare il file o l'assembly Microsoft-Data-Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Negli ambienti SharePoint 2010 in cui è disponibile [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint questo errore si verifica se si prova un'esportazione del feed di dati e nel sistema non è installata la versione richiesta di Microsoft ADO.NET Data Services.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Applicabile a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Impossibile trovare ADO.NET Data Services 3.5 SP1.|  
|Testo del messaggio|Impossibile caricare il file o l'assembly "Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral PublicKeyToken=b77a5c561934e089" o una delle relative dipendenze. Impossibile trovare il file specificato|  
  
## <a name="explanation"></a>Spiegazione  
 In SharePoint 2010 è incluso un pulsante Esporta come feed di dati che può essere utilizzato per esportare un elenco SharePoint come feed di dati XML. Inoltre, sia Reporting Services in modalità SharePoint sia [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint supportano le funzionalità dei feed di dati che richiedono ADO.NET Data Services.  
  
 Se ADO.NET Data Services non è installato, questo errore si verificherà quando si richiede un feed di dati.  
  
## <a name="user-action"></a>Azione dell'utente  
  
1.  La documentazione di requisiti hardware e software per SharePoint 2010, andare [determinare requisiti Hardware e Software (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  Nella sezione relativa ai **prerequisiti software di installazione**cercare il collegamento per ADO.NET Data Services 3.5 che corrisponde al sistema operativo in uso.  
  
3.  Fare clic sul collegamento ed eseguire il programma di installazione che consente di installare il servizio.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire soluzioni PowerPivot in SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
