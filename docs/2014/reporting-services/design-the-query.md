---
title: Progettare la query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptwizard.designquery.f1
ms.assetid: 2dad800f-10a1-453c-8761-2935b9826d84
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f09964013bdc8675e5d4701bd86421317c33fc97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109288"
---
# <a name="design-the-query"></a>Progettazione query
  Utilizzare questa pagina della Creazione guidata report per creare una query immettendola manualmente, utilizzando Generatore query per compilare una query in modo interattivo o importando la query da un altro report.  
  
 Il tipo di origine dati selezionato nella pagina Selezione origine dati, una pagina precedente della Creazione guidata report, determina la query che è possibile immettere in questa pagina. Se, ad esempio, il tipo di origine [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]dati è, è [!INCLUDE[tsql](../includes/tsql-md.md)] possibile immettere istruzioni o nomi di stored procedure. Se il tipo di origine dati [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]è, il riquadro query è disabilitato e non è possibile immettere una query direttamente. È possibile specificare la query utilizzando Generatore di query.  
  
## <a name="options"></a>Opzioni  
 **Stringa di query**  
 Consente di digitare una query che recupera i dati da utilizzare nel report.  
  
 **Generatore di query**  
 Fare clic su **Generatore di query** per aprire una finestra Progettazione query per l'origine dati o importare una query da un altro report.  
  
 Per ulteriori informazioni sugli strumenti di progettazione query, vedere [Reporting Services Query Designers](../../2014/reporting-services/reporting-services-query-designers.md).  
  
## <a name="example"></a>Esempio  
 Per il tipo di origine dati **Microsoft SQL Server**, la query seguente recupera un elenco di cognomi dalla [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] tabella `Person` di database.  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 Per il tipo di origine dati **Microsoft SQL Server**, la query seguente esegue [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] il `uspGetEmployeeManagers` stored procedure per il dipendente con numero di identificazione 1:  
  
```  
EXEC uspgetEmployeeManagers '1';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida della creazione guidata report](../../2014/reporting-services/report-wizard-help.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Aggiungere dati a un report &#40;Generatore report e SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
