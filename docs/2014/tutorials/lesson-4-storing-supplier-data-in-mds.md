---
title: 'Lezione 4: archiviazione dei dati fornitore in MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 678a7d6ce075e6a1082856aa7962bb3f6eec522d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489713"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>Lezione 4: Archiviazione dei dati fornitore in MDS
  Master Data Services (MDS) è una soluzione SQL Server per la gestione dei dati master. Nella gestione dei dati master vengono descritti gli sforzi fatti da un'organizzazione per individuare e definire elenchi non transazionali di dati.  
  
 I modelli rappresentano il livello più elevato di organizzazione in Master Data Services e consentono di organizzare la struttura dei dati master. Per l'implementazione di MDS si può disporre di uno o più modelli in ognuno dei quali vengono raggruppati dati simili. I dati master rientrano in genere in una delle quattro categorie seguenti: persone, luoghi, cose o concetti. È ad esempio possibile creare un modello Product per contenere dati relativi al prodotto oppure un modello Customer per contenere dati relativi al cliente. Per ulteriori informazioni, vedere [modelli (Master Data Services)](https://msdn.microsoft.com/library/ee633746.aspx) .  
  
 In un modello possono essere incluse una o più entità. Ogni entità dispone di attributi (colonne) e membri (righe). In ogni riga sono contenuti i dati master. In questa lezione viene creato un modello Suppliers con due entità denominate Supplier e State. L'entità Supplier avrà i seguenti attributi: Code, Name, Contact First Name, Contact Last Name, Contact Email Address, Address Line, City, State, Zip e Country. Per ulteriori informazioni sugli attributi in generale, vedere [attributi (Master Data Services)](https://msdn.microsoft.com/library/ee633745.aspx) . Gli attributi Name e Code corrispondono alle colonne SupplierID e Supplier Name nel file di Excel relativo ai fornitori con dati puliti e corrispondenti.  
  
 Un attributo basato su dominio è un attributo i cui valori sono popolati da membri di un'altra entità. Gli attributi basati su dominio non consentono l'immissione di valori di attributo non validi da parte di utenti. È possibile selezionare un valore di attributo solo nell'elenco a discesa popolato da un'altra entità. In questa esercitazione, l'attributo State dell'entità Supplier è un attributo basato su dominio con valori dell'entità State. Il valore dell'attributo State dell'entità Supplier può essere impostato solo su uno dei valori nell'entità State. Per ulteriori informazioni, vedere [attributi basati su dominio](../master-data-services/domain-based-attributes-master-data-services.md) .  
  
 Una gerarchia derivata in MDS deriva dalla relazione tra attributi basati su dominio nel modello. In questa esercitazione viene creata una gerarchia derivata tra l'entità Supplier e l'entità State. Dopo aver creato la gerarchia derivata, verrà visualizzato un elenco di stati nel visualizzatore di Gestione dati master. Quando si fa clic su uno stato nell'elenco, vengono visualizzati i fornitori nello stato in questione nel riquadro destro. Successivamente, verrà creata una gerarchia derivata basata su questa relazione. Per ulteriori informazioni, vedere [gerarchie derivate](../master-data-services/derived-hierarchies-master-data-services.md) .  
  
 È stata compilata una Knowledge Base in DQS che è stata utilizzata per la pulizia e la corrispondenza dei dati fornitore e i risultati sono stati archiviati nel file Cleansed and Matched Supplier Data.xls. In questa lezione i dati puliti e corrispondenti vengono caricati in MDS. In DQS sono contenute solo le informazioni sui dati (metadati), mentre i dati stessi (set master) vengono archiviati da MDS. Ad esempio, è possibile che in DQS siano disponibili informazioni su diversi fornitori, ma in MDS vengono gestiti solo i fornitori utilizzati da una società.  
  
 In questa lezione vengono effettuate le attività seguenti:  
  
1.  Creare il modello **Suppliers** in **MDS** tramite l' **applicazione Web gestione dati master**.  
  
2.  Aprire **cleaned and Matched Supplier Data. xls** in Excel e usare il **componente aggiuntivo MDS per Excel** per creare un'entità denominata **Supplier** e caricare i dati in MDS.  
  
3.  Verificare che i dati vengano creati in MDS usando il **Gestione dati master**.  
  
4.  Creare un'entità denominata **state** e aggiornare l'attributo **state** dell'entità **Supplier** in modo che sia un attributo basato su dominio a seconda dell'entità **state** . Questa operazione viene eseguita usando il **componente aggiuntivo MDS per Excel**.  
  
5.  Verificare che l'attributo basato su dominio venga creato utilizzando **Gestione dati master** e aggiornare i valori per l'attributo **Name** dell'entità **state** .  
  
6.  Visualizzare gli aggiornamenti effettuati utilizzando **Gestione dati master** in **Excel**.  
  
7.  Caricare i valori dall'entità **state** in **Excel** e aggiungere un valore e verificare l'aggiunta usando **Gestione dati master**.  
  
8.  Creare e utilizzare una gerarchia derivata utilizzando la relazione tra attributi basati su dominio tra l'entità **Supplier** e l'entità **state** (l'attributo State dell'entità Supplier è di tipo entità State) utilizzando **Gestione dati master**.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 1: Creazione del modello Supplier tramite Gestione dati master](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
