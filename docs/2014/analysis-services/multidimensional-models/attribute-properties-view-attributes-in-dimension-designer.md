---
title: Visualizzazione degli attributi in Progettazione dimensioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- displaying attributes
- attributes [Analysis Services], viewing
- viewing attributes
ms.assetid: 855bef07-b72d-4ce3-bf02-de77abeee71a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec86d5e7a910b7fb17397b1601fcc912b46c4d7f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077126"
---
# <a name="view-attributes-in-dimension-designer"></a>Visualizzare attributi in Progettazione dimensioni
  Gli attributi vengono creati in oggetti dimensione. È possibile visualizzare e configurare gli attributi tramite Progettazione dimensioni in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Nel riquadro **Attributi** della scheda **Struttura dimensione** di Progettazione dimensioni sono elencati gli attributi inclusi in una dimensione. Utilizzare questo riquadro per aggiungere, rimuovere o configurare attributi. È inoltre possibile selezionare gli attributi da utilizzare come livello in una nuova gerarchia o da aggiungere come livello in una gerarchia esistente.  
  
 Per visualizzare gli attributi in una dimensione, aprire Progettazione dimensioni per tale dimensione. Nel riquadro **Attributi** della scheda **Struttura dimensione**  della finestra di progettazione vengono visualizzati gli attributi inclusi nella dimensione. È possibile spostarsi tra un elenco, un albero o una visualizzazione griglia scegliendo **Mostra attributi in** dal menu **dimensione** di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e quindi facendo clic su uno dei comandi mostrati nella tabella seguente.  
  
|Mostra attributi in|Descrizione|  
|------------------------|-----------------|  
|**Elenco**|Consente di visualizzare gli attributi in formato di elenco.<br /><br /> Fare clic con il pulsante destro del mouse su un attributo per eliminarlo dall'elenco, rinominarlo oppure modificarne l'utilizzo.<br /><br /> Utilizzare questa visualizzazione per compilare gerarchie. Le informazioni sugli attributi e le proprietà membro non sono visibili.|  
|**Albero**|Consente di visualizzare gli attributi in formato di albero, con la dimensione come nodo di livello principale dell'albero. Utilizzare questa visualizzazione per visualizzare e creare proprietà membro. Può inoltre essere utilizzata per compilare gerarchie. Espandere un attributo per visualizzarne le relazioni tra attributi o per creare una nuova relazione tra attributi, eseguendo le operazioni seguenti:<br /><br /> Fare clic sulla dimensione, su un attributo o su una proprietà membro per visualizzarne le proprietà nella finestra **Proprietà** .<br /><br /> Fare clic con il pulsante destro del mouse su una proprietà membro o su un attributo per eliminarlo dall'elenco, rinominarlo oppure modificarne l'utilizzo.|  
|**Griglia**|Consente di visualizzare gli attributi in formato di griglia. Fare clic su qualsiasi riga della griglia per visualizzare le proprietà dell'attributo.  Utilizzare questa visualizzazione per creare e configurare attributi. Nella griglia vengono visualizzate le colonne seguenti:<br /><br /> **Nome**: Mostra il valore della proprietà **Name** . Digitare un diverso nome per modificare l'impostazione.<br /><br /> **Usage**: specifica se si tratta di un attributo Regular, Key, Parent o AccountType. Fare clic su un valore in questa colonna per selezionare un'impostazione diversa.<br /><br /> **Tipo**: specifica la categoria di Business Intelligence per l'attributo. Fare clic sulla cella per selezionare un'impostazione diversa.<br /><br /> **Chiave Column**: Mostra il tipo di dati OLE DB per la proprietà chiave **Column** sull'attributo. Questa colonna non può essere modificata.<br /><br /> **Nome colonna**: indica se l'impostazione della proprietà **NameColumn** nell'attributo è la stessa colonna dell'impostazione per la proprietà della **colonna** . Questa colonna non può essere modificata.|  
  
 In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]gli attributi vengono contrassegnati in base al relativo utilizzo tramite le icone illustrate nella tabella seguente.  
  
|Icona|Utilizzo dell'attributo|  
|----------|---------------------|  
|![Icona di attributo](../media/as-icon-attribute.gif "Icona di attributo")|Regular o AccountType|  
|![Icona di attributo chiave](../media/as-icon-key-attribute.gif "Icona di attributo chiave")|Chiave|  
|![Icona di attributo padre](../media/as-icon-parent-attribute.gif "Icona di attributo padre")|Parent|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributo delle dimensioni](dimension-attribute-properties-reference.md)  
  
  
