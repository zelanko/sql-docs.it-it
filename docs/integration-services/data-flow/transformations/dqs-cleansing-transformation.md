---
title: Trasformazione DQS Cleansing | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssdqs.designer.cleansing.f1
- sql13.SSDQS.DESIGNER.DQCONNECTION.F1
helpviewer_keywords:
- data correction
- correct data
ms.assetid: d2ec1b1a-c745-4741-b57c-6fdb524a154c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1c3ccadbe443ca555e5386ea3d3434405ae97461
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71291474"
---
# <a name="dqs-cleansing-transformation"></a>Trasformazione DQS Cleansing

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione DQS Cleansing utilizza Data Quality Services (DQS) per correggere i dati da un'origine dati connessa, applicando le regole approvate create per l'origine dati connessa o un'origine dati simile. Per ulteriori informazioni sulle regole di correzione dei dati, vedere [DQS Knowledge Bases and Domains](../../../data-quality-services/dqs-knowledge-bases-and-domains.md). Per ulteriori informazioni su DQS, vedere [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md).  
  
 Per determinare se è necessario correggere i dati, la trasformazione DQS Cleansing elabora i dati da una colonna di input quando le condizioni seguenti sono vere:  
  
-   La colonna è selezionata per la correzione dei dati.  
  
-   Il tipo di dati della colonna è supportato per la correzione dei dati.  
  
-   È stato eseguito il mapping della colonna a un dominio con un tipo di dati compatibile.  
  
 La trasformazione include inoltre un output degli errori da configurare per gestire gli errori a livello di riga. Per configurare l'output degli errori, utilizzare **Editor trasformazione DQS Cleansing**.  
  
 È possibile includere [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) nel flusso di dati per identificare righe di dati che probabilmente sono duplicati.  
  
## <a name="data-quality-projects-and-values"></a>Progetti Data Quality e valori  
 Quando si elaborano i dati con la trasformazione DQS Cleansing, viene creato un progetto di pulizia nel server Data Quality. È possibile utilizzare il client Data Quality per gestire il progetto. Inoltre, è possibile utilizzare il client Data Quality per importare i valori del progetto in un dominio di una Knowledge Base in DQS. È possibile importare i valori solo in un dominio (o dominio collegato) configurato per l'utilizzo dalla trasformazione DQS Cleansing.  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Aprire progetti di Integration Services in Data Quality Client](../../../data-quality-services/open-integration-services-projects-in-data-quality-client.md)  
  
-   [Importare i valori di un progetto di pulizia in un dominio](../../../data-quality-services/import-cleansing-project-values-into-a-domain.md)  
  
