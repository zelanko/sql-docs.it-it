---
title: Creare un dominio composito | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.createcd.f1
- sql13.dqs.dm.cdproperties.f1
ms.assetid: c7f0bd84-a02e-4a81-885d-985e6415c499
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 81173982e9c44b135a3ba98312839ac799461988
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52616861"
---
# <a name="create-a-composite-domain"></a>Creazione di un dominio composito

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come creare un dominio composito in una Knowledge Base in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Un dominio composito è costituito da uno o più singoli domini che si applicano a un singolo campo di dati. Per informazioni dettagliate sui domini compositi, vedere [Gestione di un dominio composito](../data-quality-services/managing-a-composite-domain.md).  
  
 Sono disponibili due modi per creare un nuovo dominio composito. Il primo viene utilizzato durante il passaggio di mapping dell'attività di individuazione delle informazioni, quando è in corso l'analisi di un campione di dati per aggiungere informazioni a una Knowledge Base nuova o esistente. Il secondo viene utilizzato durante l'attività di gestione del dominio, quando anziché modificare un dominio esistente, se ne crea uno nuovo. Per creare un dominio composito, è necessario avere già creato almeno due singoli domini da aggiungere al dominio composito. Quando si crea un nuovo dominio composito, sono disponibili solo i singoli domini che sono già stati creati e che non sono stati aggiunti a un dominio composito esistente. Non è possibile aggiungere un singolo dominio a più di un dominio composito così come non è possibile aggiungere un dominio composito a un altro dominio composito.  
  
 Dopo aver creato un dominio composito, è possibile modificarne le proprietà, allegarvi un servizio dati di riferimento, creare regole tra domini o relazioni di valori. A tale scopo, selezionare il dominio composito nell'elenco **Dominio** della pagina **Gestione dominio** , quindi selezionare la scheda appropriata.  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
 Per creare un dominio composito, è necessario avere creato e aperto una Knowledge Base e almeno due singoli domini da aggiungere al dominio composito.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN per creare un dominio composito.  
  
##  <a name="ParsingKnowledgeDiscoveryActivity"></a> Creazione di un dominio composito nell'attività di individuazione delle informazioni  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale di [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , fare clic su **Apri Knowledge Base** , quindi selezionare una Knowledge Base o fare clic su **Nuova Knowledge Base** e immettere le proprietà per la nuova Knowledge Base.  
  
3.  Selezionare **Individuazione informazioni** come attività, quindi fare clic su **Crea** per creare la nuova Knowledge Base, oppure **Apri** per aprirne una esistente.  
  
4.  Nella pagina **Mappa** specificare una connessione all'origine dati. Per ulteriori informazioni, vedere [Perform Knowledge Discovery](../data-quality-services/perform-knowledge-discovery.md).  
  
5.  Nella tabella **Mapping** selezionare una colonna di origine dall'elenco a discesa per la **Colonna di origine** di una riga vuota. Verificare che la colonna di origine contenga un dominio composito indirizzato da due singoli domini esistenti. Se non esiste alcun dominio singolo corrispondente, fare clic sull'icona **Crea un dominio** .  
  
6.  Nella tabella **Mapping** selezionare una colonna di origine dall'elenco a discesa per la **Colonna di origine** di una riga vuota. Verificare che la colonna di origine contenga un dominio composito con parti indirizzate da due singoli domini esistenti. Se non esistono singoli domini corrispondenti, fare clic sull'icona **Crea un dominio** per crearli. Per altre informazioni, vedere [Creazione di un dominio](../data-quality-services/create-a-domain.md).  
  
7.  Fare clic sull'icona **Crea un dominio composito** .  
  
##  <a name="DomainManagementActivity"></a> Creazione di un dominio composito nell'attività di gestione del dominio  
  
1.  Nella home page di del client Data Quality Services, fare clic su **Apri Knowledge Base** , quindi selezionare una Knowledge Base o fare clic su **Nuova Knowledge Base** e immettere le proprietà per la nuova Knowledge Base.  
  
2.  Selezionare **Gestione dominio** come attività, quindi fare clic su **Crea** per creare la nuova Knowledge Base, oppure **Apri** per aprirne una esistente.  
  
3.  Assicurarsi che esistano due o più singoli domini, necessari per il dominio composito. Se non ne esistono, fare clic sull'icona **Crea un dominio** e crearli. Per altre informazioni, vedere [Creazione di un dominio](../data-quality-services/create-a-domain.md).  
  
4.  Nella pagina **Gestione dominio** , fare clic sull'icona **Crea un dominio composito** sopra l'elenco di domini.  
  
5.  Immettere un nome univoco per la Knowledge Base e una descrizione di un massimo di 256 caratteri.  
  
6.  In **Elenco di domini**, selezionare i domini che faranno parte del dominio composito e fare clic sulla freccia a destra per spostarli nella tabella **Domini nel dominio composito** .  
  
7.  Fare clic su **OK**.  
  
##  <a name="CompositeDomainProperties"></a> Impostazione delle proprietà di un dominio composito  
  
