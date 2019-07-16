---
title: Visualizzare attributi in Progettazione dimensioni | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c8e0535a1df60b4a4e1550e2b49a02e7a60e2c04
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68179414"
---
# <a name="attribute-properties---view-attributes-in-dimension-designer"></a>Proprietà degli attributi - Visualizzare attributi in Progettazione dimensioni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Gli attributi vengono creati in oggetti dimensione. È possibile visualizzare e configurare gli attributi tramite Progettazione dimensioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Nel riquadro **Attributi** della scheda **Struttura dimensione** di Progettazione dimensioni sono elencati gli attributi inclusi in una dimensione. Utilizzare questo riquadro per aggiungere, rimuovere o configurare attributi. È inoltre possibile selezionare gli attributi da utilizzare come livello in una nuova gerarchia o da aggiungere come livello in una gerarchia esistente.  
  
 Per visualizzare gli attributi in una dimensione, aprire Progettazione dimensioni per tale dimensione. Nel riquadro **Attributi** della scheda **Struttura dimensione**  della finestra di progettazione vengono visualizzati gli attributi inclusi nella dimensione. È possibile impostare una visualizzazione elenco, albero e griglia scegliendo **Mostra attributi in** dal menu **Dimensione** di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , quindi facendo clic su uno dei comandi seguenti:  
  
1.  Mostra attributi in **Elenco**. Consente di visualizzare gli attributi in formato di elenco. Fare clic con il pulsante destro del mouse su un attributo per eliminarlo dall'elenco, rinominarlo oppure modificarne l'utilizzo. Utilizzare questa visualizzazione per compilare gerarchie. Le informazioni sugli attributi e le proprietà membro non sono visibili.  
  
2.  Mostra attributi in **Albero**. Consente di visualizzare gli attributi in formato di albero, con la dimensione come nodo di livello principale dell'albero. Espandere un attributo per visualizzarne le relazioni tra attributi o per creare una nuova relazione tra attributi, eseguendo le operazioni seguenti:  
  
    -   Fare clic sulla dimensione, su un attributo o su una proprietà membro per visualizzarne le proprietà nella finestra **Proprietà** .  
  
    -   Fare clic con il pulsante destro del mouse su una proprietà membro o su un attributo per eliminarlo dall'elenco, rinominarlo oppure modificarne l'utilizzo.  
  
     Utilizzare questa visualizzazione per visualizzare e creare proprietà membro. Può inoltre essere utilizzata per compilare gerarchie.  
  
3.  Mostra attributi in **Griglia**. Consente di visualizzare gli attributi in formato di griglia. Nella griglia vengono visualizzate le colonne seguenti:  
  
    -   In**Nome** viene visualizzato il valore della proprietà **Nome** . Digitare un diverso nome per modificare l'impostazione.  
  
    -   **Utilizzo** specifica che si tratta di un attributo Regular, Key, Parent o AccountType. Fare clic su un valore in questa colonna per selezionare un'impostazione diversa.  
  
    -   **Tipo** specifica la categoria di Business Intelligence per l'attributo. Fare clic sulla cella per selezionare un'impostazione diversa.  
  
    -   In**Colonna chiave** viene visualizzato il tipo di dati OLE DB per la proprietà **KeyColumn** dell'attributo. Questa colonna non può essere modificata.  
  
    -   In**Colonna nome** viene indicato se l'impostazione della proprietà **NameColumn** dell'attributo corrisponde alla colonna impostata per la proprietà **KeyColumn** . Questa colonna non può essere modificata.  
  
     Fare clic su qualsiasi riga della griglia per visualizzare le proprietà dell'attributo.  
  
     Utilizzare questa visualizzazione per creare e configurare attributi.  
  
 In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]gli attributi vengono contrassegnati in base al relativo utilizzo tramite le icone illustrate nella tabella seguente.  
  
|Icona|Utilizzo dell'attributo|  
|----------|---------------------|  
|![Icona di attributo](../../analysis-services/multidimensional-models/media/as-icon-attribute.gif "icona di attributo")|Regular o AccountType|  
|![Icona di attributo chiave](../../analysis-services/multidimensional-models/media/as-icon-key-attribute.gif "icona di attributo chiave")|Chiave|  
|![Icona di attributo padre](../../analysis-services/multidimensional-models/media/as-icon-parent-attribute.gif "icona di attributo padre")|Parent|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributi delle dimensioni](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
