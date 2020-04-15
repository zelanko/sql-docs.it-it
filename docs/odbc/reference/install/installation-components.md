---
title: Componenti per l'installazione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
- ODBC [ODBC], component installation
ms.assetid: 9de15ca0-fe6a-4634-8709-a928d3c9cc73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a196e9b935229fa03c6dd0eda92b8e99e69f0ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285251"
---
# <a name="installation-components"></a>Componenti di installazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare ODBC in modo esplicito solo nelle versioni precedenti di Windows.  
  
 Il processo di installazione viene avviato quando l'utente esegue il programma di installazione. Il programma di installazione funziona insieme alla DLL del *programma di installazione* e a una DLL di installazione del *driver* per ogni driver. Sia il programma di installazione che la DLL del programma di installazione utilizzano gli argomenti nelle funzioni **SQLInstallDriverEx** e **SQLInstallTranslatorEx** per determinare i file da copiare o eliminare per ogni componente. Nella figura seguente viene illustrata la relazione tra questi componenti di installazione.  
  
 ![Relazione tra componenti di installazione](../../../odbc/reference/install/media/pr29.gif "pr29 (informazioni in stato di")  
  
> [!IMPORTANT]
>  Il file Odbc.inf utilizzato in ODBC *2.x* per descrivere i file richiesti da ogni componente ODBC non viene utilizzato in ODBC *3.x*. I driver che inspediscono i componenti ODBC *3.x* non è necessario creare un file Odbc.inf. La rimozione di **SQLInstallDriver** e **SQLInstallODBC**e la deprecazione di **SQLInstallTranslator**hanno reso Odbc.inf non necessario. Le informazioni sul driver che in precedenza si trovavano nelle sezioni Driver Keyword di Odbc.inf sono ora fornite nell'argomento *lpszDriver* in **SQLInstallDriverEx**. Le informazioni sul traduttore che in precedenza erano contenute nelle sezioni [ODBC Translator] e Translator Specification di Odbc.inf sono ora fornite nell'argomento *lpszTranslator* di **SQLInstallTranslatorEx**. Queste modifiche consentono al programma di installazione ODBC di essere più portabile tra le piattaforme.  
  
 Per ulteriori informazioni su questi componenti, vedere gli argomenti seguenti alla fine di questa sezione.  
  
-   [Programma di installazione](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL di installazione](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL di installazione driver](../../../odbc/reference/install/driver-setup-dll.md)
