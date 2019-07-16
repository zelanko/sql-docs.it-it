---
title: Concedere l'accesso personalizzato ai dati della dimensione (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb93b4aeeaae9d659a225763286fc15a7d9f52a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208868"
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>Concedere l'accesso personalizzato ai dati della dimensione (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dopo avere abilitato l'accesso in lettura a un cubo, è possibile impostare ulteriori autorizzazioni che consentono o negano in modo esplicito l'accesso ai membri della dimensione, comprese le misure presenti all'interno della Dimensione di tipo misure in cui sono contenute tutte le misure usate in un cubo. Se ad esempio sono presenti più categorie di rivenditori, si potrebbe voler impostare le autorizzazioni per escludere i dati per un tipo di attività specifico. La seguente figura mostra l'effetto che si ottiene prima e dopo avere negato l'accesso al tipo di attività Warehouse nella dimensione Reseller.  
  
 ![Le tabelle pivot con e senza un membro della dimensione](../../analysis-services/multidimensional-models/media/ssas-permsdimdenied.png "tabelle pivot con e senza un membro della dimensione")  
  
 Per impostazione predefinita, se è possibile leggere i dati da un cubo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , si dispone automaticamente delle autorizzazioni di lettura su tutte le misure e i membri della dimensione associati a tale cubo. Sebbene questo comportamento possa essere sufficiente per molti scenari, talvolta i requisiti di sicurezza richiedono una strategia di autorizzazione più segmentata con vari livelli di accesso per diversi utenti nella stessa dimensione.  
  
 È possibile limitare l'accesso scegliendo i membri a cui consentire (AllowedSet) o negare (DeniedSet) l'accesso. A tale scopo, selezionare o deselezionare i membri della dimensione per includere o escludere un membro dal ruolo.  
  
 La sicurezza delle dimensioni di base è la più semplice. È sufficiente selezionare gli attributi della dimensione e le gerarchie di attributi da includere o escludere nel ruolo. La sicurezza avanzata è più complessa e richiede una certa esperienza nella creazione di script MDX. Di seguito vengono descritti entrambi gli approcci.  

> [!NOTE]  
>  Le istruzioni seguenti presuppongono una connessione client che esegue query in MDX. Se il client usa DAX, ad esempio Power View in Power BI, la sicurezza delle dimensioni non è evidente nei risultati della query. Per altre informazioni, vedere [Informazioni su Power View per modelli multidimensionali](understanding-power-view-for-multidimensional-models.md) .
      
## <a name="prerequisites"></a>Prerequisiti  
 Negli scenari di accesso personalizzati non è possibile usare tutte le misure e i membri della dimensione. La connessione non riesce se un ruolo limita l'accesso a una misura o un membro predefinito oppure limita l'accesso a misure che fanno parte di espressioni di misura.  
  
 **Verificare la presenza di limitazioni alla sicurezza delle dimensioni: misure predefinite, membri predefiniti e misure usate in espressioni di misura**  
  
1.  In SQL Server Management Studio fare doppio clic su un cubo e selezionare **Crea Script per cubo** | **ALTER in** | **Nuova finestra editor di query**.  
  
2.  Cercare **DefaultMeasure**. Ne verrà trovato uno per il cubo e uno per ogni prospettiva. Quando si definisce la sicurezza delle dimensioni evitare di limitare l'accesso alle misure predefinite.  
  
3.  Cercare quindi **MeasureExpression**. Un'espressione di misura è una misura, basata su un calcolo, in cui il calcolo include spesso altre misure. Verificare che la misura da limitare non sia usata in un'espressione. In alternativa, procedere con la limitazione dell'accesso, assicurandosi solo di escludere anche tutti i riferimenti a tale misura in tutto il cubo.  
  
4.  Cercare infine **DefaultMember**. Prendere nota di tutti gli attributi che fungono da membro predefinito di un attributo. Evitare di definire limitazioni in tali attributi quando si configura la sicurezza delle dimensioni.  
  
## <a name="basic-dimension-security"></a>Sicurezza delle dimensioni di base  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti e quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
     Il ruolo dovrebbe già disporre dell'accesso di lettura al cubo. Per altre informazioni, vedere [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) .  
  
2.  In **Dati della dimensione** | **Di base**selezionare la dimensione per la quale si stanno impostando le autorizzazioni.  
  
3.  Scegliere la gerarchia dell'attributo. Non tutti gli attributi saranno disponibili. Nell'elenco **Gerarchia dell'attributo** sono visualizzati solo gli attributi con **AttributeHierarchyEnabled** .  
  
