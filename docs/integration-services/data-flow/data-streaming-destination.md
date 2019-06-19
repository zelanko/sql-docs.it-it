---
title: Destinazione flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 504c05882d1e7c690b8ddbd46c331073f63bbb7c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726996"
---
# <a name="data-streaming-destination"></a>Destinazione flusso di dati

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Destinazione flusso di dati** è un componente di destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) che consente al **provider OLE DB per SSIS** di usare l'output di un pacchetto SSIS come set di risultati tabulare. È possibile creare un server collegato che usa il provider OLE DB per SSIS e quindi eseguire una query SQL su tale server per visualizzare i dati restituiti dal pacchetto SSIS.  
  
 La query dell'esempio seguente restituisce l'output dal pacchetto Package.dtsx nel progetto SSISPackagePublishing nella cartella di Power BI del catalogo SSIS. La query usa il server collegato denominato [Server collegato predefinito per Integration Services] che a sua volta usa il nuovo provider OLE DB per SSIS. La query include il nome della cartella, il nome del progetto e il nome del pacchetto nel catalogo SSIS. Il provider OLE DB per SSIS esegue il pacchetto specificato nella query e restituisce il set di risultati tabulare.  
  
```sql
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>Componenti di pubblicazione del feed di dati  
 I componenti di pubblicazione del feed di dati includono i seguenti: provider OLE DB per SSIS, Destinazione flusso di dati e procedura guidata di pubblicazione di pacchetti SSIS. La procedura guidata consente di pubblicare un pacchetto SSIS come vista SQL in un'istanza del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La procedura agevola la creazione di un server collegato che usa il provider OLE DB per SSIS e di una vista SQL che rappresenta la query sul server collegato. La vista consente di visualizzare i risultati della query dal pacchetto SSIS come set di dati tabulari.  
  
 Per verificare l'installazione del provider SSISOLEDB, in SQL Server Management Studio espandere **Oggetti server**, **Server collegati**, **Provider**e quindi accertarsi che il provider **SSISOLEDB** sia visibile. Fare doppio clic su **SSISOLEDB**, abilitare l'opzione **Consenti in-process** se non è abilitata e quindi fare clic su **OK**.  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>Pubblicare un pacchetto SSIS come vista SQL  
 La procedura seguente descrive i passaggi per la pubblicazione di un pacchetto SSIS come vista SQL.  
  
1.  Creare un pacchetto SSIS con il componente **Destinazione flusso di dati** e distribuire il pacchetto nel catalogo SSIS.  
  
2.  Avviare la **Pubblicazione guidata di pacchetti SSIS** eseguendo ISDataFeedPublishingWizard.exe da C:\Programmi\Microsoft SQL Server\130\DTS\Binn o Pubblicazione guidata feed di dati dal menu Start.  
  
     La procedura guidata crea un server collegato usando il provider OLE DB per SSIS (SSISOLEDB) e quindi crea una vista SQL costituita da una query su tale server. La query include il nome della cartella, il nome del progetto e il nome del pacchetto nel catalogo SSIS.  
  
3.  Eseguire la vista SQL in SQL Server Management Studio ed esaminare i risultati dal pacchetto SSIS. La vista invia la query al provider OLE DB per SSIS usando il server collegato che è stato creato. Il provider OLE DB per SSIS esegue il pacchetto specificato nella query e restituisce il set di risultati tabulare alla query.  
  
> [!IMPORTANT]  
>  Per informazioni dettagliate, vedere [Procedura dettagliata: Pubblicare un pacchetto SSIS come vista SQL](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md).  

## <a name="configure-data-streaming-destination"></a>Configurare Destinazione flusso di dati
  Per configurare Destinazione del flusso di dati si usa la finestra di dialogo **Editor avanzato per Destinazione flusso di dati** . Per aprire questa finestra di dialogo, fare doppio clic sul componente oppure fare clic con il pulsante destro del mouse sul componente nella finestra di progettazione del flusso di dati e quindi scegliere **Modificare**.  
  
 Questa finestra di dialogo contiene tre schede: **Proprietà componente**, **Colonne di input**e **Proprietà input e output**.  
  
## <a name="component-properties-tab"></a>Scheda Proprietà componente  
 Questa scheda contiene i campi modificabili seguenti:  
  
|Campo|Descrizione|  
|-----------|-----------------|  
|nome|Nome del componente Destinazione flusso di dati nel pacchetto.|  
|ValidateExternalMetadata|Indica se il componente viene convalidato usando origini dati esterne in fase di progettazione. Se è impostato su false, la convalida rispetto a origini dati esterne viene posticipata fino alla fase di esecuzione.|  
|IDColumnName|La vista generata dalla Pubblicazione guidata di feed di dati contiene questa colonna ID supplementare. La colonna ID funge da EntityKey per i dati di output del flusso di dati quando i dati vengono utilizzati come feed OData da altre applicazioni.<br /><br /> Il nome predefinito di questa colonna è _ID. È possibile specificare un nome diverso per la colonna ID.|  
  
## <a name="input-columns-tab"></a>Scheda Colonne di input  
 Nel riquadro superiore di questa scheda sono mostrate tutte le colonne di input disponibili. Selezionare le colonne da includere nell'output di questo componente. Le colonne selezionate vengono visualizzate in un elenco nel riquadro inferiore. È possibile modificare il nome della colonna di output immettendo il nuovo nome per il campo **Alias di output** nell'elenco.  
  
## <a name="input-output-properties-tab"></a>Scheda Proprietà input e output  
 Analogamente alla scheda Colonne di input, è possibile modificare i nomi delle colonne di output in questa scheda. Nella visualizzazione albero a sinistra espandere **Input di Destinazione flusso di dati** e quindi espandere **Colonne di input**. Fare clic sul nome della colonna di input e modificare il nome del nome della colonna di output nel riquadro di destra.
