---
title: Definire un membro predefinito | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 10b5776a4d4be5f31522740c28a6142a7e213576
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516727"
---
# <a name="attribute-properties---define-a-default-member"></a>Proprietà degli attributi - Definire un membro predefinito
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Il membro predefinito di una gerarchia dell'attributo viene utilizzato per valutare le espressioni quando una gerarchia dell'attributo non è inclusa in una query. Il membro predefinito viene ignorato ogni volta che una query include una gerarchia dell'attributo o dell'utente contenente l'attributo che dà origine alla gerarchia dell'attributo, poiché viene utilizzato il membro specificato nella query.  
  
 Il membro predefinito per una gerarchia dell'attributo viene impostato specificando un membro dell'attributo come valore della proprietà **DefaultMember** per la gerarchia dell'attributo. È possibile impostare questa proprietà nella scheda Struttura dimensione di Progettazione dimensioni o nello script di calcolo del cubo nella scheda Calcolo di Progettazione cubi in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. È inoltre possibile specificare la proprietà **DefaultMember** per un ruolo di sicurezza (sostituendo il membro predefinito impostato sulla dimensione) nella scheda Dati della dimensione quando viene definita la sicurezza delle dimensioni. Per evitare problemi di risoluzione del nome, definire il membro predefinito nello script MDX del cubo nelle situazioni seguenti: se il cubo fa riferimento a una dimensione del database più di una volta, se la dimensione nel cubo ha un nome diverso da quello nel database o se si desidera avere membri predefiniti diversi in cubi diversi.  
  
 Il membro predefinito di un attributo viene utilizzato per valutare le espressioni se un attributo non è incluso in una query. Il membro predefinito per un attributo viene specificato tramite la proprietà **DefaultMember** nell'attributo. Se in una query è inclusa una gerarchia di una dimensione, verranno ignorati tutti i membri predefiniti degli attributi corrispondenti ai livelli della gerarchia. Se in una query non viene inclusa alcuna gerarchia di una dimensione, i membri predefiniti vengono utilizzati per tutti gli attributi della dimensione.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Risoluzione del membro predefinito quando non viene specificato alcun membro predefinito  
 Se non viene specificato alcun membro predefinito per una gerarchia dell'attributo e tale gerarchia è aggregabile, ovvero la proprietà **IsAggregatable** dell'attributo è impostata su **True**, il membro (Totale) sarà il membro predefinito. Se non viene specificato alcun membro predefinito e la gerarchia dell'attributo non è aggregabile, ovvero la proprietà **IsAggregatable** dell'attributo è impostata su **False**, verrà selezionato un membro predefinito dal livello principale della gerarchia dell'attributo.  
  
## <a name="specifying-the-default-member"></a>Impostazione del membro predefinito  
 Ogni attributo di una dimensione in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dispone di un membro predefinito, che è possibile specificare tramite la proprietà **DefaultMember** dell'attributo. Questa impostazione viene utilizzata per valutare espressioni nel caso in cui in una query non venga specificato un attributo. Se in una query viene specificata una gerarchia di una dimensione, i membri predefiniti degli attributi nella gerarchia verranno ignorati. Se in una query non viene specificata una gerarchia di una dimensione, verranno applicate le impostazioni della proprietà **DefaultMember** degli attributi della dimensione.  
  
 Se l'impostazione della proprietà **DefaultMember** di un attributo è vuota e la proprietà **IsAggregatable** è impostata su **True**, il membro predefinito sarà il membro Totale. Se la proprietà **IsAggregatable** è impostata su **False**, il membro predefinito sarà il primo membro del primo livello visibile.  
  
 L'impostazione della proprietà **DefaultMember** di un attributo viene applicata a tutte le gerarchie in cui è presente l'attributo. Non è possibile utilizzare impostazioni diverse per gerarchie diverse in una dimensione. Se, ad esempio, il membro [1998] è il membro predefinito di un attributo [Year], questa impostazione verrà applicata a tutte le gerarchie della dimensione. L'impostazione della proprietà **DefaultMember** in questo caso non può essere [1998] in una gerarchia e [1997] in un'altra.  
  
 Se si definisce un membro predefinito per un livello particolare di una gerarchia che non viene aggregato in modo naturale, sarà necessario definire membri predefiniti in tutti i livelli al di sopra di tale livello nella gerarchia. Nella gerarchia All-paesi-climatici, ad esempio, è possibile definire un membro predefinito per Climate se non si definisce un membro predefinito per Countries. Se non si rispetta questo requisito, si verificheranno errori durante l'esecuzione delle query.  
  
 Quando i livelli di una gerarchia vengono aggregati in modo naturale, è possibile definire un membro predefinito per qualsiasi attributo della gerarchia senza tenere conto di altri attributi di tale gerarchia. Ad esempio, nella gerarchia di stato-provincia-città, è possibile definire un membro predefinito per City quale [City]. [Montreal] senza definire il membro predefinito per State o Country.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare il livello &#40;Totale&#41; per le gerarchie di attributi](../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
