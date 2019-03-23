---
title: Creare i parametri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.parameterwindow.f1
ms.assetid: cd5d675b-dd5d-49cc-8b1f-dc717a973f99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e1cc5bfb5388cd71ca3217bd060e3dde0428f36
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392139"
---
# <a name="create-parameters"></a>Create Parameters
  Usare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare parametri di progetto e parametri di pacchetto. Le procedure riportate di seguito contengono istruzioni dettagliate per la creazione di parametri di pacchetto/progetto.  
  
> [!NOTE]  
>  Se si converte un progetto creato con una versione precedente di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nel modello di distribuzione del progetto, è possibile usare la **Conversione guidata progetto di Integration Services** per creare parametri basati su configurazioni. Per altre informazioni, vedere [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
### <a name="to-create-package-parameters"></a>Per creare parametri del pacchetto  
  
1.  Aprire il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] e quindi fare clic sulla scheda **Parametri** in Progettazione SSIS.  
  
     ![Scheda dei parametri del pacchetto](media/denali-package-parameters.gif "Scheda dei parametri del pacchetto")  
  
2.  Fare clic sul pulsante **Aggiungi parametro** sulla barra degli strumenti.  
  
     ![Pulsante di aggiunta sulla barra degli strumenti](media/denali-parameter-add.gif "Pulsante di aggiunta sulla barra degli strumenti")  
  
3.  Immettere i valori per le proprietà **Nome**, **Tipo di dati**, **Valore**, **Sensibile** e **Richiesto** nell'elenco stesso o nella finestra **Proprietà**. Nella tabella seguente vengono descritte tali proprietà.  
  
    |Proprietà|Descrizione|  
    |--------------|-----------------|  
    |nome|Nome del parametro.|  
    |Tipo di dati|Tipo di dati del parametro.|  
    |Valore predefinito|Valore predefinito del parametro assegnato in fase di progettazione. Noto anche come valore predefinito di progettazione.|  
    |Sensibile|I valori di parametri sensibili sono crittografati nel catalogo e risultano NULL quando vengono visualizzati con Transact-SQL o con SQL Server Management Studio.|  
    |Obbligatorio|Richiede che un valore diverso dal valore predefinito di progettazione venga specificato prima dell'esecuzione del pacchetto.|  
    |Descrizione|Per manutenzione, la descrizione del parametro. In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], impostare la descrizione del parametro nella finestra Proprietà di Visual Studio quando il parametro viene selezionato nella finestra dei parametri applicabile.|  
  
    > [!NOTE]  
    >  Quando si distribuisce un progetto nel catalogo, molte più proprietà vengono associate al progetto. Per visualizzare tutte le proprietà di tutti i parametri nel catalogo, usare la vista [catalog.object_parameters &#40;database SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database).  
  
4.  Salvare il progetto per salvare le modifiche ai parametri. I valori dei parametri vengono archiviati nel file di progetto.  
  
    > [!WARNING]  
    >  È possibile modificare direttamente l'elenco oppure usare la finestra **Proprietà** per modificare i valori delle proprietà dei parametri. È possibile eliminare un parametro tramite il pulsante **Elimina (X)**. Utilizzando l'ultimo pulsante della barra degli strumenti, è possibile specificare un valore per un parametro utilizzato solo quando si esegue il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
    > [!NOTE]  
    >  Se si riapre il file di pacchetto senza aprire il progetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], la scheda **Parametri** sarà vuota e disabilitata.  
  
### <a name="to-create-project-parameters"></a>Per creare parametri del progetto  
  
1.  Aprire il progetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse su **Project.params** in Esplora soluzioni e quindi scegliere **Apri** (OPPURE) fare doppio clic su **Project.params** per aprirlo.  
  
     ![Finestra dei parametri di progetto](media/denali-project-parameters.gif "Finestra dei parametri di progetto")  
  
3.  Fare clic sul pulsante **Aggiungi parametro** sulla barra degli strumenti.  
  
     ![Pulsante di aggiunta sulla barra degli strumenti](media/denali-parameter-add.gif "Pulsante di aggiunta sulla barra degli strumenti")  
  
4.  Immettere valori per le proprietà **Nome**, **Tipo di dati**, **Valore**, **Sensibile** e **Richiesto**.  
  
    |Proprietà|Descrizione|  
    |--------------|-----------------|  
    |nome|Nome del parametro.|  
    |Tipo di dati|Tipo di dati del parametro.|  
    |Valore predefinito|Valore predefinito del parametro assegnato in fase di progettazione. Noto anche come valore predefinito di progettazione.|  
    |Sensibile|I valori di parametri sensibili sono crittografati nel catalogo e risultano NULL quando vengono visualizzati con Transact-SQL o con SQL Server Management Studio.|  
    |Obbligatorio|Richiede che un valore diverso dal valore predefinito di progettazione venga specificato prima dell'esecuzione del pacchetto.|  
    |Descrizione|Per manutenzione, la descrizione del parametro. In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], impostare la descrizione del parametro nella finestra Proprietà di Visual Studio quando il parametro viene selezionato nella finestra dei parametri applicabile.|  
  
5.  Salvare il progetto per salvare le modifiche ai parametri. I valori dei parametri sono archiviati nelle configurazioni del file di progetto. Salvare il file di progetto per eseguire il commit al disco delle eventuali modifiche apportate ai valori dei parametri.  
  
    > [!WARNING]  
    >  È possibile modificare direttamente l'elenco oppure usare la finestra **Proprietà** per modificare i valori delle proprietà dei parametri. È possibile eliminare un parametro tramite il pulsante **Elimina (X)**. Usando l'ultimo pulsante della barra degli strumenti per aprire la finestra di dialogo **Gestione dei valori dei parametri**, è possibile specificare un valore per un parametro usato solo quando si esegue il pacchetto in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;SSIS&#41; parametri](integration-services-ssis-package-and-project-parameters.md)  
  
  
