---
title: I componenti di configurazione | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: bcf7d34f8faf70f57373ad1a5dae55261799145b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198415"
---
# <a name="configuration-components"></a>Componenti di configurazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows.  Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Origini dati sono configurate dal programma di installazione DLL, che a turni chiamate driver installazione DLL e file DLL di installazione di Microsoft translator, se necessario. Il programma di installazione DLL è sia richiamata direttamente dal Pannello di controllo o caricata e chiamata da un altro programma, noto come il *programma di amministrazione*. Nella figura seguente mostra la relazione tra i componenti di configurazione.  
  
 ![Relazione tra i componenti di configurazione](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 Per altre informazioni su questi componenti, vedere gli argomenti seguenti alla fine di questa sezione.  
  
-   [Programma di installazione](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL di installazione](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL di installazione driver](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Componenti di installazione](../../../odbc/reference/install/installation-components.md)
