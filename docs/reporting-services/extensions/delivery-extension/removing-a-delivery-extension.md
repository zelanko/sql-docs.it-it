---
title: Rimozione di un'estensione per il recapito | Microsoft Docs
description: Informazioni su come rimuovere un'estensione per il recapito da Reporting Services in modo che il server di report non la elenchi come disponibile e disattivi le sottoscrizioni che la usano.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6f4f23d58836dbadb9393be49dd34425c89a15c3
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529487"
---
# <a name="removing-a-delivery-extension"></a>Rimozione di un'estensione per il recapito
  Per rimuovere un'estensione per il recapito di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], rimuovere semplicemente l'elemento **Extension** per l'estensione dal file di configurazione. Dopo la rimozione delle informazioni di configurazione, l'estensione per il recapito non è più disponibile per il server di report.  
  
 Dopo aver rimosso l'elemento **Extension** corrispondente di un'estensione per il recapito dal file di configurazione, l'estensione non è più registrata nel server di report. Il server di report rimuove la voce dall'elenco di estensioni per il recapito e disattiva qualsiasi sottoscrizione che utilizza tale estensione. Quando un'estensione per il recapito viene rimossa, gli utenti non possono più selezionarla come metodo di notifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
