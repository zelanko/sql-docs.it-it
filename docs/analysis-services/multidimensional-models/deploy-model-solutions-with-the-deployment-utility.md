---
title: Distribuire soluzioni di modelli con l'utilità di distribuzione | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76d1a3e3cfff777f610bb00f52644af3903ac615
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178507"
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>Distribuire soluzioni di modelli con l'utilità di distribuzione
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  L'utilità **Microsoft.AnalysisServices.Deployment** consente di avviare il motore di distribuzione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dal prompt dei comandi. Come file di input vengono usati i file di output XML generati dalla compilazione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. I file di input sono facilmente modificabili in modo da personalizzare la distribuzione di un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Lo script di distribuzione generato può quindi essere eseguito subito oppure salvato per essere distribuito in una fase successiva.  
  
> [!NOTE]
> Il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] guidata/Utilità di distribuzione viene installato con [SQL Server Managment Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). Assicurarsi che si usa la versione più recente. Per impostazione predefinita, la versione più recente della procedura guidata distribuzione è installata per \Microsoft SQL Server\140\Tools\Binn\ManagementStudio C:\Program Files (x86). 

## <a name="syntax"></a>Sintassi  
  
```  
  
Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> Argomenti  
 *ASdatabasefile*  
 Percorso completo della cartella in cui si trova il file dello script di distribuzione (con estensione asdatabase) di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Questo file viene generato quando si distribuisce un progetto in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Si trova nella cartella bin del progetto. Nel file .asdatabase sono contenute le definizioni degli oggetti da distribuire. Se omesso, viene utilizzata la cartella corrente.  
  
 **/s**  
 Viene eseguita l'utilità in modalità non interattiva e non viene visualizzata alcuna finestra di dialogo. Per altre informazioni sulle modalità, vedere la sezione [Modalità](#Modes)di seguito in questo argomento.  
  
 *logfile*  
 Percorso completo e nome file del file di log. Gli eventi di traccia verranno registrati nel file di log specificato. Se il file di log esiste già, il relativo contenuto verrà sostituito.  
  
 **/a**  
 Viene eseguita l'utilità in modalità di risposta. Tutte le risposte fornite durante l'esecuzione guidata dell'utilità verranno scritte nei file di input, ma non verrà apportata alcuna modifica alle destinazioni di distribuzione.  
  
 **/o**  
 Viene eseguita l'utilità in modalità output. La distribuzione non verrà eseguita, ma lo script XML for Analysis (XMLA) che in genere viene inviato alle destinazioni di distribuzione viene invece salvato nel file script di output specificato. Se non si specifica *output_script_file* , l'utilità cerca di usare il file script di output specificato nel file di input delle opzioni di distribuzione con estensione deploymentoptions. Se non si specifica un file script di output nel file di input delle opzioni di distribuzione, si verificherà un errore.  
  
 Per altre informazioni sulle modalità, vedere la sezione [Modalità](#Modes)di seguito in questo argomento.  
  
 *output_script_file*  
 Percorso completo e nome file del file script di output.  
  
 **/d**  
 Se si usa l'argomento **/o** , viene specificato che l'utilità non deve connettersi all'istanza di destinazione. Poiché non vengono stabilite connessioni alle destinazioni di distribuzione, lo script di output viene generato solo in base alle informazioni recuperate dai file di input.  
  
> [!NOTE]  
>  L'argomento **/d** viene usato solo nella modalità di output. Questo argomento viene ignorato se specificato in modalità di risposta o automatica. Per altre informazioni sulle modalità, vedere la sezione [Modalità](#Modes)di seguito in questo argomento.  
  
## <a name="remarks"></a>Note  
 L'utilità **Microsoft.AnalysisServices.Deployment** usa un set di file che includono le definizioni degli oggetti, le destinazioni di distribuzione, le opzioni di distribuzione e le impostazioni di configurazione e cerca di distribuire le definizioni degli oggetti alle destinazioni di distribuzione specificate usando le opzioni di distribuzione e le impostazioni di configurazione impostate. Questa utilità può implementare un'interfaccia utente se richiamata in modalità file di risposte o output. Per altre informazioni sull'uso dell'interfaccia utente implementata da questa utilità per creare i file di risposte, vedere [Distribuire soluzioni di modelli tramite la Distribuzione guidata](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md).  
  
 L'utilità si trova nella cartella \Programmi file (x86) \Microsoft SQL Server\140\Binn\ManagementStudio.  
  
##  <a name="Modes"></a> Modalità  
 L'utilità può essere eseguita nelle modalità riportate nella tabella seguente.  
  
|Modalità|Descrizione|  
|----------|-----------------|  
|Modalità automatica|Non viene visualizzata alcuna interfaccia utente e tutte le informazioni necessarie per la distribuzione vengono recuperate dai file di input. In questa modalità lo stato di avanzamento non viene visualizzato. È invece possibile utilizzare un file di log facoltativo per acquisire le informazioni sullo stato e sugli errori per una verifica successiva.|  
|Modalità di risposta|Viene visualizzata l'interfaccia utente Distribuzione guidata e le risposte dell'utente vengono memorizzate nei file di input specificati per la distribuzione successiva. In questa modalità la distribuzione non viene eseguita. Questa modalità ha lo scopo di acquisire le risposte dell'utente.|  
|Modalità output|Non viene visualizzata alcuna interfaccia utente e tutte le informazioni necessarie per la distribuzione vengono recuperate dai file di input.<br /><br /> A differenza della modalità automatica, tuttavia, l'output dell'utilità viene scritto in un file script di output e non inviato alle destinazioni di distribuzione indicate nei file di input. A meno che non venga specificato l'argomento **/d** , l'utilità si connette a ogni destinazione di distribuzione per confrontare i metadati durante la generazione del file script di output.|  
  
 [Torna agli argomenti](#Arguments)  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come distribuire un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità automatica e registrare i messaggi di stato e di errore per una verifica successiva:  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle utilità del prompt dei comandi &#40;motore di database&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
