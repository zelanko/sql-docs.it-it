---
title: Definire un membro predefinito | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
author: minewiskan
ms.author: owend
ms.openlocfilehash: e781e26dc2e45c6637b6868304be08452d31a996
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544823"
---
# <a name="define-a-default-member"></a>Definire un membro predefinito
  Il membro predefinito di una gerarchia dell'attributo viene utilizzato per valutare le espressioni quando una gerarchia dell'attributo non è inclusa in una query. Il membro predefinito viene ignorato ogni volta che una query include una gerarchia dell'attributo o dell'utente contenente l'attributo che dà origine alla gerarchia dell'attributo, poiché viene utilizzato il membro specificato nella query.  
  
 Il membro predefinito per una gerarchia dell'attributo viene impostato specificando un membro dell'attributo come valore della proprietà `DefaultMember` per la gerarchia dell'attributo. È possibile impostare questa proprietà nella scheda Struttura dimensione di Progettazione dimensioni o nello script di calcolo del cubo nella scheda Calcolo di Progettazione cubi in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. È inoltre possibile specificare la proprietà `DefaultMember` per un ruolo di sicurezza (sostituendo il membro predefinito impostato sulla dimensione) nella scheda Dati della dimensione quando viene definita la sicurezza delle dimensioni. Per evitare problemi di risoluzione del nome, definire il membro predefinito nello script MDX del cubo nelle situazioni seguenti: se il cubo fa riferimento a una dimensione del database più di una volta, se la dimensione nel cubo ha un nome diverso da quello nel database o se si desidera avere membri predefiniti diversi in cubi diversi.  
  
 Il membro predefinito di un attributo viene utilizzato per valutare le espressioni se un attributo non è incluso in una query. Il membro predefinito per un attributo viene specificato tramite la proprietà `DefaultMember` nell'attributo. Se in una query è inclusa una gerarchia di una dimensione, verranno ignorati tutti i membri predefiniti degli attributi corrispondenti ai livelli della gerarchia. Se in una query non viene inclusa alcuna gerarchia di una dimensione, i membri predefiniti vengono utilizzati per tutti gli attributi della dimensione.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Risoluzione del membro predefinito quando non viene specificato alcun membro predefinito  
 Se non viene specificato alcun membro predefinito per una gerarchia dell'attributo e tale gerarchia è aggregabile, ovvero la proprietà `IsAggregatable` dell'attributo è impostata su `True`, il membro (All) è sarà il membro predefinito. Se non viene specificato alcun membro predefinito e la gerarchia dell'attributo non è aggregabile, ovvero la proprietà `IsAggregatable` dell'attributo è impostata su `False`, verrà selezionato un membro predefinito dal livello principale della gerarchia dell'attributo.  
  
## <a name="specifying-the-default-member"></a>Impostazione del membro predefinito  
 Ogni attributo di una dimensione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dispone di un membro predefinito, che è possibile specificare usando la `DefaultMember` proprietà per un attributo. Questa impostazione viene utilizzata per valutare espressioni nel caso in cui in una query non venga specificato un attributo. Se in una query viene specificata una gerarchia di una dimensione, i membri predefiniti degli attributi nella gerarchia verranno ignorati. Se una query non specifica una gerarchia in una dimensione, verranno `DefaultMember` applicate le impostazioni per gli attributi della dimensione.  
  
 Se l' `DefaultMember` impostazione per un attributo è vuota e la relativa `IsAggregatable` proprietà è impostata su `True` , il membro predefinito è il membro totale. Se la `IsAggregatable` proprietà è impostata su `False` , il membro predefinito è il primo membro del primo livello visibile.  
  
 L' `DefaultMember` impostazione di un attributo si applica a ogni gerarchia a cui partecipa l'attributo. Non è possibile utilizzare impostazioni diverse per gerarchie diverse in una dimensione. Se, ad esempio, il membro [1998] è il membro predefinito di un attributo [Year], questa impostazione verrà applicata a tutte le gerarchie della dimensione. `DefaultMember`In questo caso, l'impostazione non può essere [1998] in una gerarchia e [1997] in una gerarchia diversa.  
  
 Se si definisce un membro predefinito per un livello particolare di una gerarchia che non viene aggregato in modo naturale, sarà necessario definire membri predefiniti in tutti i livelli al di sopra di tale livello nella gerarchia. Ad esempio, nella gerarchia all-countries-Climate non è possibile definire un membro predefinito per Climate se non si definisce un membro predefinito per i paesi. Se non si rispetta questo requisito, si verificheranno errori durante l'esecuzione delle query.  
  
 Quando i livelli di una gerarchia vengono aggregati in modo naturale, è possibile definire un membro predefinito per qualsiasi attributo della gerarchia senza tenere conto di altri attributi di tale gerarchia. Ad esempio, nella gerarchia Country-Province-City è possibile definire un membro predefinito per City come [City]. [Montreal] senza definire il membro predefinito per state o Country.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare il livello &#40;Totale&#41; per le gerarchie di attributi](database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
