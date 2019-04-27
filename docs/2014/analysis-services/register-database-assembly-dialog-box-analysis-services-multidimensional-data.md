---
title: Database dialogo Registra Assembly (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aad57083bdcd8337e9320e81a662bef12888011e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748515"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Registra assembly database (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Registra assembly server** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per impostare le proprietà di un riferimento ad assembly in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per visualizzare la finestra di dialogo **Registra assembly server** , è possibile fare clic con il pulsante destro del mouse sulla cartella Assembly di un database o di un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in **Esplora oggetti** e scegliere **Nuovo assembly**.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Tipo**|Consente di selezionare il tipo di riferimento ad assembly. Sono disponibili i valori seguenti.<br /><br /> **Assembly .NET**: <br />                      Il riferimento a un assembly si riferisce a un assembly di [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **DLL COM**: <br />                      Il riferimento a un assembly si riferisce a una libreria COM.<br /><br /> <br /><br /> **\*\* Nota sulla sicurezza \* \***  gli assembly COM possono rappresentare un rischio per la sicurezza. A causa di tale rischio e di altre considerazioni, gli assembly COM sono stati deprecati in [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)] e potrebbero non essere supportati nelle versioni future.|  
|**Nome file**|Consente di specificare il nome e il percorso completo del file di assembly .NET o della libreria COM.|  
|**...**|Fare clic su questo pulsante per visualizzare la finestra di dialogo **Apri** e selezionare il nome e il percorso completo del file di assembly .NET o della libreria COM.|  
|**Nome dell'assembly**|Consente di digitare il nome del riferimento all'assembly.<br /><br /> Nota: Se si modifica questo valore non modifica il nome dell'assembly a cui fa riferimento all'assembly, ma la modifica del nome utilizzato il di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza o dal database quando si fa riferimento il riferimento all'assembly.|  
|**Includi informazioni di debug**|Selezionare questa opzione per includere informazioni di debug, se disponibili, relative all'assembly .NET o alla libreria COM.|  
|**Timestamp creazione**|Consente di visualizzare la data e l'ora di creazione del riferimento a un assembly.|  
|**Ultimo aggiornamento schema**|Consente di visualizzare la data e l'ora dell'ultimo aggiornamento ai metadati per il riferimento a un assembly.|  
|**Origine**|Consente di visualizzare l'origine del riferimento a un assembly. Questa proprietà in genere contiene il percorso completo e il nome file di assembly a cui si riferisce il riferimento a un assembly.|  
|**Safe**|Selezionare questa opzione per utilizzare l'impostazione di autorizzazione corrispondente per il riferimento all'assembly. Se questa opzione è selezionata, viene consentito l'utilizzo dell'assembly esclusivamente per operazioni di calcolo interne e accesso ai dati locali. Il codice eseguito da un assembly per cui è stata selezionata tale opzione non può accedere a risorse di sistema esterne, quali file, reti, variabili di ambiente o al Registro di sistema.<br /><br /> **\*\* Nota sulla sicurezza \* \***  questa opzione è l'impostazione di autorizzazioni consigliata per gli assembly che eseguono attività di gestione di calcolo e i dati senza accedere alle risorse esterne [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Si tratta dell'impostazione di autorizzazione più restrittiva.|  
|**Accesso esterno**|Selezionare questa opzione per utilizzare l'impostazione di autorizzazione corrispondente per il riferimento all'assembly. Se questa opzione è selezionata, viene consentito l'utilizzo dell'assembly esclusivamente per operazioni di calcolo interne e accesso ai dati locali. Il codice eseguito da un assembly per cui è stata selezionata tale opzione può accedere a risorse di sistema esterne, quali file, reti, variabili di ambiente e al Registro di sistema.<br /><br /> **\*\* Nota sulla sicurezza \* \***  questa opzione è consigliata per gli assembly che accedono a risorse esterne [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Per impostazione predefinita, gli assembly per i quali è stata selezionata tale opzione vengono eseguiti utilizzando le credenziali di sicurezza dell'account del servizio. È possibile che il codice all'interno dell'assembly in modo esplicito rappresentare il chiamante [!INCLUDE[msCoName](../includes/msconame-md.md)] il contesto di sicurezza di autenticazione di Windows. Dal momento che per impostazione predefinita l'esecuzione avviene mediante l'account del servizio, è necessario concedere l'autorizzazione all'esecuzione di assembly per i quali è stata selezionata questa opzione esclusivamente a ruoli autorizzati all'utilizzo dell'account del servizio. Questa opzione è meno restrittiva dell'impostazione di autorizzazione **Sicure**, ma lo è di più rispetto a **Senza restrizioni**.|  
|**Unrestricted**|Selezionare questa opzione per utilizzare l'impostazione di autorizzazione corrispondente per il riferimento all'assembly. Se questa opzione è selezionata, all'assembly è garantito accesso illimitato alle risorse sia interne sia esterne. L'esecuzione del codice contenuto in un assembly per il quale è stata selezionata tale opzione consente di chiamare codice non gestito.<br /><br /> **\*\* Nota sulla sicurezza \* \***  questa opzione non è consigliata a meno che l'assembly richiede l'accesso senza restrizioni. Dal punto di vista della sicurezza, questa opzione è equivalente ad **Accesso esterno**. Gli assembly per i quali è stata selezionata l'opzione **Accesso esterno** offrono tuttavia varie protezioni in termini di affidabilità ed efficacia che non sono disponibili negli assembly che usano questa opzione. Se si seleziona questa opzione, infatti, il codice contenuto nell'assembly può eseguire operazioni non valide sullo spazio di processo e pertanto può compromettere l'affidabilità e la scalabilità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Questa impostazione di autorizzazione è in assoluto la meno restrittiva ed è necessario utilizzarla con cautela.|  
|**Usa nome utente e password specifici**|Selezionare questa opzione per fare in modo che l'oggetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usi le credenziali di sicurezza di un determinato account utente.|  
|**Nome utente**|Digitare il dominio e il nome dell'account utente che verranno usati dall'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selezionato. Per il dominio e il nome dell'account utente viene utilizzato il formato seguente:<br /><br /> *\<Nome di dominio >* **\\**  *\<nome dell'account utente >*<br /><br /> Nota: Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .|  
|**Password**|Digitare il dominio e il nome dell'account utente che verranno usati dall'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selezionato.|  
|**Usa account del servizio**|Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzi le credenziali di sicurezza associate al servizio di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che gestisce l'oggetto.|  
|**Usa credenziali dell'utente corrente**|Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usi le credenziali di sicurezza dell'utente corrente.|  
|**Default**|Selezionare questa opzione per fare in modo che [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]utilizzi l'account utente predefinito. Questa opzione è equivalente all'opzione **Usa credenziali dell'utente corrente** .|  
|**Descrizione**|Consente di digitare una descrizione del riferimento all'assembly.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gestione di assembly di modelli multidimensionali](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
