---
title: Creare un'entità (componente aggiuntivo MDS per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d354abb3-88fe-4b40-a374-f6256b84ffae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9ad6b25d347de4c832097c05f27854bacbebaf6f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84961311"
---
# <a name="create-an-entity-mds-add-in-for-excel"></a>Creare un'entità (componente aggiuntivo MDS per Excel)
  Nel [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], gli amministratori possono creare nuove entità per archiviare i dati. Quando si crea un'entità, è necessario caricare almeno un campionamento dei dati che si desidera archiviare.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre dell'autorizzazione di accesso alle aree funzionali **Amministrazione sistema** e **Visualizzatore** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](../administrators-master-data-services.md).  
  
-   È necessario disporre di un modello esistente in cui creare l'entità. Per altre informazioni, vedere [Creare un modello &#40;Master Data Services&#41;](../create-a-model-master-data-services.md).  
  
-   Verificare che i dati soddisfino i requisiti seguenti:  
  
    -   Nei dati deve essere presente una riga di intestazione.  
  
    -   È utile disporre delle colonne **Nome** e **Codice** . **Codice** è un identificatore univoco per ogni riga.  
  
    -   Deve essere presente almeno una riga di dati diversa dall'intestazione. Non è necessario che siano presenti valori in tutte le colonne, ma i dati devono essere rappresentativi di quelli che saranno presenti nell'entità.  
  
    -   Se è presente una colonna contenente un identificatore univoco (noto in MDS come **Codice**), assicurarsi che i valori siano univoci. Se nessuna colonna contiene identificatori, è possibile generarli automaticamente quando si crea l'entità.  
  
    -   Verificare che nessuna cella contenga formule.  
  
    -   Verificare che nessuna cella contenga valori relativi all'ora. In MDS è possibile salvare i valori relativi alla data ma non quelli relativi all'ora.  
  
### <a name="to-create-an-entity-and-load-data"></a>Per creare un'entità e caricare i dati  
  
1.  Aprire o creare un foglio di lavoro di Excel contenente i dati che si desidera caricare.  
  
2.  Selezionare le celle che si desidera caricare nella nuova entità.  
  
3.  Nel gruppo **Compila modello** della scheda **Dati master** fare clic su **Crea entità**.  
  
4.  Se viene richiesto di connettersi a un repository MDS, effettuare la connessione.  
  
5.  Nella finestra di dialogo **Crea entità** lasciare l'intervallo predefinito oppure modificarlo in base ai dati che si vuole caricare.  
  
6.  Non deselezionare la casella di controllo **Dati con intestazioni** .  
  
7.  Selezionare un modello dall'elenco **Modello** .  
  
8.  Selezionare una versione dall'elenco **Versione** .  
  
9. Nella casella **Nome nuova entità** digitare un nome per l'entità.  
  
10. Nell'elenco **Codice** selezionare la colonna contenente identificatori univoci o codici generatati automaticamente.  
  
11. Facoltativa. Nell'elenco **Nome** selezionare una colonna contenente i nomi per ogni membro.  
  
12. Fare clic su **OK**. Dopo che l'entità è stata creata, viene visualizzata una nuova riga di intestazione, le celle vengono evidenziate e il nome del foglio viene aggiornato in base al nome dell'entità.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   Per visualizzare gli errori che si sono verificati, fare clic su **Mostra stato** nel gruppo **Pubblica e convalida**. Verranno visualizzate le colonne ValidationStatus e InputStatus. Per altre informazioni, vedere [Convalida dei dati &#40;componente aggiuntivo MDS per Excel&#41;](validating-data-mds-add-in-for-excel.md).  
  
-   Verificare che gli attributi siano stati creati con il tipo di dati previsto.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un attributo basato su dominio &#40;componente aggiuntivo MDS per Excel&#41;](create-a-domain-based-attribute-mds-add-in-for-excel.md)  
  
  