1.  Nella finestra di dialogo **Crea un dominio composito** immettere un nome univoco per la Knowledge Base e una descrizione di un massimo di 256 caratteri.  
  
2.  In **Elenco di domini**, selezionare i domini che faranno parte del dominio composito e fare clic sulla freccia a destra per spostarli nella tabella **Domini nel dominio composito** . Si tratta di un elenco di singoli domini disponibili per l'aggiunta al dominio composito che si sta creando. Sono disponibili solo i singoli domini che sono già stati creati e che non sono stati aggiunti a un dominio composito esistente. Non è possibile aggiungere un singolo dominio a più di un dominio composito nella Knowledge Base, così come non è possibile aggiungere un dominio composito a un altro dominio composito.  
  
3.  Fare clic su **Avanzate**.  
  
4.  Selezionare una delle opzioni seguenti come **Metodo di analisi**:  
  
    -   **Dati di riferimento**: analizza i valori del campo in base a come i dati vengono formattati dal servizio dati di riferimento. Data Quality Services invia i valori nel dominio composito al servizio dati di riferimento e quest'ultimo restituisce i dati corretti e analizzati in base al dominio nel dominio composito.  
  
    -   **In ordine**: analizza i valori del campo in base all'ordine dei domini nel dominio composito. Il primo valore verrà incluso nel primo dominio, il secondo valore nel secondo e così via.  
  
    -   **Delimitatori**: analizza i valori del campo in base al delimitatore selezionato dai pulsanti di opzione visualizzati quando viene selezionata l'opzione Delimitatori. Il valore può essere **Tabulazione**, **Punto e virgola**, **Virgola**, **Spazio**o **Altro**. Se il valore è **Altro**, immettere il valore che servirà come delimitatore.  
  
5.  Se è stato selezionato **Delimitatori** per il metodo di analisi, è inoltre possibile selezionare **Usa analisi Knowledge Base**. Per altre informazioni, vedere [Knowledge-Based Parsing](#KnowledgeBaseParsing).  
  
6.  Fare clic su **Fine** per completare l'attività di gestione del dominio, come descritto in [Sospensione dell'attività di gestione del dominio](https://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0).  
  
##  <a name="FollowUp"></a> Completamento: Dopo la creazione di un dominio composito  
 Dopo avere creato un dominio composito, è possibile eseguire ulteriori attività di gestione sul dominio, quali l'individuazione delle informazioni per aggiungere informazioni o l'aggiunta di criteri di corrispondenza al dominio. Per altre informazioni, vedere [Eseguire l'individuazione delle informazioni](../data-quality-services/perform-knowledge-discovery.md), [Gestione di un dominio](../data-quality-services/managing-a-domain.md) o [Creare criteri di corrispondenza](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="KnowledgeBaseParsing"></a> Knowledge-Based Parsing  
 Data Quality Services consente di analizzare i dati in base alle informazioni e non solo in base al delimitatore o all'ordine. L'analisi basata sulle informazioni viene utilizzata quando viene eseguito il mapping di dati di origine complessi a un dominio composito e non si utilizzano servizi dati di riferimento. È possibile utilizzare l'analisi basata sulle informazioni per analizzare i dati dall'origine dati nei singoli domini interessati. Con l'analisi basata sulle informazioni, DQS tenterà in primo luogo di utilizzare le informazioni per analizzare dati complessi nei singoli domini. Se possibile, verranno identificate parti della stringa in uno o più domini e la stringa verrà analizzata nei vari domini. Si supponga ad esempio di disporre di un valore complesso denominato "John B. Doe" in un campo di nome completo rappresentato da un dominio composito Full Name. Se DQS identifica "John" come nel dominio Nome e "Doe" come nel dominio Cognome, verrà aggiunto "B". al dominio Secondo nome in base alle informazioni del dominio.  
  
 È possibile utilizzare l'analisi basata sulle informazioni solo se si seleziona anche l'analisi basata su delimitatore. L'analisi basata sulle informazioni non sostituisce l'analisi basata su delimitatore, ma la rende più efficace. Solo nel caso in cui non esistano informazioni per tale tipo di esecuzione DQS utilizzerà un delimitatore per eseguire l'analisi. In alcune circostanze, DQS può effettuare alcune analisi mediante analisi basata sulle informazioni e altre mediante analisi basata su delimitatore.  
  
 L'analisi basata sulle informazioni può essere utilizzata quando il dominio composito è costituito da domini stringa o da una combinazione di tipi diversi di domini (int, date, time e così via). Se l'origine dati è costituita da tipi diversi di dati, l'analisi deve essere eseguita prima per i tipi di dati non di tipo stringa, quindi, come descritto sopra, in base alle informazioni di dominio per il resto dei dati.  
  
 Quando si utilizza l'analisi basata sulle informazioni e sono presenti meno valori nei dati di origine di quanti sono i domini nel dominio composito, DQS inserirà un valore Null nel dominio mancante. Quando sono presenti più valori nei dati di origine di quanti sono i domini nel dominio composito, DQS aggiungerà i dati aggiuntivi a una delle colonne. Se due o più domini includono gli stessi valori, l'origine dati verrà analizzata fino al primo dominio corrispondente.  
  
  
