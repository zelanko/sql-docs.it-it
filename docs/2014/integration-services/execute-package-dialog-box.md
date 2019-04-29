---
title: Execute Package Dialog Box | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageexecute.f1
- sql12.ssis.ssms.executepackage.f1
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f019f2a2e3df3cd32ff7e699022f83f5fc84f0eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898969"
---
# <a name="execute-package-dialog-box"></a>Execute Package Dialog Box
  Usare la finestra di dialogo **Esegui pacchetto** per eseguire un pacchetto archiviato nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 È possibile che in un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] siano contenuti i parametri con i valori archiviati nelle variabili di ambiente. Prima di eseguire tale pacchetto, è necessario specificare l'ambiente che sarà utilizzato per fornire i valori della variabile di ambiente. Un progetto può contenere più ambienti, ma solo un ambiente può essere utilizzato per l'associazione di valori della variabile di ambiente al momento dell'esecuzione. Se nel pacchetto non viene utilizzata alcuna variabile di ambiente, non sarà necessario alcun ambiente.  
  
 Per saperne di più  
  
-   [Aprire la finestra di dialogo Esegui pacchetto](#open_dialog)  
  
-   [Impostare le opzioni nella pagina Generale](#general)  
  
-   [Impostare le opzioni nella scheda Parametri](#parameters)  
  
-   [Impostare le opzioni nella scheda Gestioni connessioni](#connection)  
  
-   [Impostare le opzioni nella scheda Avanzate](#advanced)  
  
-   [Creazione di script per le opzioni contenute nella finestra di dialogo Esegui pacchetto](#script)  
  
##  <a name="open_dialog"></a> Aprire la finestra di dialogo Esegui pacchetto  
  
1.  In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] in cui è ospitato il database SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Espandere la cartella contenente il pacchetto che si desidera eseguire.  
  
5.  Fare clic con il pulsante destro del mouse sul pacchetto, quindi scegliere **Esegui**.  
  
##  <a name="general"></a> Impostare le opzioni nella pagina Generale  
 Selezionare **Ambiente** per specificare l'ambiente che viene applicato quando si esegue il pacchetto.  
  
##  <a name="parameters"></a> Impostare le opzioni nella scheda Parametri  
 Usare la scheda **Parametri** per modificare i valori dei parametri usati quando si esegue il pacchetto.  
  
##  <a name="connection"></a> Impostare le opzioni nella scheda Gestioni connessioni  
 Utilizzare la scheda Gestione connessioni per impostare le proprietà della gestione connessione del pacchetto.  
  
##  <a name="advanced"></a> Impostare le opzioni nella scheda Avanzate  
 Utilizzare la scheda Avanzate per gestire le proprietà e le altre impostazioni del pacchetto.  
  
 **Aggiungi**, **Modifica**, **Rimuovi**  
 Selezionare queste opzioni per aggiungere, modificare o rimuovere una proprietà.  
  
 **Livello di registrazione**  
 Consente di selezionare il livello di registrazione per l'esecuzione del pacchetto. Per altre informazioni, vedere [catalog.start_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database).  
  
 **Dump su errori**  
 Specificare se creare un file di dump quando si verifica un errore durante l'esecuzione del pacchetto. Per altre informazioni, vedere [Generazione di file di dump per l'esecuzione del pacchetto](troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **Runtime a 32 bit**  
 Specificare che il pacchetto verrà eseguito in un sistema a 32 bit.  
  
##  <a name="script"></a> Creazione di script per le opzioni contenute nella finestra di dialogo Esegui pacchetto  
 Mentre si è nella finestra di dialogo **Esegui pacchetto** , è inoltre possibile usare il pulsante **Script** nella barra degli strumenti per scrivere automaticamente codice [!INCLUDE[tsql](../includes/tsql-md.md)] . Lo script generato chiama le stored procedure [catalog.start_execution &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) con le stesse opzioni selezionate nella finestra di dialogo **Esegui pacchetto**. Lo script verrà visualizzato in una nuova finestra dello script di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
  
