---
title: Editor origine ODBC (pagina colonne) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5bfda61e5a57dabd62289f32d04d6367695b070b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057165"
---
# <a name="odbc-source-editor-columns-page"></a>Editor origine ODBC (pagina Colonne)
  Usare la pagina **Colonne** della finestra di dialogo **Editor origine ODBC** per eseguire il mapping tra una colonna di output e ogni colonna esterna (di origine).  
  
 Per ulteriori informazioni sull'origine ODBC, vedere [ODBC Source](data-flow/odbc-source.md).  
  
## <a name="task-list"></a>Elenco attività  
 **Per aprire ODBC Source Editor (pagina Colonne)**  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] che contiene l'origine ODBC.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine ODBC.  
  
3.  In **ODBC Source Editor**, fare clic su **Colonne**.  
  
## <a name="options"></a>Opzioni  
  
### <a name="available-external-columns"></a>Colonne esterne disponibili  
 Elenco delle colonne esterne disponibili nell'origine dei dati. Non è possibile utilizzare questa tabella per l'aggiunta o l'eliminazione di colonne. Selezionare le colonne da utilizzare dall'origine. Le colonne scelte vengono aggiunte all'elenco **Colonna esterna** nell'ordine in cui vengono selezionate.  
  
 Selezionare la casella di controllo **Seleziona tutto** per selezionare tutte le colonne.  
  
### <a name="external-column"></a>Colonna esterna  
 Una vista delle colonne esterne (di origine) nell'ordine in cui vengono presentate durante la configurazione di componenti che utilizzano i dati dell'origine ODBC.  
  
### <a name="output-column"></a>Colonna di output  
 Consente di immettere un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco. Il nome immesso viene visualizzato in Progettazione SSIS.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor origine ODBC &#40;pagina Output degli errori&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
