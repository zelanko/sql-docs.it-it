---
title: 'Passaggio 3: Modifica del valore di configurazione proprietà Directory | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba2a091f-361c-4331-afe2-53b465164c36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 011cd07c0f28f884f460d78d5f2f88631bfe2fd9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807503"
---
# <a name="step-3-modifying-the-directory-property-configuration-value"></a>Passaggio 3: Modifica del valore di configurazione della proprietà Directory
  In questa attività verrà modificata l'impostazione di configurazione archiviata nel file SSISTutorial.dtsConfig relativa alla proprietà Value della variabile a livello di pacchetto `User::varFolderName`. Tale variabile aggiorna la proprietà Directory del contenitore Ciclo Foreach. Il valore modificato punterà il `New Sample Data` cartella creata nell'attività precedente. Dopo la modifica dell'impostazione di configurazione e l'esecuzione del pacchetto, la proprietà Directory viene aggiornata dalla variabile, usando il valore popolato dal file di configurazione anziché il valore della directory configurato in origine nel pacchetto.  
  
### <a name="to-modify-the-configuration-setting-of-the-directory-property"></a>Per modificare l'impostazione di configurazione della proprietà Directory  
  
1.  In Blocco note o in un altro editor di testo, individuare ed aprire il file di configurazione SSISTutorial.dtsConfig creato nell'attività precedente utilizzando Configurazione guidata pacchetto.  
  
2.  Modificare il valore del **ConfiguredValue** in base al percorso di elemento di `New Sample Data` cartella creata nell'attività precedente. Non racchiudere il percorso tra virgolette. Se il `New Sample Data` cartella è a livello di radice dell'unità (ad esempio, c\\), il codice XML aggiornato dovrebbe essere simile all'esempio seguente:  
  
     `<?xml version="1.0"?><DTSConfiguration><DTSConfigurationHeading><DTSConfigurationFileInfo GeneratedBy="DOMAIN\UserName" GeneratedFromPackageName="Lesson 5" GeneratedFromPackageID="{F4475E73-59E3-478F-8EB2-B10AFA61D3FA}" GeneratedDate="6/10/2012 8:16:50 AM"/></DTSConfigurationHeading><Configuration ConfiguredType="Property" Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"><ConfiguredValue></ConfiguredValue></Configuration></DTSConfiguration>`  
  
     Le informazioni dell'intestazione, `GeneratedBy`, `GeneratedFromPackageID`, e **GeneratedDate** sarà diverso nel file, naturalmente. L'elemento da esaminare è `Configuration`. La proprietà `Value` della variabile `User::varFolderName` contiene ora C:\New Sample Data.  
  
3.  Salvare le modifiche e chiudere l'editor di testo.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 4: Test del pacchetto dell'esercitazione della lezione 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
  
