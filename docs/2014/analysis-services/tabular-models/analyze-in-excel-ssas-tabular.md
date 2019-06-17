---
title: Analizza in Excel (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8090c75108f7a384019030082699917fca915b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067693"
---
# <a name="analyze-in-excel-ssas-tabular"></a>Analizzare in Excel (SSAS tabulare)
  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]la caratteristica Analizza in Excel consente agli autori di modelli tabulari di analizzare rapidamente i progetti di modelli durante lo sviluppo. La caratteristica Analizza in Excel consente di aprire Microsoft Excel, di creare una connessione dell'origine dati al database dell'area di lavoro modello e di aggiungere automaticamente una tabella pivot al foglio di lavoro. Gli oggetti del database dell'area di lavoro (tabelle, colonne e misure) sono inclusi come campi nel relativo elenco della tabella pivot. Gli oggetti e i dati possono essere quindi visualizzati all'interno del contesto dell'utente effettivo o del ruolo e della prospettiva.  
  
 Per questo argomento si presuppone che l'utente abbia già familiarità con Microsoft Excel, nonché con le tabelle e i grafici pivot. Per ulteriori informazioni sull'utilizzo di Excel, vedere la relativa Guida.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Attività correlate](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 La caratteristica Analizza in Excel consente agli autori di modelli di verificare l'efficacia di un progetto di modello utilizzando l'applicazione per l'analisi dei dati comuni, ovvero Microsoft Excel. Per usare la caratteristica Analizza in Excel, è necessario che Microsoft Office 2003 o versione successiva sia installato nello stesso computer di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Se Office non è installato nello stesso computer di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], è possibile usare Excel in un altro computer e connettersi al database dell'area di lavoro come origine dati. Successivamente, è possibile aggiungere manualmente una tabella pivot al foglio di lavoro.  
  
 La caratteristica Analizza in Excel consente di aprire Excel e di creare una nuova cartella di lavoro (con estensione xls). In seguito, viene creata una connessione dati dalla cartella di lavoro al database dell'area di lavoro modello, viene aggiunta una tabella pivot vuota al foglio di lavoro e i metadati dell'oggetto modello vengono popolati nell'elenco di campi della tabella pivot. Successivamente, è possibile aggiungere i dati e i relativi filtri visualizzabili alla tabella pivot.  
  
 Se si utilizza la caratteristica Analizza in Excel, per impostazione predefinita, l'account utente che ha attualmente effettuato l'accesso è l'utente effettivo. Questo account è in genere un amministratore senza restrizioni di visualizzazione relativamente agli oggetti o ai dati del modello. Tuttavia, è possibile specificare un nome utente o un ruolo effettivo diverso. In questo modo, l'utente può sfogliare un progetto di modello in Excel all'interno del contesto di un utente o ruolo specifico. La specificazione dell'utente effettivo prevede le opzioni seguenti:  
  
 **Utente di Windows corrente**  
 Viene utilizzato l'account utente con cui è stato effettuato l'accesso.  
  
 **Altro utente di Windows**  
 Viene utilizzato un nome utente di Windows specificato piuttosto che l'utente che ha effettuato l'accesso. L'utilizzo di un utente di Windows diverso non richiede una password. Gli oggetti e i dati possono essere visualizzati solo in Excel all'interno del contesto del nome utente effettivo. Non è possibile apportare alcuna modifica agli oggetti o ai dati del modello in Excel.  
  
 **Ruolo**  
 Un ruolo viene utilizzato per definire le autorizzazioni utente sui metadati e dati dell'oggetto. I ruoli vengono generalmente definiti per un utente di Windows o un gruppo di utenti di Windows particolare. In alcuni ruoli possono essere inclusi ulteriori filtri a livello di riga definiti in una formula DAX. Se si utilizza la caratteristica Analizza in Excel, è possibile selezionare facoltativamente un ruolo da utilizzare. Le viste dei metadati e dei dati dell'oggetto saranno limitate dall'autorizzazione e dai filtri definiti per il ruolo. Per altre informazioni, vedere [Creare e gestire ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md).  
  
 Oltre all'utente o al ruolo effettivo, è possibile specificare una prospettiva. Le prospettive consentono agli autori di modelli di definire viste di oggetti e dati del modello in scenari aziendali particolari. Per impostazione predefinita, non viene utilizzata alcuna prospettiva. Per utilizzare una prospettiva con Analizza in Excel, le prospettive devono essere già state definite tramite la finestra di dialogo Prospettive in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Se viene specificata una prospettiva, nell'elenco di campi della tabella pivot saranno contenuti solo gli oggetti selezionati nella prospettiva. Per altre informazioni, vedere [Creare e gestire prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md).  
  
##  <a name="bkmk_rt"></a> Attività correlate  
  
|**Argomento**|**Descrizione**|  
|---------------|---------------------|  
|[Analizzare un modello tabulare in Excel &#40;SSAS tabulare&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)|In questo argomento viene descritto come utilizzare la caratteristica Analizza in Excel in Progettazione modelli per aprire Excel, creare una connessione dell'origine dati al database dell'area di lavoro modello e aggiungere una tabella pivot al foglio di lavoro.|  
  
## <a name="see-also"></a>Vedere anche  
 [Analizzare un modello tabulare in Excel &#40;SSAS tabulare&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md)   
 [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md)  
  
  
