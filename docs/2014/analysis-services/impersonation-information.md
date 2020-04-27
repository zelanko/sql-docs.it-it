---
title: Informazioni di rappresentazione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 42319d60-ccd0-46b8-af0b-f0968c390d8a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9314494230469cca5e8db9926ddf71cb790b96ec
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080649"
---
# <a name="impersonation-information"></a>Impostazioni di rappresentazione
  Usare la pagina **Impostazioni di rappresentazione** per specificare le credenziali usate da Analysis Services per la connessione all'origine dati.  
  
## <a name="options"></a>Opzioni  
 **Usa nome utente e password specifici di Windows**  
 Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usi le credenziali di sicurezza di un account utente di Windows specificato. Le credenziali specificate verranno usate per l'elaborazione, le query ROLAP, le associazioni out-of-line, i cubi locali, i modelli di data mining, le partizioni remote, gli oggetti collegati e la sincronizzazione dalla destinazione all’origine. Per le istruzioni DMX (Data Mining Extensions) OPENQUERY, invece, questa opzione viene ignorata e verranno usate le credenziali dell'utente corrente.  
  
 **Nome utente**  
 Digitare il dominio e il nome dell'account utente che verranno usati dall'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selezionato. Utilizzare il seguente formato:  
  
 Nome di **\\** dominio>* \<nome account utente>* * \<*  
  
 Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .  
  
 **Password**  
 Digitare la password dell'account utente che verrà utilizzata dall'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selezionato.  
  
 Questa opzione è abilitata solo se si seleziona l'opzione **Usa nome utente e password specifici** .  
  
 **Usa account del servizio**  
 Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzi le credenziali di sicurezza associate al servizio di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che gestisce l'oggetto. Le credenziali dell'account del servizio verranno utilizzate per l'elaborazione, le query ROLAP, le partizioni remote, gli oggetti collegati e la sincronizzazione da un'origine a una destinazione. Per le istruzioni DMX (Data Mining Extensions) OPENQUERY, i cubi locali, i modelli di data mining, verranno utilizzate invece le credenziali dell'utente corrente. Questa opzione non è supportata per le associazioni out-of-line.  
  
 **Usa credenziali dell'utente corrente**  
 Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzi le credenziali di sicurezza dell'utente corrente per le associazioni out-of-line, le istruzioni DMX OPENQUERY, i cubi locali e i modelli di data mining. Questa opzione non è supportata per l'elaborazione, le query ROLAP, le partizioni remote, gli oggetti collegati e la sincronizzazione da un'origine a una destinazione.  
  
 **Ereditare**  
 Selezionare questa opzione per utilizzare il comportamento della rappresentazione, definito al livello del database impostato dall'amministratore del server utilizzando la proprietà del database `DataSourceImpersonation`.  
  
## <a name="see-also"></a>Vedi anche  
 [Origini dati nei modelli multidimensionali](multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Origini dati supportate &#40;SSAS multidimensionale&#41;](multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
