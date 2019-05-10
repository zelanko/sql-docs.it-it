---
title: Caricare dati da MDS in Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbe1188773d0770ff345cd54ea47e03a3c05555f
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482709"
---
# <a name="load-data-from-mds-into-excel"></a>Caricare i dati da MDS in Excel
  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], è necessario caricare i dati dal repository MDS per utilizzarli.  
  
 Se si desidera filtrare il set di dati prima del caricamento, vedere [filtrare i dati prima del caricamento &#40;il componente aggiuntivo MDS per Excel&#41; ](filter-data-before-exporting-mds-add-in-for-excel.md) alternativa.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione per accedere all'area funzionale **Esplora** .  
  
### <a name="to-load-data-from-mds-into-excel"></a>Per caricare i dati da MDS in Excel  
  
1.  Aprire Excel e nella scheda **Dati master** connettersi a un repository MDS. Per altre informazioni, vedere [Connettersi a un repository MDS &#40;componente aggiuntivo MDS per Excel&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md).  
  
2.  Nel riquadro **Esplora dati master** selezionare un modello e una versione. L'elenco di entità viene popolato.  
  
    -   Se il riquadro **Esplora dati master** non è visibile, nel gruppo **Connetti e carica** fare clic su **Esplora dati master**.  
  
    -   Se il riquadro **Esplora dati master** è disabilitato, significa che il foglio esistente contiene già i dati gestiti da MDS. Per abilitare il riquadro, aprire un nuovo foglio di lavoro.  
  
3.  Nel riquadro **Esplora dati master** nell'elenco di entità fare doppio clic sull'entità che si vuole caricare.  
  
    > [!NOTE]  
    >  -   Solo il primo milione di membri viene caricato in Excel. Per filtrare l'elenco prima di caricarlo, sulla barra multifunzione del gruppo **Connetti e carica** fare clic su **Filtro**.  
    > -   Nelle colonne che sono elenchi vincolati (attributi basati su dominio) vengono caricati solo i primi 25.000 valori. È possibile modificare questo numero nella proprietà MaximumDbaEntitySize nel file excelusersettings.config che si trova nel computer in cui è installato Excel. Questo file si trova in C:\Users\\< utente\>\AppData\Local\Microsoft\Microsoft SQL Server\120\MasterDataServices\\.  
  
    > [!NOTE]  
    >  Quando si caricano dati delimitati da testo usando il componente aggiuntivo per Microsoft Excel con Excel a 32 bit e le impostazioni per le proprietà relative al **numero di celle da caricare** e al **numero di celle da pubblicare** sono entrambe impostate sul valore massimo 1000, si verificherà un errore di memoria insufficiente. È necessario usare Excel a 64 bit per usare le impostazioni massime per le due proprietà relative al **numero di celle da caricare** e al **numero di celle da pubblicare**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Pubblicare dati da Excel a MDS &#40;componente aggiuntivo MDS per Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Il caricamento dei dati &#40;componente aggiuntivo MDS per Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [Finestra di dialogo Filtro &#40;componente aggiuntivo MDS per Excel&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [Pubblicazione di dati &#40;componente aggiuntivo MDS per Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
