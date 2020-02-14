---
title: Destinazione elaborazione dimensione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dimensionprocessingdest.f1
- sql13.dts.designer.dimprocessingtransformation.connection.f1
- sql13.dts.designer.dimprocessingtransformation.mappings.f1
- sql13.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing destination
- loading dimensions
- destinations [Integration Services], Dimension Processing
- dimensions [Analysis Services], processing
ms.assetid: 4c49bb95-7259-42f4-a785-bb6aaf5f8566
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ef381f9ff470422ed85b81832b1078d6c8767dcf
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71292878"
---
# <a name="dimension-processing-destination"></a>destinazione elaborazione dimensione

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione elaborazione dimensione consente di caricare ed elaborare una dimensione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per altre informazioni sulle dimensioni, vedere [Dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data).  
  
 La destinazione elaborazione dimensione include le caratteristiche seguenti:  
  
-   Opzioni per l'esecuzione di elaborazioni incrementali, complete o di aggiornamento.  
  
-   Configurazione degli errori, per specificare se l'elaborazione della dimensione deve ignorare gli errori o arrestarsi dopo un numero di errori specificato.  
  
-   Mapping di colonne di input a colonne nelle tabelle delle dimensioni.  
  
 Per altre informazioni sull'elaborazione degli oggetti [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Opzioni e impostazioni di elaborazione &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services).  
  
## <a name="configuration-of-the-dimension-processing-destination"></a>Configurazione della destinazione Elaborazione dimensione  
 La destinazione Elaborazione dimensione utilizza una gestione connessione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per connettersi al progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene le dimensioni elaborate dalla destinazione. Per altre informazioni, vedere [Gestione connessione Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Questa destinazione include un input. Non supporta un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di programmazione, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="dimension-processing-destination-editor-connection-manager-page"></a>Editor destinazione elaborazione dimensione (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione elaborazione dimensione** per specificare una connessione a un progetto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
### <a name="options"></a>Opzioni  
 **Connection manager**  
 Consente di selezionare una gestione connessione esistente nell'elenco o di creare una nuova gestione connessione facendo clic su **Nuova** .  
  
 **Nuovo**  
 Consente di creare una connessione usando la finestra di dialogo **Aggiungi gestione connessione Analysis Services** .  
  
 **Elenco delle dimensioni disponibili**  
 Consente di selezionare la dimensione da elaborare.  
  
 **Metodo di elaborazione**  
 Consente di selezionare la modalità di elaborazione da applicare alla dimensione selezionata nell'elenco. Il valore predefinito di questa opzione è **Completo**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Aggiunta (incrementale)**|Consente di eseguire un'elaborazione incrementale della dimensione.|  
|**Completo**|Consente di eseguire un'elaborazione completa della dimensione.|  
|**Aggiornamento**|Consente di eseguire un'elaborazione di aggiornamento della dimensione.|  
  
## <a name="dimension-processing-destination-editor-mappings-page"></a>Editor destinazione elaborazione dimensione (pagina Mapping)
  Utilizzare la pagina **Mapping** della finestra di dialogo **Editor destinazione elaborazione dimensione** per eseguire il mapping tra le colonne di input e le colonne delle dimensioni.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di input disponibili nella tabella e le colonne di destinazione.  
  
 **Colonne di destinazione disponibili**  
 Consente di visualizzare l'elenco delle colonne di destinazione disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di destinazione disponibili nella tabella e le colonne di input.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate nella tabella precedente. È possibile modificare i mapping utilizzando l'elenco **Colonne di input disponibili**.  
  
 **Colonna di destinazione**  
 Consente di visualizzare tutte le colonne di destinazione disponibili, indicando se sono mappate o meno.  
  
## <a name="dimension-processing-destination-editor-advanced-page"></a>Editor destinazione elaborazione dimensione (pagina Avanzate)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor destinazione elaborazione dimensione** per configurare la gestione degli errori.  
  
### <a name="options"></a>Opzioni  
 **Usa configurazione errori predefinita**  
 Consente di specificare se utilizzare la gestione degli errori predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Il valore predefinito è **True**.  
  
 **Azione per errore chiave**  
 Consente di specificare la modalità di gestione dei record che hanno valori di chiave non validi.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**ConvertToUnknown**|Consente di convertire il valore di chiave non valido nel valore **UnknownMember** .|  
|**DiscardRecord**|Consente di scartare il record.|  
  
 **Ignora errori**  
 Consente di specificare che gli errori devono essere ignorati.  
  
 **Arresta in caso di errore**  
 Consente di specificare che l'elaborazione deve essere arrestata al verificarsi di un errore.  
  
 **Numero di errori**  
 Consente di specificare la soglia di errore alla quale l'elaborazione deve arrestarsi quando è stata selezionata l'opzione **Arresta in caso di errore**.  
  
 **Azione in caso di errore**  
 Consente di specificare l'azione che deve essere intrapresa al raggiungimento della soglia di errore quando è stata selezionata l'opzione **Arresta in caso di errore**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**StopProcessing**|Consente di arrestare l'elaborazione.|  
|**StopLogging**|Consente di arrestare la registrazione degli errori.|  
  
 **Chiave non trovata**  
 Consente di specificare l'azione che deve essere intrapresa per un errore di chiave non trovata. Il valore predefinito è **ReportAndContinue**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave duplicata**  
 Consente di specificare l'azione che deve essere intrapresa per un errore di chiave duplicata. Il valore predefinito è **IgnoreError**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave Null convertita in sconosciuta**  
 Consente di specificare l'azione che deve essere intrapresa quando una chiave Null è stata convertita nel valore **UnknownMember** . Il valore predefinito è **IgnoreError**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave Null non consentita**  
 Consente di specificare l'azione che deve essere intrapresa quando viene incontrata una chiave Null e le chiavi Null non sono consentite. Il valore predefinito è **ReportAndContinue**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Percorso log degli errori**  
 Consente di digitare il percorso del log degli errori o di selezionare una destinazione con il pulsante **Sfoglia (...)** .  
  
 **Sfoglia (...)**  
 Consente di selezionare il percorso del log degli errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
