---
title: Finestra di dialogo Editor trasformazione pulizia DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssdqs.designer.cleansing.f1
- SQL12.SSDQS.DESIGNER.DQCONNECTION.F1
ms.assetid: 07e79641-71ee-45d0-a9ba-ed6f9f68f333
author: janinezhang
ms.author: janinez
ms.openlocfilehash: eaff1c5ac8ae5a804f546fc5e551dcb62e2fda7a
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966907"
---
# <a name="dqs-cleansing-transformation-editor-dialog-box"></a>Finestra di dialogo Editor trasformazione DQS Cleansing
  Usare la finestra di dialogo **Editor trasformazione DQS Cleansing** per correggere dati usando Data Quality Services (DQS). Per altre informazioni, vedere [Concetti di Data Quality Services](../../2014/data-quality-services/data-quality-services-concepts.md).  
  
 Per altre informazioni sulla trasformazione, vedere [Trasformazione DQS Cleansing](data-flow/transformations/dqs-cleansing-transformation.md).  
  
 **Per saperne di più**  
  
-   [Aprire Editor trasformazione DQS Cleansing](#open)  
  
-   [Impostare le opzioni nella scheda Gestione connessione](#connection)  
  
-   [Impostare le opzioni nella scheda Mapping](#mapping)  
  
-   [Impostare le opzioni nella scheda Avanzate](#advanced)  
  
-   [Impostare le opzioni nella finestra di dialogo Gestione connessione DQS Cleansing](#manager)  
  
##  <a name="open-the-dqs-cleansing-transformation-editor"></a><a name="open"></a>Aprire l'Editor trasformazione DQS cleaning  
  
1.  Aggiungere la trasformazione DQS Cleansing al pacchetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente e quindi scegliere **Modifica**.  
  
##  <a name="set-options-on-the-connection-manager-tab"></a><a name="connection"></a> Impostare le opzioni nella scheda Gestione connessione  
 **Gestione connessione Data Quality**  
 Consente di selezionare una gestione connessione DQS esistente nell'elenco oppure di crearne una facendo clic sul pulsante **Nuova**.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Gestione connessione DQS Cleansing** . Per altre informazioni, vedere [Impostare le opzioni nella finestra di dialogo Gestione connessione DQS Cleansing](#manager).  
  
 **Data Quality Knowledge Base**  
 Selezionare una Knowledge Base DQS esistente per l'origine dati connessa. Per altre informazioni sulla Knowledge Base DQS, vedere [Knowledge Base e domini DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Crittografa connessione**  
 consente di specificare se crittografare la connessione, per crittografare il trasferimento dei dati tra il server DQS e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 **Domini disponibili**  
 Consente di elencare i domini disponibili per la Knowledge Base selezionata. Esistono due tipi di domini, cioè singoli e composti. In questi ultimi sono contenuti due o più domini singoli.  
  
 Per informazioni su come eseguire il mapping di colonne a domini composti, vedere [Eseguire il mapping delle colonne ai domini compositi](data-flow/transformations/map-columns-to-composite-domains.md).  
  
 Per altre informazioni sui domini, vedere [Knowledge Base e domini DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
 **Configura output errori**  
 Consente di specificare come gestire gli errori a livello di riga. Possono verificarsi degli errori quando la trasformazione corregge i dati dall'origine dati connessa, a causa di valori di dati o vincoli di convalida non previsti.  
  
 Di seguito sono riportati i valori validi:  
  
-   **Interrompi componente**: indica che la trasformazione ha esito negativo e che i dati di input non vengono inseriti nel database Data Quality Services. Si tratta del valore predefinito.  
  
-   **Reindirizza riga**: indica che i dati di input non vengono inseriti nel database di Data Quality Services e che vengono reindirizzati all'output degli errori.  
  
##  <a name="set-options-on-the-mapping-tab"></a><a name="mapping"></a>Impostare le opzioni nella scheda mapping  
 Per informazioni su come eseguire il mapping di colonne a domini composti, vedere [Eseguire il mapping delle colonne ai domini compositi](data-flow/transformations/map-columns-to-composite-domains.md).  
  
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
  
##  <a name="set-options-on-the-advanced-tab"></a><a name="advanced"></a>Impostare le opzioni nella scheda Avanzate  
 **Standardizzare output**  
 Consente di specificare se restituire i dati nel formato standardizzato basato sul formato di output definito per i domini. Per altre informazioni sul formato standardizzato, vedere [Pulizia dei dati](../../2014/data-quality-services/data-cleansing.md).  
  
 **Fiducia**  
 Consente di specificare se includere il livello di confidenza per i dati corretti. Il livello di confidenza indica il livello di certezza di DQS in relazione a correzione o suggerimento. Per altre informazioni sui livelli di confidenza, vedere [Pulizia dei dati](../../2014/data-quality-services/data-cleansing.md).  
  
 **Motivo**  
 Consente di specificare se includere il motivo per la correzione dei dati.  
  
 **Dati accodati**  
 Consente di specificare se restituire dati aggiuntivi ricevuti da un provider di dati di riferimento esistente. Per altre informazioni, vedere [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md).  
  
 **Schema dati accodati**  
 Consente di specificare se restituire lo schema dati. Per ulteriori informazioni, vedere [la pagina relativa alla connessione di un dominio o un dominio composito ai dati di riferimento](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="set-the-options-in-the-dqs-cleansing-connection-manager-dialog-box"></a><a name="manager"></a>Impostare le opzioni nella finestra di dialogo Gestione connessione DQS cleaning  
 **Nome server**  
 Selezionare o digitare il nome del server DQS a cui si desidera connettersi. Per altre informazioni sul server, vedere [Amministrazione DQS](../../2014/data-quality-services/dqs-administration.md).  
  
 **Test connessione**  
 Fare clic per verificare che la connessione specificata sia disponibile.  
  
 È anche possibile aprire la finestra di dialogo **Gestione connessione DQS Cleansing** dall'area relativa alle connessioni eseguendo queste operazioni:  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], aprire un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] esistente o crearne uno nuovo.  
  
2.  Fare clic con il pulsante destro sull'area relativa alle connessioni, scegliere **Nuova connessione**e quindi fare clic su **DQS**.  
  
3.  Scegliere **Aggiungi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Applicazione delle regole relative alla qualità dei dati all'origine dati](data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
  