4.  Scegliere i membri a cui consentire o negare l'accesso. L'impostazione predefinita è consentire l'accesso tramite l'opzione **Seleziona tutti i membri** . È consigliabile usare questa impostazione predefinita e quindi deselezionare i singoli membri che non devono essere visibili agli account utente e di gruppo di Windows nel riquadro **Appartenenze** tramite questo ruolo. In questo modo i nuovi membri aggiunti nelle operazioni di elaborazione successive saranno automaticamente disponibili per gli utenti che si connettono tramite questo ruolo.  
  
     In alternativa, è possibile usare l'opzione **Deseleziona tutti i membri** per revocare l'accesso a tutti i membri e quindi selezionare i membri a cui consentire l'accesso. Nelle successive operazioni di elaborazione, i nuovi membri non saranno visibili finché non si modifica manualmente la sicurezza dei dati della dimensione per consentirne l'accesso.  
  
5.  Facoltativamente, fare clic su **Avanzate** e selezionare **Consenti totali visualizzati** per questa gerarchia attributi. Questa opzione ricalcola le aggregazioni in base ai membri disponibili tramite il ruolo.  
  
    > [!NOTE]  
    >  Quando si applicano le autorizzazioni che escludono i membri della dimensione, i totali aggregati non vengono ricalcolati automaticamente. Si supponga che il membro **Totale** di una gerarchia attributi restituisca 200 prima dell'applicazione delle autorizzazioni. Dopo avere applicato le autorizzazioni che negano l'accesso ad alcuni membri, **Totale** restituisce ancora 200, sebbene i valori del membro visibili all'utente siano molti di meno. Per non confondere gli utenti del cubo, è possibile configurare il membro **Totale** in modo che rappresenti l'aggregazione solo dei membri ai quali i membri del ruolo hanno accesso anziché l'aggregazione di tutti i membri della gerarchia attributi. Per richiamare questo comportamento, è possibile abilitare **Visual Totals** nella scheda **Avanzate** durante la configurazione della sicurezza delle dimensioni. Una volta abilitato, l'aggregato viene calcolato in fase di query anziché recuperato dalle aggregazioni precalcolate. Questa operazione può influire in modo significativo sulle prestazioni. Usarla pertanto solo quando è necessario.  
  
## <a name="hiding-measures"></a>Nascondere le misure  
 In [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)è stato descritto che per nascondere completamente tutti gli aspetti visivi di una misura, e non solo i dati della cella, sono necessarie le autorizzazioni per i membri della dimensione. Questa sezione descrive come negare l'accesso ai metadati degli oggetti di una misura.  
  
1.  In **Dati della dimensione** | **Di base**scorrere l'elenco Dimensione fino a visualizzare le dimensioni del cubo, quindi selezionare **Dimensione di tipo misure**.  
  
2.  Nell'elenco delle misure deselezionare la casella di controllo per le misure che non devono essere visualizzate dagli utenti che si connettono tramite questo ruolo.  
  
> [!NOTE]  
>  Verificare i prerequisiti per informazioni su come identificare le misure che possono violare la sicurezza dei ruoli.  
  
## <a name="advanced-dimension-security"></a>Sicurezza delle dimensioni avanzata  
 Se si è esperti di MDX, un altro approccio consiste nello scrivere espressioni MDX che impostano i criteri in base ai quali viene consentito o negato l'accesso ai membri. Fare clic su **Crea ruolo** | **Dati della dimensione** | **Avanzate** per fornire lo script.  
  
 Per scrivere l'istruzione MDX, è possibile usare Generatore MDX. Per informazioni dettagliate, vedere [Generatore MDX &#40;Analysis Services - Dati multidimensionali&#41;](http://msdn.microsoft.com/library/fecbf093-65ea-4e1b-b637-f04876f1cb0f). Nella scheda **Avanzate** sono disponibili le opzioni seguenti:  
  
 **Attribute**  
 Consente di selezionare l'attributo per cui gestire la sicurezza dei membri.  
  
 **Set di membri autorizzati**  
 La proprietà AllowedSet può restituire nessun membro (impostazione predefinita), tutti i membri o alcuni membri. Se si consente l'accesso a un attributo e non si definisce alcun membro del set delle autorizzazioni concesse, verrà consentito l'accesso a tutti i membri. Se si consente l'accesso a un attributo e si definisce un set di membri dell'attributo, saranno visibili solo i membri consentiti in modo esplicito.  
  
 La creazione di AllowedSet genera una reazione a catena quando l'attributo fa parte di una gerarchia a più livelli. Si supponga, ad esempio, che un ruolo consenta l'accesso allo stato di Washington. Si consideri uno scenario in cui il ruolo conceda le autorizzazioni alla divisione vendite dello stato di Washington di una società. Per gli utenti che si connettono tramite questo ruolo, le query che includono predecessori (Stati Uniti) o discendenti (Seattle e Redmond) visualizzeranno solo i membri in una catena che includono lo stato di Washington. Poiché gli altri stati non vengono consentiti in modo esplicito, l'effetto sarà identico a quello del caso in cui gli stati vengano negati.  
  
