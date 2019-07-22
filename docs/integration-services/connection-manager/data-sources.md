---
title: Origini dati | Microsoft Docs
ms.custom: ''
ms.date: 08/27/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 89b6660f5a989cec23b5a92c09dabb36f891e1c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968112"
---
# <a name="data-sources"></a>Origini dati

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] include un oggetto della modalità progettazione che è possibile usare nei pacchetti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] : l'origine dati.  
  
 Un oggetto di origine dati è un riferimento a una connessione in cui sono inclusi almeno una stringa di connessione e l'identificatore di un'origine dati. Può includere anche metadati aggiuntivi quali una descrizione, un nome, un nome utente e una password.  
  
> **NOTA:** È possibile aggiungere le origini dati solo ai progetti configurati per utilizzare il modello di distribuzione del pacchetto. Se un progetto è configurato per utilizzare il modello di distribuzione del progetto, è possibile utilizzare le gestioni connessioni create a livello di progetto per condividere le connessioni anziché le origini dati.  
>   
>  Per altre informazioni sui modelli di distribuzione, vedere [Distribuzione di progetti e pacchetti](../packages/deploy-integration-services-ssis-projects-and-packages.md). Per altre informazioni sulla conversione di un progetto nel modello di distribuzione del progetto, vedere [Distribuire progetti nel server Integration Services](https://msdn.microsoft.com/library/hh231102.aspx).  
  
 L'utilizzo di origini dei dati nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre i vantaggi seguenti:  
  
-   Poiché le origini dati hanno ambito di progetto, un'origine dati creata in un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è disponibile per tutti i pacchetti del progetto. È inoltre possibile definire un'origine dei dati una sola volta e farvi riferimento da gestioni connessioni in più pacchetti.  
  
-   Le origini dei dati consentono di mantenere la sincronizzazione tra l'oggetto di origine dati e i relativi riferimenti nei pacchetti. Se l'origine dei dati e i pacchetti che vi fanno riferimento risiedono nello stesso progetto, la proprietà relativa alla stringa di connessione dei riferimenti all'origine dei dati verrà automaticamente aggiornata quando l'origine dei dati viene modificata.  
  
## <a name="reference-data-sources"></a>Riferimento a origini dati  
 Per aggiungere un oggetto origine dati a un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , fare clic con il pulsante destro del mouse sulla cartella **Origini dati** in **Esplora soluzioni** , quindi scegliere **Nuova origine dati**. L'elemento verrà aggiunto alla cartella **Origini dati** . Se desidera utilizzare oggetti di origine dati creati in altri progetti, sarà prima necessario aggiungerli al progetto.  
  
 Per utilizzare un origine dei dati in un pacchetto è necessario aggiungere al pacchetto una gestione connessione che fa riferimento all'oggetto di origine dati. La gestione connessione può essere aggiunta prima della compilazione del flusso di controllo e dei flussi di dati del pacchetto oppure in un passaggio della procedura di creazione.  
  
 Un oggetto di origine dati rappresenta una semplice connessione a un'origine dei dati e consente di accedere agli oggetti nell'archivio dati a cui fa riferimento. Un oggetto origine dati che si connette al database di esempio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AdventureWorks, ad esempio, include tutte e 60 le tabelle del database.  
  
 Non esiste alcuna dipendenza tra un'origine dei dati e le gestioni connessioni che vi fanno riferimento. Se un'origine dei dati non fa più parte di un progetto i pacchetti rimangono comunque validi, perché le informazioni relative all'origine dei dati, quali il tipo di connessione e la stringa di connessione, sono incluse nella definizione del pacchetto.  
  
  