-   [Applicare le regole relative alla qualità dei dati all'origine dati](../../../integration-services/data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Aprire, sbloccare, rinominare ed eliminare un progetto Data Quality](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)  
  
-   Articolo relativo alla [pulizia dei dati complessi utilizzando domini compositi](https://social.technet.microsoft.com/wiki/contents/articles/13324.using-dqs-cleansing-complex-data-using-composite-domains.aspx)su social.technet.microsoft.com.  
  
## <a name="dqs-cleansing-transformation-editor-dialog-box"></a>Finestra di dialogo Editor trasformazione DQS Cleansing
  Usare la finestra di dialogo **Editor trasformazione DQS Cleansing** per correggere dati usando Data Quality Services (DQS). Per altre informazioni, vedere [Concetti di Data Quality Services](../../../data-quality-services/data-quality-services-concepts.md).  
  
 **Per saperne di più**  
  
-   [Aprire Editor trasformazione DQS Cleansing](#open)  
  
-   [Impostare le opzioni nella scheda Gestione connessione](#connection)  
  
-   [Impostare le opzioni nella scheda Mapping](#mapping)  
  
-   [Impostare le opzioni nella scheda Avanzate](#advanced)  
  
-   [Impostare le opzioni nella finestra di dialogo Gestione connessione DQS Cleansing](#manager)  
  
###  <a name="open-the-dqs-cleansing-transformation-editor"></a><a name="open"></a> Aprire Editor trasformazione DQS Cleansing  
  
1.  Aggiungere la trasformazione DQS Cleansing al pacchetto [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente e quindi scegliere **Modifica**.  
  
###  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Impostare le opzioni nella scheda Gestione connessione  
 **Gestione connessione Data Quality**  
 Consente di selezionare una gestione connessione DQS esistente nell'elenco oppure di crearne una facendo clic sul pulsante **Nuova**.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Gestione connessione DQS Cleansing** . Per altre informazioni, vedere [Impostare le opzioni nella finestra di dialogo Gestione connessione DQS Cleansing](#manager).  
  
 **Data Quality Knowledge Base**  
 Selezionare una Knowledge Base DQS esistente per l'origine dati connessa. Per altre informazioni sulla Knowledge Base DQS, vedere [Knowledge Base e domini DQS](../../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Crittografia connessione**  
 Consente di specificare se crittografare la connessione, per crittografare il trasferimento dei dati tra il Server DQS e [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 **Domini disponibili**  
 Consente di elencare i domini disponibili per la Knowledge Base selezionata. Esistono due tipi di domini, cioè singoli e composti. In questi ultimi sono contenuti due o più domini singoli.  
  
 Per informazioni su come eseguire il mapping di colonne a domini composti, vedere [Eseguire il mapping delle colonne ai domini compositi](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md).  
  
 Per altre informazioni sui domini, vedere [Knowledge Base e domini DQS](../../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Configura output errori**  
 Consente di specificare come gestire gli errori a livello di riga. Possono verificarsi degli errori quando la trasformazione corregge i dati dall'origine dati connessa, a causa di valori di dati o vincoli di convalida non previsti.  
  
 Di seguito sono riportati i valori validi:  
  
-   **Interrompi componente**: indica che la trasformazione ha esito negativo e che i dati di input non vengono inseriti nel database Data Quality Services. Si tratta del valore predefinito.  
  
-   **Reindirizza riga**: indica che i dati di input non vengono inseriti nel database di Data Quality Services e che vengono reindirizzati all'output degli errori.  
  
###  <a name="set-options-on-the-mapping-tab"></a><a name="mapping"></a> Impostare le opzioni nella scheda Mapping  
 Per informazioni su come eseguire il mapping di colonne a domini composti, vedere [Eseguire il mapping delle colonne ai domini compositi](../../../integration-services/data-flow/transformations/map-columns-to-composite-domains.md).  
  
 **Colonne di input disponibili**  
 Elenca le colonne dall'origine dati connessa. Selezionare una o più colonne contenenti i dati che si desidera correggere.  
  
 **Colonna di input**  
 Elenca una colonna di input selezionata nell'area **Colonne di input disponibili** .  
  
 **Dominio**  
 Consente di selezionare un dominio di cui si desidera eseguire il mapping alle colonne di input.  
  
 **Alias di origine**  
 Consente di visualizzare la colonna di origine contenente il valore della colonna originale.  
  
 Fare clic all'interno del campo per modificare il nome della colonna.  
  
 **Alias di output**  
 Consente di visualizzare la colonna che viene restituita da **Trasformazione DQS Cleansing**. La colonna contiene il valore della colonna originale o il valore corretto.  
  
 Fare clic all'interno del campo per modificare il nome della colonna.  
  
 **Alias di stato**  
 Consente di visualizzare la colonna contenente le informazioni sullo stato per i dati corretti. Fare clic all'interno del campo per modificare il nome della colonna.  
  
###  <a name="set-options-on-the-advanced-tab"></a><a name="advanced"></a> Impostare le opzioni nella scheda Avanzate  
 **Standardizzare output**  
 Consente di specificare se restituire i dati nel formato standardizzato basato sul formato di output definito per i domini. Per altre informazioni sul formato standardizzato, vedere [Pulizia dei dati](../../../data-quality-services/data-cleansing.md).  
  
 **Confidenza**  
 Consente di specificare se includere il livello di confidenza per i dati corretti. Il livello di confidenza indica il livello di certezza di DQS in relazione a correzione o suggerimento. Per altre informazioni sui livelli di confidenza, vedere [Pulizia dei dati](../../../data-quality-services/data-cleansing.md).  
  
 **Motivo**  
 Consente di specificare se includere il motivo per la correzione dei dati.  
  
 **Dati accodati**  
 Consente di specificare se restituire dati aggiuntivi ricevuti da un provider di dati di riferimento esistente. Per altre informazioni, vedere [Reference Data Services in DQS](../../../data-quality-services/reference-data-services-in-dqs.md).  
  
 **Schema dati accodati**  
 Consente di specificare se restituire lo schema dati. Per altre informazioni, vedere [Collegare un dominio o un dominio composito ai dati di riferimento](../../../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md).  
  
###  <a name="set-the-options-in-the-dqs-cleansing-connection-manager-dialog-box"></a><a name="manager"></a> Impostare le opzioni nella finestra di dialogo Gestione connessione DQS Cleansing  
 **Nome server**  
 Selezionare o digitare il nome del server DQS a cui si desidera connettersi. Per altre informazioni sul server, vedere [Amministrazione DQS](../../../data-quality-services/dqs-administration.md).  
  
 **Test connessione**  
 Fare clic per verificare che la connessione specificata sia disponibile.  
  
 È anche possibile aprire la finestra di dialogo **Gestione connessione DQS Cleansing** dall'area relativa alle connessioni eseguendo queste operazioni:  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], aprire un progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] esistente o crearne uno nuovo.  
  
2.  Fare clic con il pulsante destro sull'area relativa alle connessioni, scegliere **Nuova connessione**e quindi fare clic su **DQS**.  
  
3.  Fare clic su **Aggiungi**.  
  
