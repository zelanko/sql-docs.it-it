---
title: Proprietà Detail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27d9d7ab4cd29c6eb0ea7ae1c6bddbe8c1b7ef06
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60158817"
---
# <a name="detail-property"></a>Proprietà Detail
  La proprietà **Detail** della classe [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] **SoapException** ha la struttura XML seguente:  
  
## <a name="elements"></a>Elementi  
 **Detail**  
 Elemento di livello principale che contiene tutti gli altri elementi relativi ai dettagli dell'errore.  
  
 **ErrorCode**  
 Codice di errore specifico di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 **HttpStatus**  
 Codice di stato HTTP.  
  
 **Message**  
 Messaggio di errore e codice di errore assegnati dal server di report.  
  
 **HelpLink**  
 URL di collegamento alla Guida che rimanda a un sito Web in cui è possibile trovare ulteriori informazioni sull'errore. Per altre informazioni, vedere [Elemento HelpLink](helplink-element.md).  
  
 **LinkID**  
 ID assegnato al collegamento.  
  
 **ProductName**  
 Nome del prodotto. Il valore predefinito è **Microsoft SQL Server Reporting Services**.  
  
 **ProductVersion**  
 Versione di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. La lunghezza massima è di 15 caratteri. Il formato del numero di versione deve essere come segue: 8.00.0xxx.00.  
  
 **ProductLocaleId**  
 ID delle impostazioni locali o della lingua della DLL INTL dell'applicazione (ad esempio, 0x41A).  
  
 **OperatingSystem**  
 Sistema operativo in cui è installato [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. I valori validi includono **0** per indicare una versione indipendente dal sistema operativo, **1** per [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)] e **16** per Windows XP.  
  
 **CountryLocaleId**  
 ID delle impostazioni locali o della lingua del sistema operativo. Il valore della versione francese di Windows è ad esempio 0x040c.  
  
 **MoreInformation**  
 Stringa XML contenente eccezioni nidificate che si sono verificate durante l'esecuzione del metodo.  
  
 **Origine**  
 Elemento figlio di **MoreInformation**. Indica l'origine dell'errore.  
  
 **Message**  
 Elemento figlio di **MoreInformation**. Indica il messaggio di errore di un'eccezione nidificata. Questo elemento include gli attributi XML per **ErrorCode** e **HelpLink**.  
  
 **Avvisi**  
 Stringa XML contenente gli avvisi restituiti dall'elaborazione del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla gestione delle eccezioni in Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException di Reporting Services](reporting-services-soapexception-class.md)   
 [Uso della proprietà Detail per la gestione di errori specifici](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
