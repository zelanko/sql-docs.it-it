---
title: Finestra di dialogo Aggiungi riferimento (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.addreference.f1
- sql12.asvs.bidevstudio.assembly.addassembly.f1
helpviewer_keywords:
- Add Reference dialog box
ms.assetid: 457958c4-6baa-474d-99a0-34c195ceba09
author: minewiskan
ms.author: owend
ms.openlocfilehash: e35eeae8f48fe25e8f0c79455271d83ca1c609f8
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528282"
---
# <a name="add-reference-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Aggiungi riferimento (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Aggiungi riferimento** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per aggiungere a un progetto di sviluppo un riferimento a un assembly [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework o a un altro progetto. Per visualizzare la finestra di dialogo **Aggiungi riferimento** fare clic con il pulsante destro del mouse sulla cartella **Assembly** di un progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in **Esplora soluzioni** e scegliere **Nuovo riferimento ad assembly** dal menu di scelta rapida.  
  
## <a name="options"></a>Opzioni  
  
|Termine|Definizione|  
|----------|----------------|  
|**.NET**|Selezionare questa scheda per aggiungere un riferimento a un componente registrato. Questa scheda consente di visualizzare una griglia contenente un elenco di componenti .NET Framework registrati. Selezionare uno o più elementi nella griglia e quindi fare clic su **Aggiungi** per aggiungere i componenti .NET selezionati a **Progetti e componenti selezionati**. La griglia include le colonne seguenti:<br /><br /> **Nome del componente**: nome completo, o descrittivo, del componente. Selezionare il titolo della colonna per impostare l'ordinamento in base al nome dei componenti.<br /><br /> **Version (versione**): il numero di versione del componente specificato. Selezionare il titolo della colonna per impostare l'ordinamento in base alla versione.<br /><br /> **Runtime**: versione della .NET Framework su cui è basato il componente. Selezionare il titolo della colonna per impostare l'ordinamento in base alla versione run-time.<br /><br /> **Path**: nome del file del componente e percorso in cui si trova. Selezionare il titolo della colonna per impostare l'ordinamento in base al percorso.|  
|**Sfoglia**|Fare clic per cercare nel file system un assembly non incluso nelle schede **.NET** o **Recente** . Questa scheda visualizza le opzioni seguenti:<br /><br /> **Cerca in**: selezionare una cartella da questo elenco a discesa. Selezionando una cartella in questo elenco viene visualizzato il contenuto della cartella nel riquadro principale.<br /><br /> **Vai all'ultima cartella visitata**: **restituisce il** percorso precedente.<br /><br /> **Un livello**superiore: individua la cartella successiva più alta nella gerarchia.<br /><br /> **Crea nuova cartella**: selezionare questa opzione per creare una nuova cartella figlio nella cartella selezionata in **Cerca in**.<br /><br /> **Menu Visualizza**: selezionare questa voce per modificare la visualizzazione dei contenuti nel riquadro principale.  Per altre informazioni sulle opzioni in **Visualizza menu**, vedere l'argomento la panoramica sulla visualizzazione di file e cartelle nella documentazione di [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Sono disponibili le opzioni seguenti:<br />Anteprime<br />Riquadri<br />Icone<br />Elenco<br />Dettagli<br /><br /> **Riquadro principale**: consente di visualizzare il contenuto della cartella selezionata in **Cerca in**. Selezionare uno o più elementi e quindi fare clic su **Aggiungi** per aggiungere i file selezionati ai **prodotti e ai componenti selezionati**. Per ulteriori informazioni sulle opzioni e sul menu di scelta rapida del riquadro principale, vedere l'argomento relativo alla panoramica sulla visualizzazione di file e cartelle nella documentazione di Windows.<br /><br /> **Nome file**: usare questa opzione per filtrare i file e le cartelle visualizzati. Digitare un nome completo o parziale di file da utilizzare come filtro. È possibile utilizzare l'asterisco (\*) come carattere jolly. Per selezionare più file digitare più nomi di file, con ogni nome di file racchiuso tra virgolette (") e delimitato da uno spazio. È inoltre possibile selezionare file precedentemente esaminati selezionando un nome di file nell'elenco a discesa. Suggerimento: è possibile individuare i server Web e i computer di rete immettendo un URL o un percorso di rete in **nome file**. Ad esempio, se si digita "http://mywebsite" vengono visualizzati i file disponibili nel percorso Web "mywebsite", mentre se si digita "\\" vengono visualizzati i file disponibili nel percorso "myshare" del server "myserver".<br /><br /> **File di tipo**: usare questa opzione per filtrare il contenuto della cartella o della directory selezionata in **Cerca in** per un particolare tipo di file.|  
|**Origini**|Consente di visualizzare un elenco di riferimenti a componenti aggiunti recentemente ai progetti in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Selezionare uno o più elementi nella griglia e fare clic su **Aggiungi** per aggiungere gli assembly .NET Framework selezionati a **Progetti e componenti selezionati**. La griglia include le colonne seguenti:<br /><br /> **Nome del componente**: nome completo, o descrittivo, del componente. Selezionare il titolo della colonna per impostare l'ordinamento in base al nome dei componenti.<br /><br /> **Version (versione**): il numero di versione del componente specificato. Selezionare il titolo della colonna per impostare l'ordinamento in base alla versione.<br /><br /> **Runtime**: versione della .NET Framework su cui è basato il componente. Selezionare il titolo della colonna per impostare l'ordinamento in base alla versione run-time.<br /><br /> **Path**: nome del file del componente e percorso in cui si trova. Selezionare il titolo della colonna per impostare l'ordinamento in base al percorso.|  
|**Aggiungere**|Fare clic su questo pulsante per aggiungere a **Progetti e componenti selezionati**un componente selezionato nelle schede **.NET**, **Sfoglia** o **Recente**.|  
|**Rimuovi**|Fare clic per rimuovere un componente selezionato da **Progetti e componenti selezionati**.|  
|**Recente**|Consente di visualizzare un elenco di riferimenti a componenti da aggiungere al progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Selezionare uno o più elementi nella griglia e quindi fare clic su **Rimuovi** per rimuovere i componenti selezionati dalla griglia. La griglia include le colonne seguenti:<br /><br /> **Nome del componente**: nome completo, o descrittivo, del componente. Selezionare il titolo della colonna per impostare l'ordinamento in base al nome dei componenti.<br /><br /> **Version (versione**): il numero di versione del componente specificato. Selezionare il titolo della colonna per impostare l'ordinamento in base alla versione.<br /><br /> **Runtime**: versione della .NET Framework su cui è basato il componente. Selezionare il titolo della colonna per impostare l'ordinamento in base alla versione run-time.<br /><br /> **Path**: nome del file del componente e percorso in cui si trova. Selezionare il titolo della colonna per impostare l'ordinamento in base al percorso.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gestione di assembly di modelli multidimensionali](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
