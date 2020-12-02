---
description: Percorsi in Integration Services
title: Percorsi in Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.patheditor.general.f1
- sql13.dts.designer.patheditor.metadata.f1
- sql13.dts.designer.patheditor.visualizers.f1
helpviewer_keywords:
- paths [Integration Services], about paths
- data flow [Integration Services], paths
- paths [Integration Services]
- destinations [Integration Services], paths
- sources [Integration Services], paths
ms.assetid: 6c4629a9-2ede-4011-9101-3b342249640e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a69d70b9e58458303dbba3444b6a8c38fb40ccc0
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "88495858"
---
# <a name="integration-services-paths"></a>Percorsi in Integration Services

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Un percorso collega due componenti in un flusso di dati connettendo l'output di un componente all'input dell'altro. Un percorso ha un'origine e una destinazione. Se un percorso connette, ad esempio, un'origine OLE DB e una trasformazione Ordinamento, l'origine OLE DB costituirà l'origine del percorso e la trasformazione Ordinamento ne costituirà la destinazione. L'origine è il componente da cui inizia il percorso, mentre la destinazione è il componente in cui termina.  
  
 Se si esegue un pacchetto in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , è possibile visualizzare i dati in un flusso di dati collegando visualizzatori dati a un percorso. Un visualizzatore dati può essere configurato in modo da visualizzare i dati in una griglia. Si tratta di un utile strumento di debug. Per altre informazioni, vedere [Debug di un flusso di dati](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
## <a name="configure-the-path"></a>Configurare il percorso  
 In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] è disponibile la finestra di dialogo **Editor percorso flusso di dati** che consente di impostare le proprietà di un percorso, visualizzare i metadati delle colonne di dati che passano attraverso il percorso e configurare i visualizzatori dati.  
  
 Le proprietà configurabili di un percorso includono nome, descrizione e annotazione. È possibile configurare i percorsi anche a livello di codice. Per altre informazioni, vedere [Connessione dei componenti del flusso di dati a livello di programmazione](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md).  
  
 L'annotazione di un percorso visualizza il nome dell'origine del percorso o il nome del percorso sull'area di progettazione della scheda **Flusso di dati** in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Le annotazioni dei percorsi sono simili a quelle che è possibile aggiungere a flussi di dati, flussi di controllo e gestori di eventi. L'unica differenza è costituita dal fatto che sono collegate a un percorso, mentre le altre annotazioni vengono visualizzate nelle schede **Flusso di dati**, **Flusso di controllo** e **Gestore evento** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 I metadati indicano il nome, il tipo di dati, la precisione, la scala, la lunghezza, la tabella codici e il componente di origine di ogni colonna nell'output del componente precedente. Il componente di origine è il componente del flusso di dati che ha creato la colonna e può anche non essere il primo componente nel flusso di dati. Le trasformazioni Unione input multipli e Ordinamento, ad esempio, creano proprie colonne e costituiscono pertanto l'origine delle relative colonne di output. La trasformazione Copia colonna, invece, può passare colonne senza modificarle oppure creare nuove colonne copiando le colonne di input. La trasformazione Copia colonna costituisce il componente di origine solo per le nuove colonne.  

## <a name="set-the-properties-of-a-path-with-the-data-flow-path-editor"></a>Impostare le proprietà di un percorso tramite l'Editor percorso flusso di dati
I percorsi connettono due componenti flusso di dati. Affinché sia possibile impostare le proprietà di un percorso, il flusso di dati deve contenere almeno due componenti connessi.
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** , quindi fare doppio clic su un percorso.  
  
4.  Nella finestra di dialogo **Editor percorso flusso di dati** fare clic su **Generale**. È possibile modificare il nome predefinito del percorso e specificarne una descrizione. È anche possibile modificare la proprietà PathAnnotation.  
  
5.  Fare clic su **OK**.  
  
6.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  

## <a name="general-page---data-flow-path-editor"></a>Pagina Generale - Editor percorso flusso di dati
Utilizzare la finestra di dialogo **Editor percorso flusso di dati** per impostare le proprietà del percorso, visualizzare i metadati delle colonne e gestire i visualizzatori di dati collegati al percorso.  
  
 Utilizzare il nodo **Generale** della finestra di dialogo **Editor percorso flusso di dati** per assegnare un nome e una descrizione al percorso e per specificare le opzioni relative all'annotazione del percorso.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare un nome univoco per il percorso.  
  
 **ID**  
 L'identificatore di derivazione del percorso. Questa proprietà è di sola lettura.  
  
 **IdentificationString**  
 Stringa che identifica il percorso. Viene generata automaticamente in base al nome immesso sopra.  
  
 **Descrizione**  
 Consente di digitare una descrizione del percorso.  
  
 **PathAnnotation**  
 Specificare il tipo di annotazione da utilizzare. Selezionare **Never** per disabilitare le annotazioni, **AsNeeded** per abilitare le annotazioni su richiesta, **SourceName** per aggiungere automaticamente le annotazioni utilizzando il valore dell'opzione **SourceName** e **PathName** per aggiungere automaticamente le annotazioni utilizzano il valore della proprietà **Nome** .  
  
 **DestinationName**  
 Consente di visualizzare l'input corrispondente alla fine del percorso.  
  
 **SourceName**  
 Indica l'output che corrisponde all'inizio del percorso.  
 
