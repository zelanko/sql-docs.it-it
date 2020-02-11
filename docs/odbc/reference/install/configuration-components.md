---
title: Componenti di configurazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 248a9e31b176444ad51cb3a62c7c5f12f1b7bde3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068582"
---
# <a name="configuration-components"></a>Componenti di configurazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare solo in modo esplicito ODBC nelle versioni precedenti di Windows.  
  
 Le origini dati vengono configurate tramite la DLL del programma di installazione, che a sua volta chiama le DLL di installazione del driver e le DLL di installazione del convertitore. La DLL del programma di installazione viene richiamata direttamente dal pannello di controllo o caricata e chiamata da un altro programma, noto come *programma di amministrazione*. Nella figura seguente viene illustrata la relazione tra i componenti di configurazione di.  
  
 ![Relazione tra componenti di configurazione](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Per ulteriori informazioni su questi componenti, vedere gli argomenti seguenti alla fine di questa sezione.  
  
-   [Programma di installazione](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL di installazione](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL di installazione driver](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Componenti di installazione](../../../odbc/reference/install/installation-components.md)
