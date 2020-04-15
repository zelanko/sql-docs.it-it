---
title: Componenti di configurazione - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37c2518c3b18423c804631780ee4a18bff29d88b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289012"
---
# <a name="configuration-components"></a>Componenti di configurazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare ODBC in modo esplicito solo nelle versioni precedenti di Windows.  
  
 Le origini dati vengono configurate dalla DLL del programma di installazione, che a sua volta chiama le DLL di installazione dei driver e le DLL di installazione del convertitore in base alle esigenze. La DLL del programma di installazione viene richiamata direttamente dal Pannello di controllo o caricata e chiamata da un altro programma, noto come programma di *amministrazione.* Nella figura seguente viene illustrata la relazione tra i componenti di configurazione.  
  
 ![Relazione tra componenti di configurazione](../../../odbc/reference/install/media/pr30.gif "pr30 (informazioni in base alla")  
  
 Per ulteriori informazioni su questi componenti, vedere gli argomenti seguenti alla fine di questa sezione.  
  
-   [Programma di installazione](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL di installazione](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL di installazione driver](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Componenti di installazione](../../../odbc/reference/install/installation-components.md)
