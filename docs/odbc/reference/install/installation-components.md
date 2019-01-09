---
title: Componenti di installazione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a883377a17aa9e0c3426b4805263616375ea6215
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208780"
---
# <a name="installation-components"></a>Componenti di installazione
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows.  Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Il processo di installazione viene avviato quando l'utente esegue il programma di installazione. Il programma di installazione funziona in combinazione con il *DLL di installazione* e una *DLL di installazione driver* per ogni driver. Il programma di installazione sia il programma di installazione DLL utilizzare gli argomenti in di **SQLInstallDriverEx** e **SQLInstallTranslatorEx** funzioni per determinare quali file copiare o eliminare per ciascun componente. Nella figura seguente mostra la relazione tra questi componenti di installazione.  
  
 ![Relazione tra i componenti di installazione](../../../odbc/reference/install/media/pr29.gif "pr29")  
  
> [!IMPORTANT]
>  Il file Odbc.inf che è stato usato in ODBC 2. *x* per descrivere i file necessari per ogni ODBC componente non verrà utilizzata in ODBC 3*x*. I driver di ODBC 3*x* componenti non sono necessario creare un file Odbc.inf. La rimozione dei **la funzione SQLInstallDriver** e **la funzione SQLInstallODBC**e la rimozione del **SQLInstallTranslator**, hanno sottoposto a rendering Odbc.inf non necessari. Le informazioni del driver che erano nelle sezioni della parola chiave Driver del Odbc.inf sono ora disponibili nel *lpszDriver* nell'argomento **SQLInstallDriverEx**. Le informazioni di Microsoft translator che usato in [ODBC Microsoft Translator] e le sezioni specifiche di Microsoft Translator di Odbc.inf sono ora disponibili nel *lpszTranslator* argomenti del **SQLInstallTranslatorEx**. Queste modifiche consentono il programma di installazione ODBC garantire la portabilità tra piattaforme.  
  
 Per altre informazioni su questi componenti, vedere gli argomenti seguenti alla fine di questa sezione.  
  
-   [Programma di installazione](../../../odbc/reference/install/setup-program.md)  
  
-   [DLL di installazione](../../../odbc/reference/install/installer-dll.md)  
  
-   [DLL di installazione driver](../../../odbc/reference/install/driver-setup-dll.md)
