---
title: Impossibile caricare il file o l'assembly &#39;Microsoft.Data.Services, Version = 3.5.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089&#39; o una delle relative dipendenze. Impossibile trovare il file specificato. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 81ed0f44-8782-462d-af8f-0ba5b975df27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49e2ce59b8662a8deaf47099c967355150dca201
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62749583"
---
# <a name="could-not-load-file-or-assembly-39microsoftdataservices-version3500-cultureneutral-publickeytokenb77a5c561934e08939-or-one-of-its-dependencies-the-system-cannot-find-the-file-specified"></a>Impossibile caricare il file o l'assembly &#39;Microsoft.Data.Services, Version = 3.5.0.0, Culture = neutral, PublicKeyToken = b77a5c561934e089&#39; o una delle relative dipendenze. Impossibile trovare il file specificato.
  Negli ambienti di SharePoint 2010 in cui è disponibile PowerPivot per SharePoint, questo errore si verificherà se si tenta un'esportazione del feed di dati e nel sistema non è presente la versione richiesta di Microsoft ADO.NET Data Services.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Si applica a|PowerPivot per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Impossibile trovare ADO.NET Data Services 3.5 SP1.|  
|Testo del messaggio|Impossibile caricare il file o l'assembly "Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral PublicKeyToken=b77a5c561934e089" o una delle relative dipendenze. Impossibile trovare il file specificato|  
  
## <a name="explanation"></a>Spiegazione  
 In SharePoint 2010 è incluso un pulsante Esporta come feed di dati che può essere utilizzato per esportare un elenco SharePoint come feed di dati XML. Inoltre, sia Reporting Services in modalità SharePoint sia PowerPivot per SharePoint supportano le funzionalità del feed di dati che richiedono ADO.NET Data Services.  
  
 Se ADO.NET Data Services non è installato, questo errore si verificherà quando si richiede un feed di dati.  
  
## <a name="user-action"></a>Azione dell'utente  
  
1.  La documentazione di requisiti hardware e software per SharePoint 2010, andare [determinare requisiti Hardware e Software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734) (https://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  Nella sezione relativa ai **prerequisiti software di installazione**cercare il collegamento per ADO.NET Data Services 3.5 che corrisponde al sistema operativo in uso.  
  
3.  Fare clic sul collegamento ed eseguire il programma di installazione che consente di installare il servizio.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire soluzioni PowerPivot in SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
