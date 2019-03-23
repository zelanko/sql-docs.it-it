---
title: Distribuzione di progetti e pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a2212b44af9eb17625ef296deb9d6223deb313e1
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380949"
---
# <a name="deployment-of-projects-and-packages"></a>Distribuzione di progetti e pacchetti
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supporta due modelli di distribuzione, il modello di distribuzione del progetto e il modello di distribuzione del pacchetto. Tramite il modello di distribuzione del progetto è possibile distribuire i progetti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Per altre informazioni sulla distribuzione di progetti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vedere [Distribuire progetti nel server Integration Services](../deploy-projects-to-integration-services-server.md).  
  
 Per altre informazioni sul modello di distribuzione del pacchetto, vedere [pacchetto di distribuzione &#40;SSIS&#41;](legacy-package-deployment-ssis.md).  
  
## <a name="compare-project-deployment-and-package-deployment"></a>Eseguire un confronto tra la distribuzione del progetto e quella del pacchetto  
 Il tipo di modello di distribuzione scelto determina le opzioni di sviluppo e amministrazione disponibili per il progetto. Nella tabella seguente vengono illustrate le differenze e le similitudini tra l'utilizzo del modello di distribuzione del progetto e quello del pacchetto.  
  
|Utilizzo del modello di distribuzione del progetto|Utilizzo del modello di distribuzione del pacchetto|  
|---------------------------------------------|---------------------------------------------|  
|L'unità di distribuzione è un progetto.|L'unità di distribuzione è un pacchetto.|  
|Per assegnare valori alle proprietà del pacchetto si utilizzano i parametri.|Per assegnare valori alle proprietà del pacchetto si utilizzano le configurazioni.|  
|Un progetto, contenente pacchetti e parametri, viene compilato su un file di distribuzione del progetto (estensione ispac).|I pacchetti (estensione dtsx) e le configurazioni (estensione dtsConfig) vengono salvati singolarmente nel file system.|  
|Un progetto, contenente pacchetti e parametri, viene distribuito nel catalogo SSISDB in un'istanza di SQL Server.|I pacchetti e le configurazioni vengono copiati nel file system in un altro computer. I pacchetti possono anche essere salvati nel database MSDB in un'istanza di SQL Server.|  
|L'integrazione con CLR è necessaria nel motore di database.|L'integrazione con CLR non è necessaria nel motore di database.|  
|I valori dei parametri specifici dell'ambiente vengono archiviati nelle variabili di ambiente.|I valori di configurazione specifici dell'ambiente vengono archiviati nei file di configurazione.|  
|I progetti e i pacchetti nel catalogo possono essere convalidati nel server prima dell'esecuzione. È possibile utilizzare SQL Server Management Studio, le stored procedure o il codice gestito per eseguire la convalida.|I pacchetti vengono convalidati appena prima dell'esecuzione. È anche possibile convalidare un pacchetto con dtExec o codice gestito.|  
|I pacchetti vengono eseguiti avviando un'esecuzione nel motore di database. L'identificatore di un progetto, i valori di parametri espliciti (facoltativi) e i riferimenti all'ambiente (facoltativi) vengono assegnati a un'esecuzione prima dell'avvio.<br /><br /> I pacchetti possono anche essere eseguiti utilizzando `dtExec`.|I pacchetti vengono eseguiti utilizzando le utilità di esecuzione `dtExec` e `DTExecUI`. Le configurazioni applicabili vengono identificate tramite argomenti del prompt dei comandi (facoltativo).|  
|Durante l'esecuzione, gli eventi generati dal pacchetto vengono acquisiti automaticamente e salvati nel catalogo. È possibile eseguire query su questi eventi con le viste Transact-SQL.|Durante l'esecuzione, gli eventi generati da un pacchetto non vengono acquisiti automaticamente. Per acquisire gli eventi, è necessario aggiungere un provider di log al pacchetto.|  
|I pacchetti vengono eseguiti in un processo di Windows separato.|I pacchetti vengono eseguiti in un processo di Windows separato.|  
|Per pianificare l'esecuzione dei pacchetti si utilizza SQL Server Agent.|Per pianificare l'esecuzione dei pacchetti si utilizza SQL Server Agent.|  
  
## <a name="features-of-project-deployment-model"></a>Funzionalità del modello di distribuzione del progetto  
 Nella tabella seguente sono elencate le funzionalità disponibili per i progetti sviluppati solo per il modello di distribuzione del progetto.  
  
|Funzionalità|Descrizione|  
|-------------|-----------------|  
|Parametri|Un parametro specifica i dati che verranno utilizzati da un pacchetto. È possibile determinare l'ambito dei parametri a livello di pacchetto o di progetto, rispettivamente con i parametri di pacchetto e i parametri di progetto. I parametri possono essere utilizzati in espressioni o attività. Quando il progetto viene distribuito nel catalogo, è possibile assegnare un valore letterale a ogni parametro oppure utilizzare il valore predefinito assegnato in fase di progettazione. Al posto di un valore letterale, è anche possibile fare riferimento a una variabile di ambiente. I valori delle variabili di ambiente vengono risolti al momento dell'esecuzione del pacchetto.|  
|Ambienti|Un ambiente è un contenitore di variabili a cui i progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] possono fare riferimento. Ogni progetto può presentare più riferimenti all'ambiente, tuttavia una singola istanza di esecuzione del pacchetto può fare riferimento solo alle variabili di un ambiente. Gli ambienti consentono di organizzare i valori assegnati a un pacchetto. È ad esempio possibile disporre di ambienti denominati "Dev", "test" e "Produzione".|  
|Variabili di ambiente|Una variabile di ambiente definisce un valore letterale che è possibile assegnare a un parametro durante l'esecuzione del pacchetto. Per utilizzare una variabile di ambiente, creare un riferimento all'ambiente (nel progetto che corrisponde all'ambiente con il parametro), assegnare un valore di parametro al nome della variabile di ambiente, quindi specificare il riferimento all'ambiente corrispondente quando si configura un'istanza di esecuzione.|  
|Catalogo SSISDB|Tutti gli oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] vengono archiviati e gestiti in un'istanza di SQL Server in un database noto come catalogo SSISDB. Il catalogo consente di utilizzare cartelle per organizzare progetti e ambienti. Ogni istanza di SQL Server può disporre di un catalogo. Ogni catalogo può contenere zero o più cartelle. Ogni cartella può contenere zero o più progetti e zero o più ambienti. Una cartella del catalogo può anche essere utilizzata come limite per le autorizzazioni per gli oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|Viste e stored procedure del catalogo|È possibile utilizzare diverse stored procedure e viste per gestire gli oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel catalogo. È ad esempio possibile specificare valori per parametri e variabili di ambiente, creare e avviare esecuzioni e monitorare le operazioni del catalogo. È inoltre possibile sapere esattamente quali valori verranno utilizzati da un pacchetto prima dell'avvio dell'esecuzione.|  
  
## <a name="project-deployment"></a>Distribuzione del progetto  
 Al centro del modello di distribuzione del progetto si trova il file di distribuzione con estensione ispac. Il file di distribuzione del progetto è un'unità di distribuzione autonoma che include solo le informazioni essenziali sui pacchetti e i parametri del progetto. Il file di distribuzione del progetto non acquisisce tutte le informazioni contenute nel file di progetto di Integration Services (estensione dtproj). Ad esempio, i file di testo aggiuntivi che si utilizzano per la scrittura di note non vengono archiviati nel file di distribuzione del progetto, pertanto non vengono distribuiti nel catalogo.  
  
## <a name="required-tasks"></a>Attività richieste  
  
-   [Distribuire progetti nel server Integration Services](../deploy-projects-to-integration-services-server.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog sulle [opinioni relative alle strategie di diramazione per i progetti SSIS](https://go.microsoft.com/fwlink/?LinkId=245739)sul sito Web mattmasson.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità dtexec](dtexec-utility.md)  
  
  