## <a name="metadata-page---data-flow-path-editor"></a>Pagina Metadati - Editor percorso flusso di dati
Utilizzare la pagina **Metadati** della finestra di dialogo **Editor percorso flusso di dati** per visualizzare i metadati delle colonne percorso.  
  
### <a name="options"></a>Opzioni  
 **Metadati percorso**  
 Elenca i metadati delle colonne. Fare clic sulle intestazioni di colonna per ordinarne i dati.  
  
 **Nome**  
 Indica il nome delle colonne.  
  
 **Tipo di dati**  
 Indica il tipo di dati della colonna.  
  
 **Precisione**  
 Indica il numero di cifre in un valore numerico.  
  
 **Ridimensionamento**  
 Indica il numero di cifre a destra del separatore decimale in un valore numerico.  
  
 **Lunghezza**  
 Indica la lunghezza corrente della colonna.  
  
 **Tabella codici**  
 Indica la tabella codici della colonna. Il valore **0** indica che la colonna non utilizza alcuna tabella codici. Ciò si verifica quando i dati sono di tipo Unicode, numerico, data o ora.  
  
 **Posizione chiave ordinamento**  
 Indica la posizione della chiave di ordinamento della colonna. Il valore **0** indica che la colonna non è ordinata.  
  
> [!NOTE]  
>  Il prefisso meno (-) indica che l'ordinamento della colonna è decrescente.  
  
 **Flag di confronto**  
 Elenca i flag di confronto applicati alla colonna.  
  
 **Componente di origine**  
 Indica il componente di flusso di dati che corrisponde all'origine della colonna.  
  
 **Copia negli Appunti**  
 Consente di copiare i metadati della colonna negli Appunti. Per impostazione predefinita, tutte le righe di metadati vengono copiate nell'ordine in cui sono attualmente visualizzate.  
 
## <a name="data-viewers-page---data-flow-path-editor"></a>Pagina Visualizzatori dati - Editor percorso flusso di dati
Utilizzare la pagina **Visualizzatori dati** della finestra di dialogo **Editor percorso flusso di dati** per gestire i visualizzatori di dati associati al percorso.  
  
### <a name="options"></a>Opzioni  
 **Nome**  
 Consente di elencare i visualizzatori di dati.  
  
 **Tipo visualizzatore dati**  
 Consente di elencare il tipo di visualizzatore di dati.  
  
 **Aggiungere**  
 Fare clic per aggiungere un visualizzatore di dati tramite la finestra di dialogo **Configura visualizzatore dati** .  
  
 **Elimina**  
 Consente di eliminare il visualizzatore di dati selezionato.  
  
 **Configurare**  
 Fare clic per configurare il visualizzatore di dati selezionato tramite la finestra di dialogo **Configura visualizzatore dati** .  
 
## <a name="path-properties"></a>Proprietà del percorso
Gli oggetti del flusso di dati nel modello a oggetti [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] hanno proprietà comuni e proprietà personalizzate a livello di componente, input e output, colonne di input e colonne di output. Molte proprietà hanno valori di sola lettura assegnati in fase di esecuzione dal motore del flusso di dati.  
  
 In questo argomento vengono elencate e descritte le proprietà personalizzate dei percorsi che connettono gli oggetti del flusso di dati.  
  
### <a name="custom-properties-of-a-path"></a>Proprietà personalizzate di un percorso  
 Nel modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] un percorso che connette componenti nel flusso di dati implementa l'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100>.  
  
 Nella tabella seguente vengono descritte le proprietà configurabili dei percorsi in un flusso di dati. Inoltre, il motore del flusso di dati assegna valori a proprietà di sola lettura aggiuntive che non sono elencate qui.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|PathAnnotation|Integer (enumerazione)|Un valore che indica se un'annotazione deve essere visualizzata con il percorso sulla superficie dell'area di progettazione. I valori possibili sono **AsNeeded**, **SourceName**, **PathName** e **Never**. Il valore predefinito è **AsNeeded**.|  
|DestinationName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>|L'input associato al percorso.|  
|SourceName|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>|L'output associato al percorso.|  
