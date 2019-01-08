---
title: Concedere l'accesso personalizzato ai dati delle celle (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.celldata.f1
helpviewer_keywords:
- user access rights [Analysis Services], cell data
- permissions [Analysis Services], cells
- read contingent permissions
- read permissions
- cells [Analysis Services]
- custom cell data access [Analysis Services]
ms.assetid: 3b13a4ae-f3df-4523-bd30-b3fdf71e95cf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc9d003fc4c1f3b3cd32e8f23fe635d56e48555e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510899"
---
# <a name="grant-custom-access-to-cell-data-analysis-services"></a>Concedere l'accesso personalizzato ai dati delle celle (Analysis Services)
  La sicurezza della cella viene usata per consentire o negare l'accesso ai dati di misura all'interno di un cubo. La figura seguente mostra una combinazione di misure consentite e negate in una tabella pivot quando il ruolo dell'utente connesso consente l'accesso a determinate misure. In questo esempio, **Reseller Sales Amount** e **Reseller Total Product Cost** sono le uniche misure disponibili tramite questo ruolo. Tutte le altre misure vengono negate in modo implicito. I passaggi usati per ottenere tale risultato vengono forniti nella sezione "Consentire l'accesso a misure specifiche" riportata di seguito.  
  
 ![Tabella pivot con celle consentite e negate](../media/ssas-permscellsallowed.png "tabella pivot con celle consentite e negate")  
  
 Le autorizzazioni per le celle vengono applicate ai dati all'interno della cella e non ai relativi metadati. Si noti come nei risultati di una query la cella venga comunque visualizzata mostrando il valore `#N/A` anziché il valore effettivo. Il `#N/A` valore viene visualizzato nella cella a meno che l'applicazione client converte il valore o un altro valore se viene specificato impostando la proprietà Secured Cell Value nella stringa di connessione.  
  
 Per nascondere completamente la cella, è necessario limitare i membri-dimensioni, attributi della dimensione e membri dell'attributo dimensione-che possono essere visualizzati. Per altre informazioni, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md).  
  
 L'amministratore può specificare se i membri del ruolo dispongono delle autorizzazioni di lettura, lettura condizionale o lettura/scrittura nelle celle di un cubo. Poiché l'assegnazione delle autorizzazioni in una cella rappresenta il livello di sicurezza più basso consentito, prima di iniziare ad applicare le autorizzazioni a questo livello è importante tenere presenti alcuni concetti:  
  
-   La sicurezza a livello di cella non può espandere i diritti limitati a un livello superiore. Ad esempio, se un ruolo nega l'accesso ai dati di dimensione, la sicurezza a livello di cella non può sostituire il set delle autorizzazioni negate. Un altro esempio: si consideri un ruolo con `Read` l'autorizzazione per un cubo e **lettura/scrittura** autorizzazione in una cella, l'autorizzazione di dati della cella non sarà **lettura/scrittura**; sarà `Read`.  
  
-   Le autorizzazioni personalizzate spesso devono essere coordinate tra i membri della dimensione e le celle all'interno dello stesso ruolo. Si supponga ad esempio di volere negare l'accesso ad alcune misure correlate allo sconto per diverse combinazioni di rivenditori. Se si specifica **Resellers** come dati di dimensione e **Discount Amount come misura** , sarà necessario combinare all'interno dello stesso ruolo le autorizzazioni sia nella misura (usando le istruzioni illustrate in questo argomento) che nei membri della dimensione. Per informazioni dettagliate sull'impostazione delle autorizzazioni per la dimensione, vedere [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) .  
  
 La sicurezza a livello di cella viene specificata tramite le espressioni MDX. Poiché la cella è una tupla, ovvero un punto di intersezione potenzialmente all'interno di più dimensioni e misure, non è necessario usare MDX per identificare celle specifiche.  
  
## <a name="allow-access-to-specific-measures"></a>Consentire l'accesso a misure specifiche  
 È possibile usare la sicurezza della cella per scegliere in modo esplicito le misure disponibili. Dopo avere identificato in modo specifico i membri consentiti, tutte le altre misure diventano non disponibili. Si tratta probabilmente dello scenario più semplice da implementare tramite lo script MDX come illustrato nella procedura seguente.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], selezionare un database, aprire la cartella **Ruolo** e quindi fare clic su un ruolo del database oppure creare un nuovo ruolo del database. L'appartenenza dovrebbe essere già specificata e il ruolo dovrebbe disporre dell'accesso `Read` al cubo. Per altre informazioni, vedere [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) .  
  
2.  In **Dati delle celle**verificare di avere scelto il cubo corretto e quindi selezionare **Abilita autorizzazioni di lettura**.  
  
     Se si seleziona solo questa casella di controllo senza fornire un'espressione MDX, l'effetto è uguale a quello ottenuto negando l'accesso a tutte le celle del cubo, poiché il set consentito predefinito è vuoto quando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] risolve un subset di celle di un cubo.  
  
