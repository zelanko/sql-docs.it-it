---
title: Concedere l'accesso personalizzato ai dati della dimensione (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.dimensiondata.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- AllowedSet property
- IsAllowed property
- DeniedSet property
- user access rights [Analysis Services], dimensions
- custom dimension data access [Analysis Services]
- permissions [Analysis Services], dimensions
- DefaultMember property
- VisualTotals property
- ApplyDenied property
ms.assetid: b028720d-3785-4381-9572-157d13ec4291
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 51e180d39df78a90869c2d6cdfc366e0cc13ba02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726607"
---
# <a name="grant-custom-access-to-dimension-data-analysis-services"></a>Concedere l'accesso personalizzato ai dati della dimensione (Analysis Services)
  Dopo avere abilitato l'accesso in lettura a un cubo, è possibile impostare ulteriori autorizzazioni che consentono o negano in modo esplicito l'accesso ai membri della dimensione, comprese le misure presenti all'interno della Dimensione di tipo misure in cui sono contenute tutte le misure usate in un cubo. Se ad esempio sono presenti più categorie di rivenditori, si potrebbe voler impostare le autorizzazioni per escludere i dati per un tipo di attività specifico. La seguente figura mostra l'effetto che si ottiene prima e dopo avere negato l'accesso al tipo di attività Warehouse nella dimensione Reseller.  
  
 ![Le tabelle pivot con e senza un membro della dimensione](../media/ssas-permsdimdenied.png "tabelle pivot con e senza un membro della dimensione")  
  
 Per impostazione predefinita, se è possibile leggere i dati da un cubo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , si dispone automaticamente delle autorizzazioni di lettura su tutte le misure e i membri della dimensione associati a tale cubo. Sebbene questo comportamento possa essere sufficiente per molti scenari, talvolta i requisiti di sicurezza richiedono una strategia di autorizzazione più segmentata con vari livelli di accesso per diversi utenti nella stessa dimensione.  
  
 È possibile limitare l'accesso scegliendo i membri a cui consentire (AllowedSet) o negare (DeniedSet) l'accesso. A tale scopo, selezionare o deselezionare i membri della dimensione per includere o escludere un membro dal ruolo.  
  
 La sicurezza delle dimensioni di base è la più semplice. È sufficiente selezionare gli attributi della dimensione e le gerarchie di attributi da includere o escludere nel ruolo. La sicurezza avanzata è più complessa e richiede una certa esperienza nella creazione di script MDX. Di seguito vengono descritti entrambi gli approcci.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Negli scenari di accesso personalizzati non è possibile usare tutte le misure e i membri della dimensione. La connessione non riesce se un ruolo limita l'accesso a una misura o un membro predefinito oppure limita l'accesso a misure che fanno parte di espressioni di misura.  
  
 **Verificare la presenza di limitazioni alla sicurezza delle dimensioni: misure predefinite, membri predefiniti e misure usate in espressioni di misura**  
  
1.  In SQL Server Management Studio fare doppio clic su un cubo e selezionare **Crea Script per cubo** | **ALTER in** | **Nuova finestra editor di query**.  
  
2.  Cercare `DefaultMeasure`. Ne verrà trovato uno per il cubo e uno per ogni prospettiva. Quando si definisce la sicurezza delle dimensioni evitare di limitare l'accesso alle misure predefinite.  
  
3.  Cercare quindi `MeasureExpression`. Un'espressione di misura è una misura, basata su un calcolo, in cui il calcolo include spesso altre misure. Verificare che la misura da limitare non sia usata in un'espressione. In alternativa, procedere con la limitazione dell'accesso, assicurandosi solo di escludere anche tutti i riferimenti a tale misura in tutto il cubo.  
  
4.  Cercare infine `DefaultMember`. Prendere nota di tutti gli attributi che fungono da membro predefinito di un attributo. Evitare di definire limitazioni in tali attributi quando si configura la sicurezza delle dimensioni.  
  
## <a name="basic-dimension-security"></a>Sicurezza delle dimensioni di base  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti e quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
     Il ruolo dovrebbe già disporre dell'accesso di lettura al cubo. Per altre informazioni, vedere [Grant cube or model permissions &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md) .  
  
2.  In **Dati della dimensione** | **Di base**selezionare la dimensione per la quale si stanno impostando le autorizzazioni.  
  
3.  Scegliere la gerarchia dell'attributo. Non tutti gli attributi saranno disponibili. Nell'elenco **Gerarchia dell'attributo** sono visualizzati solo gli attributi con **AttributeHierarchyEnabled** .  
  
4.  Scegliere i membri a cui consentire o negare l'accesso. L'impostazione predefinita è consentire l'accesso tramite l'opzione **Seleziona tutti i membri** . È consigliabile usare questa impostazione predefinita e quindi deselezionare i singoli membri che non devono essere visibili agli account utente e di gruppo di Windows nel riquadro **Appartenenze** tramite questo ruolo. In questo modo i nuovi membri aggiunti nelle operazioni di elaborazione successive saranno automaticamente disponibili per gli utenti che si connettono tramite questo ruolo.  
  
     In alternativa, è possibile usare l'opzione **Deseleziona tutti i membri** per revocare l'accesso a tutti i membri e quindi selezionare i membri a cui consentire l'accesso. Nelle successive operazioni di elaborazione, i nuovi membri non saranno visibili finché non si modifica manualmente la sicurezza dei dati della dimensione per consentirne l'accesso.  
  
