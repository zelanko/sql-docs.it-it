---
title: 'Passaggio 3: Modificare il valore di configurazione della proprietà Directory | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2b685268f1a4b76adf1d8947dde53c251190ee3d
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58274826"
---
# <a name="lesson-5-3-modify-the-directory-property-configuration-value"></a>Lezione 5-3: Modificare il valore di configurazione della proprietà Directory

In questa attività viene modificata l'impostazione di configurazione archiviata nel file **SSISTutorial.dtsConfig** relativa alla proprietà **Value** della variabile a livello di pacchetto `User::varFolderName`. La variabile aggiorna la proprietà **Directory** del contenitore Ciclo Foreach. Il valore modificato punta alla cartella **New Sample Data** creata nell'attività precedente. Dopo avere modificato l'impostazione di configurazione ed eseguito il pacchetto, la proprietà **Directory** viene aggiornata rispetto alla variabile nel file di configurazione. In precedenza il valore della proprietà **Directory** faceva parte del pacchetto.  
  
## <a name="modify-the-configuration-setting-of-the-directory-property"></a>Modificare l'impostazione di configurazione della proprietà Directory  
  
1.  In Blocco note, o un altro editor di testo, individuare e aprire il file di configurazione **SSISTutorial.dtsConfig** creato nell'attività precedente usando Configurazione guidata pacchetto.  
  
2.  Modificare il valore dell'elemento **ConfiguredValue** in modo che corrisponda al percorso della cartella **New Sample Data** creata nell'attività precedente. Non racchiudere il percorso tra virgolette. Se la cartella **New Sample Data** si trova al livello radice dell'unità (ad esempio, **C:\\**), il codice XML aggiornato deve essere simile a quello dell'esempio seguente:  
  
    ```
    <?xml version="1.0"?>
    <DTSConfiguration>
      <DTSConfigurationHeading>
        <DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFEE1D3FA}" GeneratedDate="6/10/2018 8:16:50 AM"/>
      </DTSConfigurationHeading>
      <Configuration ConfiguredType="Property" 
          Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String">
        <ConfiguredValue>C:\New Sample Data</ConfiguredValue>
      </Configuration>
    </DTSConfiguration>  
    ```

    Le informazioni di intestazione **GeneratedBy**, **GeneratedFromPackageID** e **GeneratedDate** risultano diverse nel file dell'utente. L'elemento da esaminare è **Configuration** . La proprietà **Value** della variabile, `User::varFolderName`, contiene ora **C:\New Sample Data**.  
  
3.  Salvare le modifiche e chiudere l'editor di testo.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo  
[Passaggio 4: Testare il pacchetto della lezione 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
  
