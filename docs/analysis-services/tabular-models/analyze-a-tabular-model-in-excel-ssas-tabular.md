---
title: Analizzare un modello tabulare di Analysis Services in Excel | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a3cd28375a60dc2cbf7447068fde8c5a1c7dba07
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072228"
---
# <a name="analyze-a-tabular-model-in-excel"></a>Analizzare un modello tabulare in Excel  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  La funzionalità Analizza in Excel di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] consente di aprire Microsoft Excel, di creare una connessione dell'origine dati al database dell'area di lavoro del modello e di aggiungere automaticamente una tabella pivot al foglio di lavoro. Gli oggetti del modello (tabelle, colonne, misure, gerarchie e indicatori KPI) sono inclusi come campi nel relativo elenco della tabella pivot.  
  
> [!NOTE]  
>  Per usare la funzionalità Analizza in Excel, è necessario che Microsoft Office 2003 o versione successiva sia installato nello stesso computer di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. In caso contrario, è possibile utilizzare Excel in un altro computer e connettersi al database dell'area di lavoro modello come origine dati. Successivamente, è possibile aggiungere manualmente una tabella pivot al foglio di lavoro. Gli oggetti del modello (tabelle, colonne, misure e indicatori KPI) sono inclusi come campi nel relativo elenco della tabella pivot.  
  
## <a name="tasks"></a>Attività  
  
#### <a name="to-analyze-a-tabular-model-project-by-using-the-analyze-in-excel-feature"></a>Per analizzare un progetto di modello tabulare tramite la funzionalità Analizza in Excel  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]fare clic sul menu **Modello** e quindi scegliere **Analizza in Excel**.  
  
2.  Nella finestra di dialogo **Scegli credenziale e prospettive** selezionare una delle seguenti opzioni relative alle credenziali per connettersi all'origine dati dell'area di lavoro del modello:  
  
    -   Per usare l'account utente corrente, selezionare **Utente di Windows corrente**.  
  
    -   Per usare un account utente diverso, selezionare **Altro utente di Windows**.  
  
         In genere, questo account utente sarà membro di un ruolo. Non è necessaria alcuna password. L'account può essere utilizzato solo nel contesto di una connessione di Excel al database dell'area di lavoro.  
  
    -   Per usare un ruolo di sicurezza, fare clic su **Ruolo**e quindi, nella casella di riepilogo, selezionare uno o più ruoli.  
  
         I ruoli di sicurezza devono essere definiti utilizzando Gestione ruoli. Per altre informazioni, vedere [crea e Gestisci ruoli](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
3.  Per usare una prospettiva, nella casella di riepilogo **Prospettiva** selezionare una prospettiva.  
  
     Le prospettive (diverse dall'impostazione predefinita) devono essere definite tramite la finestra di dialogo Prospettive. Per altre informazioni, vedere [crea e Gestisci prospettive](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md).  
  
> [!NOTE]  
>  L'elenco di campi della tabella pivot in Excel non viene aggiornato automaticamente mentre si apportano modifiche al progetto di modello in Progettazione modelli. Per aggiornare l'elenco di campi della tabella pivot, fare clic su **Aggiorna** nella barra multifunzione **Opzioni**di Excel.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)  
  
  