3.  Immettere l'espressione MDX seguente.  
  
    ```  
    (Measures.CurrentMember IS [Measures].[Reseller Sales Amount]) OR (Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
    ```  
  
     Questa espressione identifica in modo esplicito le misure visibili agli utenti. Tutte le altre misure non saranno disponibili agli utenti che si connettono tramite questo ruolo. Si noti che [CurrentMember &#40;MDX&#41;](/sql/mdx/current-mdx) imposta il contesto e viene seguito dalla misura consentita. L'effetto di questa espressione sarà quello di visualizzare il valore, se il membro corrente include **Reseller Sales Amount** o **Reseller Total Product Cost**. In caso contrario, verrà negato l'accesso. L'espressione è costituita da più parti, ognuna delle quali è racchiusa tra parentesi. Per specificare più misure viene usato l'operatore `OR`.  
  
## <a name="deny-access-to-specific-measures"></a>Negare l'accesso a misure specifiche  
 La seguente espressione MDX, anch'essa specificata in **Crea ruolo** | **Dati delle celle** | **Consenti lettura del contenuto del cubo**, avrà l'effetto opposto rendendo alcune misure non disponibili. In questo esempio **Discount Amount** e **Discount Percentage** vengono resi non disponibili usando il `NOT` e `AND` operatori. Tutte le altre misure saranno visibili agli utenti che si connettono tramite questo ruolo.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Discount Amount]) AND (NOT Measures.CurrentMember IS [Measures].[Discount Percentage])  
```  
  
 In Excel, la sicurezza della cella risulta chiara nella figura seguente:  
  
 ![Colonne di Excel con celle non disponibili](../media/ssas-permscellshidemeasure.png "colonne di Excel con celle non disponibili")  
  
## <a name="set-read-permissions-on-calculated-measures"></a>Impostare le autorizzazioni di lettura nelle misure calcolate  
 Le autorizzazioni in una misura calcolata possono essere impostate indipendentemente dalle parti che la costituiscono. Passare direttamente alla sezione successiva relativa alle autorizzazioni di lettura condizionale se si vogliono coordinare le autorizzazioni tra una misura calcolata e le relative misure dipendenti.  
  
 Per comprendere il funzionamento delle autorizzazioni di lettura per una misura calcolata, usare **Reseller Gross Profit** in AdventureWorks. Deriva dalle misure **Reseller Sales Amount** e **Reseller Total Product Cost** . Se un ruolo dispone dell'autorizzazione di lettura nelle celle di **Reseller Gross Profit** , questa misura può essere visualizzata anche se le autorizzazioni sono espressamente negate nelle altre misure. Come dimostrazione, copiare la seguente espressione MDX in **Crea ruolo** | **Dati delle celle** | **Consenti lettura del contenuto del cubo**.  
  
```  
(NOT Measures.CurrentMember IS [Measures].[Reseller Sales Amount])  
AND (NOT Measures.CurrentMember IS [Measures].[Reseller Total Product Cost])  
```  
  
 In Excel, connettersi al cubo usando il ruolo corrente e scegliere tutte e tre le misure per osservare gli effetti della sicurezza della cella. Si noti che le misure nel set negato non sono disponibili, mentre è visibile la misura calcolata.  
  
 ![Tabella di Excel con disponibili e non cellls](../media/ssas-permscalculatedcells.png "tabella di Excel con cellls disponibili e non disponibile")  
  
## <a name="set-read-contingent-permissions-on-calculated-measures"></a>Impostare le autorizzazioni di lettura condizionale nelle misure calcolate  
 La sicurezza della cella offre un'alternativa, ovvero l'impostazione delle autorizzazioni di lettura condizionale nelle celle correlate che fanno parte di un calcolo. Usare anche in questo caso l'esempio **Reseller Gross Profit** . Quando si immette la stessa espressione MDX fornita nella sezione precedente, questa volta inserita nella seconda area di testo della finestra di dialogo **Crea ruolo** | **Dati delle celle** (nell'area di testo che si trova al di sotto di **Consenti lettura contenuto cella in base a sicurezza cella**), il risultato è evidente quando viene visualizzato in Excel. Poiché **Reseller Gross Profit** dipende da **Reseller Sales Amount** e **Reseller Total Product Cost**, il profitto lordo sarà ora inaccessibile perché le parti che lo costituiscono sono inaccessibili.  
  
> [!NOTE]  
>  Cosa accade se si impostano le autorizzazioni di lettura e di lettura condizionale in una cella all'interno dello stesso ruolo? Il ruolo fornirà nella cella le autorizzazioni di lettura ma non quelle di lettura condizionale.  
  
 Tenere presente, secondo quanto indicato nella sezione precedente, che se si seleziona solo la casella di controllo **Abilita autorizzazioni di lettura condizionale** senza fornire un'espressione MDX, viene negato l'accesso a tutte le celle del cubo, poiché il set consentito predefinito è vuoto quando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] risolve un subset di celle di un cubo.  
  
## <a name="set-readwrite-permissions-on-a-cell"></a>Impostare le autorizzazioni di lettura/scrittura in una cella  
 Le autorizzazioni di lettura/scrittura in una cella vengono usate per consentire il writeback, a condizione che i membri dispongano delle autorizzazioni di lettura/scrittura per il cubo stesso. Le autorizzazioni concesse a livello di cella non possono essere superiori rispetto a quelle concesse a livello di cubo. Per altri dettagli, vedere [Impostare tabelle writeback delle partizioni](set-partition-writeback.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [Generatore MDX &#40;Analysis Services - Dati multidimensionali&#41;](../mdx-builder-analysis-services-multidimensional-data.md)   
 [Script MDX di base &#40;MDX&#41;](mdx/the-basic-mdx-script-mdx.md)   
 [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)   
 [Concedere le autorizzazioni per una dimensione &#40;Analysis Services&#41;](grant-permissions-on-a-dimension-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)  
  
  