5.  Facoltativamente, fare clic su **avanzate** abilitare `Visual Totals` per questa gerarchia dell'attributo. Questa opzione ricalcola le aggregazioni in base ai membri disponibili tramite il ruolo.  
  
    > [!NOTE]  
    >  Quando si applicano le autorizzazioni che escludono i membri della dimensione, i totali aggregati non vengono ricalcolati automaticamente. Si supponga che il `All` membro di una gerarchia dell'attributo restituisce un conteggio pari a 200 prima che vengano applicate le autorizzazioni. Dopo aver applicato le autorizzazioni che negano l'accesso ad alcuni membri, `All` restituisce ancora 200, sebbene i valori del membro visibili all'utente siano molti di meno. Per evitare di confondere gli utenti del cubo, è possibile configurare il `All` membro essere che rappresenti l'aggregazione solo dei membri ai quali i membri del ruolo, anziché l'aggregazione di tutti i membri della gerarchia dell'attributo. Per richiamare questo comportamento, è possibile abilitare `Visual Totals` nella **avanzate** scheda quando si configura la sicurezza delle dimensioni. Una volta abilitato, l'aggregato viene calcolato in fase di query anziché recuperato dalle aggregazioni precalcolate. Questa operazione può influire in modo significativo sulle prestazioni. Usarla pertanto solo quando è necessario.  
  
## <a name="hiding-measures"></a>Nascondere le misure  
 In [Grant custom access to cell data &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)è stato descritto che per nascondere completamente tutti gli aspetti visivi di una misura, e non solo i dati della cella, sono necessarie le autorizzazioni per i membri della dimensione. Questa sezione descrive come negare l'accesso ai metadati degli oggetti di una misura.  
  
1.  In **Dati della dimensione** | **Di base**scorrere l'elenco Dimensione fino a visualizzare le dimensioni del cubo, quindi selezionare **Dimensione di tipo misure**.  
  
2.  Nell'elenco delle misure deselezionare la casella di controllo per le misure che non devono essere visualizzate dagli utenti che si connettono tramite questo ruolo.  
  
> [!NOTE]  
>  Verificare i prerequisiti per informazioni su come identificare le misure che possono violare la sicurezza dei ruoli.  
  
## <a name="advanced-dimension-security"></a>Sicurezza delle dimensioni avanzata  
 Se si è esperti di MDX, un altro approccio consiste nello scrivere espressioni MDX che impostano i criteri in base ai quali viene consentito o negato l'accesso ai membri. Fare clic su **Crea ruolo** | **Dati della dimensione** | **Avanzate** per fornire lo script.  
  
 Per scrivere l'istruzione MDX, è possibile usare Generatore MDX. Per informazioni dettagliate, vedere [Generatore MDX &#40;Analysis Services - Dati multidimensionali&#41;](../mdx-builder-analysis-services-multidimensional-data.md). Nella scheda **Avanzate** sono disponibili le opzioni seguenti:  
  
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
  
-   Se il ruolo del database non definisce un membro predefinito per l'attributo, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà usato il membro predefinito definito per l'attributo stesso. Il membro predefinito per un attributo, a meno che l'utente non ne specifichi uno diverso e a condizione che l'attributo non sia definito come non aggregabile, è il membro `All`.  
  
 Si supponga, ad esempio, che un ruolo del database specifichi `Male` come membro predefinito per l'attributo `Gender`. A meno che una query non includa in modo esplicito l'attributo `Gender` e non specifichi un membro diverso per l'attributo, in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verrà restituito un set di dati contenente solo i clienti di sesso maschile. Per altre informazioni sull'impostazione del membro predefinito, vedere [Definire un membro predefinito](attribute-properties-define-a-default-member.md).  
  
 **Consenti totale visualizzato**  
 La proprietà VisualTotals indica se i valori di cella aggregati visualizzati vengono calcolati in base a tutti i valori di cella o solo in base ai valori di cella visibili al ruolo del database.  
  
 Per impostazione predefinita, la proprietà VisualTotals è disabilitata (impostato su `False`). L'impostazione predefinita garantisce prestazioni ottimali, in quanto consente di calcolare in modo rapido il totale di tutti i valori di cella tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , anziché dedicare il tempo necessario per selezionare i valori di cella da calcolare.  
  
 La disabilitazione della proprietà VisualTotals, tuttavia, può creare un problema di sicurezza se un utente può usare i valori di cella aggregati per dedurre i valori relativi ai membri dell'attributo a cui il proprio ruolo del database non può accedere. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , ad esempio, vengono usati i valori per tre membri dell'attributo per calcolare un valore di cella aggregato. Il ruolo del database può visualizzare due di tali membri dell'attributo. Utilizzando il valore di cella aggregato, un membro di questo ruolo del database sarebbe in grado di dedurre il valore per il terzo membro dell'attributo.  
  
 Impostazione della proprietà VisualTotals `True` possono eliminare tale rischio. Quando si abilita la proprietà VisualTotals, un ruolo del database può visualizzare solo i totali aggregati per i membri della dimensione per cui dispone delle autorizzazioni.  
  
 **Controlla**  
 Fare clic su questa opzione per testare la sintassi MDX definita in questa pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)   
 [Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Concedere le autorizzazioni per un oggetto origine dati &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