> [!NOTE]  
>  Se si definisce un set vuoto ({}) dei membri dell'attributo, nessun membro dell'attributo sarà visibile al ruolo del database. L'assenza di un set delle autorizzazioni concesse non viene interpretata come set vuoto.  
  
 **Set di membri non autorizzati**  
 La proprietà DeniedSet può restituire nessun membro, tutti i membri (impostazione predefinita) o alcuni membri dell'attributo. Se il set delle autorizzazioni negate contiene solo un set specifico di membri dell'attributo, al ruolo del database viene negato l'accesso solo a tali membri specifici, oltre ai discendenti se l'attributo fa parte di una gerarchia a più livelli. Si consideri l'esempio della divisione vendite dello stato di Washington. Se Washington viene inserito in DeniedSet, gli utenti che si connettono tramite questo ruolo visualizzeranno tutti gli altri stati eccetto Washington e gli attributi dei relativi discendenti.  
  
 Tenere presente, secondo quanto indicato nella sezione precedente, che il set delle autorizzazioni negate è una raccolta fissa. Se l'elaborazione successivamente introduce nuovi membri a cui deve essere negato l'accesso, sarà necessario modificare questo ruolo per aggiungere tali membri all'elenco.  
  
 **Membro predefinito**  
 La proprietà DefaultMember definisce il set di dati restituito a un client quando un attributo non è incluso in modo esplicito in una query. Quando l'attributo non è incluso in modo esplicito, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene usato uno dei membri predefiniti seguenti per l'attributo:  
  
-   Se il ruolo del database definisce un membro predefinito per l'attributo, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà usato tale membro predefinito.  
  
-   Se il ruolo del database non definisce un membro predefinito per l'attributo, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà usato il membro predefinito definito per l'attributo stesso. Il membro predefinito per un attributo, a meno che l'utente non ne specifichi uno diverso e a condizione che l'attributo non sia definito come non aggregabile, è il membro **All** .  
  
 Si supponga, ad esempio, che un ruolo del database specifichi **Male** come membro predefinito per l'attributo **Gender** . A meno che una query non includa in modo esplicito l'attributo **Gender** e non specifichi un membro diverso per l'attributo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituirà un set di dati contenente solo i clienti di sesso maschile. Per altre informazioni sull'impostazione del membro predefinito, vedere [Definire un membro predefinito](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 **Consenti totale visualizzato**  
 La proprietà VisualTotals indica se i valori di cella aggregati visualizzati vengono calcolati in base a tutti i valori di cella o solo in base ai valori di cella visibili al ruolo del database.  
  
 Per impostazione predefinita, la proprietà VisualTotals è disabilitata, ovvero è impostata su **False**. L'impostazione predefinita garantisce prestazioni ottimali, in quanto consente di calcolare in modo rapido il totale di tutti i valori di cella tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , anziché dedicare il tempo necessario per selezionare i valori di cella da calcolare.  
  
 La disabilitazione della proprietà VisualTotals, tuttavia, può creare un problema di sicurezza se un utente può usare i valori di cella aggregati per dedurre i valori relativi ai membri dell'attributo a cui il proprio ruolo del database non può accedere. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ad esempio, vengono usati i valori per tre membri dell'attributo per calcolare un valore di cella aggregato. Il ruolo del database può visualizzare due di tali membri dell'attributo. Utilizzando il valore di cella aggregato, un membro di questo ruolo del database sarebbe in grado di dedurre il valore per il terzo membro dell'attributo.  
  
 L'impostazione della proprietà VisualTotals su **True** può eliminare questo rischio. Quando si abilita la proprietà VisualTotals, un ruolo del database può visualizzare solo i totali aggregati per i membri della dimensione per cui dispone delle autorizzazioni.  
  
 **Controlla**  
 Fare clic su questa opzione per testare la sintassi MDX definita in questa pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)   
 [Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Concedere le autorizzazioni per un oggetto origine dati &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
